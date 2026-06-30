# Input data format

S3 works from a standard bibliographic export. The **minimum** required fields are the **title**
and **abstract** of each paper. To run the citation-analysis and validation steps (QI, MI,
local/global citations) you also need **references / cited-by** information and **publication year**.

## Supported sources

Exports from any major scientific database work, including:

- **Scopus** (CSV or RIS)
- **Web of Science** (tab-delimited / plain text / RIS)
- **Dimensions** (CSV)
- **OpenAlex** (JSON / CSV via the API)

## Recommended columns

| Field | Required | Used for |
|-------|----------|----------|
| `title` | ✅ | embeddings |
| `abstract` | ✅ | embeddings |
| `year` | ◻ (for time-masking & MI) | directed graph, maturity |
| `references` / cited references | ◻ (for citation analysis) | QI, MI, local citations |
| `cited_by` / times-cited | ◻ | global citations |
| `doi`, `authors`, `source/venue` | ◻ | bookkeeping, optional co-authorship analysis |

## Reproducibility

When contributing a new analysis, please include:

- the **exact database queries** used to retrieve the corpus (see the paper's Appendix B for the
  Scopus query format),
- the retrieval **date** and database,
- any filters (document types, language, subject areas).

Large raw exports should **not** be committed to the repository — see [`../data/README.md`](../data/README.md).
