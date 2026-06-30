# Metrics and citation definitions

This document defines the citation quantities and evaluation metrics used by S3.

## Citation quantities

For a community **c** within the retrieved corpus:

| Term | Meaning |
|------|---------|
| **Within citations** (`WithinC`) | Citations between papers that both belong to community *c*. |
| **Inward citations** (`InwardC`) | Citations that papers in *c* **receive** from papers in **other** communities. |
| **Outward citations** (`OutwardC`) | Citations that papers in *c* **make to** papers in other communities (its reliance on the surrounding field). |
| **Local citations** (`Local`) | `WithinC + InwardC` — in-field visibility and impact, confined to the study corpus. |
| **Global citations** (`Global`) | Total citations those same papers have accumulated across the entire bibliographic database (all disciplines and years) up to the retrieval date — broader, cross-field influence. |

Note the identity used for internal consistency checks: **`Local = WithinC + InwardC`**.

## Quality Index (QI)

QI measures the internal cohesion of a community: the average number of within-community citations
per paper.

```
QI_c = WithinC_c / Size_c
```

where `Size_c` is the number of papers in community *c*. A higher QI means papers in the community
cite each other more — a hallmark of a mature, consolidated research stream. QI is also the basis
for **comparing methods**: a clustering whose communities have higher QI has grouped papers that
actually exchange citations, not merely papers that look textually similar.

## Maturity Index (MI)

MI captures the share of all field-wide (local) citations that either originate within or flow into
community *c* — a single percentage-scale indicator of scholarly maturity.

```
MI_c = (WithinC_c + InwardC_c) / TotalLocalCitations  ×  100%
```

where `TotalLocalCitations` is the aggregate number of local citation links across the entire
retrieved dataset (including links involving smaller and emerging communities).

## Topic Coherence Index (TCI)

TCI measures the internal textual coherence of a cluster. For each paper it compares the paper's
TF-IDF term-probability vector with the mean TF-IDF vector of its cluster using the
**Jensen–Shannon Divergence (JSD)**:

```
JSD(P, Q) = 0.5 · KL(P ‖ M) + 0.5 · KL(Q ‖ M),   where M = 0.5 · (P + Q)
```

`KL` is the Kullback–Leibler divergence. Lower JSD ⇒ a less diverse set of words ⇒ higher textual
coherence. TCI is reported on a 0–1 scale (≈ `1 − JSD`); higher is better. A random keyword-search
baseline sits at roughly JSD ≈ 0.20 (TCI ≈ 0.80); ~0.90 is treated as a high-coherence benchmark.

Because JSD can vary with cluster size, evaluate coherence by comparing against random clusters of
matched sizes.

## Silhouette index

A standard clustering-quality metric combining **cohesion** (similarity within a cluster) and
**separation** (dissimilarity between clusters), averaged over all points. Higher ⇒ better-separated
clusters. For fair comparison across methods, compute all silhouette scores in the **same** semantic
vector space (SBERT embeddings). Absolute values are low for high-dimensional text, so interpret
relative to competing methods as well as against the 0.2 heuristic.
