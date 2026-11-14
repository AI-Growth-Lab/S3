# `src/` — reference implementation

> **An open implementation is available now:** the Python library
> [s3-bibliometric](https://github.com/AI-Growth-Lab/s3-bibliometric)
> (`pip install s3-bibliometric`) follows the published method step by step (embeddings,
> time-masked S3 matrix, Leiden with SII threshold choice, c-TF-IDF, QI and MI) and adds a
> literature-review report, a map comparison and an MCP server for Claude. Start there to build or
> test a new analysis; the [step-by-step guide](https://ai-growth-lab.github.io/S3/) shows how to run it.

This folder holds the S3 source code. If you are importing an existing (possibly
rapidly-prototyped) implementation, a suggested module layout is:

```
src/
└── s3/
    ├── __init__.py
    ├── embeddings.py     # Step 1: encode titles+abstracts (SBERT)
    ├── matrix.py         # Step 2: cosine S3 matrix + time-masking (γ)
    ├── communities.py    # Step 3: thresholding + Leiden + elbow/scree selection
    ├── characterize.py   # Step 4: c-TF-IDF labels (+ optional LLM)
    ├── citations.py      # Step 5: Within/Inward/Outward/Local/Global, QI, MI
    ├── metrics.py        # TCI (JSD), Silhouette helpers
    ├── pipeline.py       # orchestrates steps 1–6
    └── io.py             # load Scopus/WoS/Dimensions/OpenAlex exports
```

Keep each step independently callable so contributors can swap in alternative embedding models,
thresholding strategies, or community-detection algorithms. See [`../docs/method.md`](../docs/method.md)
for what each step should do and [`../docs/metrics.md`](../docs/metrics.md) for the metric formulas.

> Tip: the hosted app at https://s3-bibliometric.com/ is the canonical full-featured
> implementation; this folder is where an open, reviewable version of that pipeline should live.
