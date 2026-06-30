# Contributing to S3

The S3 project grows through community **analysis ideas**. The primary way to contribute is to
**propose a new analysis** — no coding required. You can also contribute code, docs, or review.

> **Licensing note.** This project is MIT-licensed (see [`LICENSE`](LICENSE)). By contributing you
> agree to release your contribution under the same license. If the maintainers later adopt a
> different license (e.g. **Apache-2.0** for a patent grant, or **GPL-3.0** for copyleft), that will
> be decided openly via an issue.

## 1. Propose an analysis (no code needed) ⭐

Open a **[💡 Analysis idea](../../issues/new/choose)** issue and fill in the short form. The authors
review it, test promising ideas on the app and data, and — if validated — build them into
[s3-bibliometric.com](https://s3-bibliometric.com/). The full lifecycle and crediting rules are in
[`docs/proposal-process.md`](docs/proposal-process.md); current ideas live in
[`proposals/`](proposals/README.md).

**When your idea is adopted, you are credited as a contributor** in
[`CONTRIBUTORS.md`](CONTRIBUTORS.md) and in the repository's history.

## 2. Contribute an implemented analysis or code

Once an idea is accepted, you (or a maintainer) can add the implementation under `examples/`,
`notebooks/`, or `src/`. Include the data source, exact query, and retrieval date — but **not** large
raw datasets (see [`data/README.md`](data/README.md)).

## 3. Improve the method or harden the code

Better embedding models, threshold selection, community detection, the time-masking / citation
(`γ`) step, or new metrics are all welcome. Parts of the app were built quickly with AI assistance,
so refactoring, tests, type hints, and docs are especially valuable. Open an issue to discuss larger
changes first.

## Workflow for pull requests

1. **Fork** and branch: `git checkout -b feature/short-description`.
2. Commit in small, clear steps.
3. If you accept an analysis, copy [`proposals/TEMPLATE.md`](proposals/TEMPLATE.md) to
   `proposals/NNNN-short-name.md`, add a catalogue row, and credit the proposer.
4. Open a **PR** and fill in the template.

## Style

Python: target a recent Python 3, follow **PEP 8**, and consider `black` + `ruff` before submitting.
Readable and working beats perfect. Be respectful — see the [Code of Conduct](CODE_OF_CONDUCT.md).
