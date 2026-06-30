# The S3 method, step by step

This document explains how the Semantic Similarity Score (S3) constructs the intellectual
structure of a research field. S3 is built around three design decisions:

1. **Network structure is determined exclusively by the semantic content of papers** — what they
   say — rather than by citation links or term co-occurrence.
2. **A temporal-ordering constraint** is applied so the network encodes intellectual genealogy,
   not merely similarity.
3. **Citation analysis is re-introduced only at a later stage** — not to build the map, but to
   characterise and validate the communities the content analysis reveals.

The pipeline has six steps.

---

## Step 1 — Compute text embeddings

Each paper's title and abstract are concatenated and encoded with a pre-trained sentence
transformer. The reference model is
[`sentence-transformers/all-mpnet-base-v2`](https://huggingface.co/sentence-transformers/all-mpnet-base-v2),
which maps each paper into a 768-dimensional vector. The model is chosen for its strong
performance on semantic-search and clustering tasks.

**Input:** title + abstract (the minimum required fields).
**Output:** one dense vector per paper.

---

## Step 2 — Build the S3 matrix and apply time-masking

Compute the pairwise **cosine similarity** between every pair of paper vectors. This produces a
symmetric S3 matrix in which each entry is the semantic similarity of two papers.

To turn similarity into *genealogy*, the matrix is **time-masked** using publication dates: for a
pair of papers, the edge is oriented from the earlier to the later publication, yielding a
**directed graph** that respects the chronological development of ideas.

An optional parameter `γ` controls whether citation information is blended into the construction of
the graph:

- `γ = 0` — pure semantics (used in the paper's empirical analyses, to isolate the effect of
  content and avoid contaminating the map with citation data that is later used for validation).
- `γ > 0` — re-introduce direct citations, co-citations, or bibliographic coupling into the S3
  construction. This makes the framework complementary to traditional bibliometrics and is
  available in the web app.

A worked example of the time-citation adjustment is included in the paper (Appendix D).

**Output:** a directed, time-masked similarity graph.

---

## Step 3 — Detect communities

Apply an optimal **similarity threshold** to keep only sufficiently strong edges (the paper sweeps
thresholds in the range 0.75–0.85 and selects the value that best balances sensitivity and
inclusion). Records with no strong semantic connection drop out at this stage.

Partition the thresholded graph with the **Leiden** algorithm, which finds the community structure
that maximises modularity.

To separate the core *Conceptual Building Blocks* from a long tail of micro-communities, plot the
communities in descending size order and locate the inflection point (the **elbow / scree** method).
The paper selects the top 10 communities per field; smaller clusters are treated as outliers or
nascent emerging topics.

**Output:** a set of research communities, with a chosen top-*N* as the field's building blocks.

---

## Step 4 — Characterise topics

Each community is labelled from its most distinctive vocabulary using **class-based TF-IDF
(c-TF-IDF)**. Labels can optionally be refined with a large language model (LLM) that reads the
top terms together with the titles/abstracts of the community's most central papers and proposes
an interpretable label. The full prompt-engineering and verification protocol is described in the
paper (Appendix A).

**Output:** a human-readable label and description for each community.

---

## Step 5 — Citation analysis

Citations are now re-introduced **strictly as a descriptive attribute** — never as the basis for
the map. They are used to characterise communities (maturity, impact) and to **validate** that the
content-derived structure reflects real scholarly exchange.

The metrics computed here — Within / Inward / Outward / Local / Global citations, the **Quality
Index (QI)**, and the **Maturity Index (MI)** — are defined in [`metrics.md`](metrics.md).

The logic of validation: if the content-based communities are meaningful, papers should cite
*within* their community more than *across* communities. A higher within-community citation density
is therefore evidence that the map captures the field's true intellectual structure.

**Output:** validated, characterised communities with citation-based attributes.

---

## Step 6 — Assemble the intellectual structure

Combine the content-based community structure with the citation-based attributes into a single
visual map of the field: the communities (Conceptual Building Blocks), their semantic links, and
their maturity and reach. This is the deliverable a researcher uses to read the field, isolate
specific debates, trace genealogies, and spot emerging frontiers.

---

## Why this design

- **Timeliness.** Because the map is built from content, it is not delayed by citation
  accumulation and can place very recent, uncited papers.
- **Robustness to citation bias.** Homophily, the Matthew Effect, strategic and negative citation,
  and field-specific citation cultures do not distort the underlying map.
- **Interpretability.** Citation metrics are retained, but as validation and description rather
  than as the structural skeleton.

S3 is a **complement** to traditional bibliometric methods, not a replacement: content provides
the intellectual map while citation and co-authorship analyses continue to provide structural and
social scaffolding.
