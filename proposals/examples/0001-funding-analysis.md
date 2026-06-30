# 0001 — Funding profile of communities

- **Proposed by:** _example proposal_
- **Dimension:** Funding
- **Status:** 💡 Idea (example)
- **Date:** 2025-01-01
- **Issue / PR:** —
- **In app:** —

## Question
How is research **funding** distributed across the Conceptual Building Blocks that S3 identifies?
Do funded papers sit in the field's **core** (mature, internally cohesive communities) or at its
**emerging periphery**, and which **funders** are associated with which communities?

## Motivation
Funding shapes which research directions grow. Overlaying funding on the S3 map would let
researchers, funders, and policymakers see where money is concentrated, spot well-funded emerging
areas, and identify under-funded but conceptually central communities.

## What it adds
The current app characterises communities by citations (QI, MI, local/global). This adds an
orthogonal **resource** dimension — funded vs unfunded share per community, top funders per
community, and whether funding correlates with the maturity (MI) or centrality of a community.

## Data required
Funding/grant fields from the bibliographic export:
- **Scopus**: funding sponsor / funding acknowledgement fields.
- **Dimensions**: rich funder and grant metadata (often the best source).
- **OpenAlex**: `grants` / funder information.
Coverage is uneven (not all papers report funding), so results should report a coverage rate.

## Method (sketch)
For each community *c*: compute the share of papers with any funding; the distribution of funders
(e.g., top-5 by paper count); and a per-community **funding intensity** = funded papers / size.
Optionally test association between funding intensity and MI/QI across communities. Visual: colour
or size the community nodes on the existing S3 map by funding intensity.

## Validation / results notes
_To be filled during testing — e.g. does the funding signal hold across both reference domains, and
is coverage high enough to be meaningful?_

## References
—

## Status history
- 2025-01-01 💡 Example proposal added to illustrate the format
