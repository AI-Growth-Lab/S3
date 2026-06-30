# 0002 — Geographic & institutional spread of communities

- **Proposed by:** _example proposal_
- **Dimension:** Geography
- **Status:** 💡 Idea (example)
- **Date:** 2025-01-01
- **Issue / PR:** —
- **In app:** —

## Question
Where, geographically and institutionally, is each community concentrated? Are some Conceptual
Building Blocks driven by a few countries/institutions while others are globally distributed?

## Motivation
The intellectual structure of a field often has a geography. Mapping the countries and institutions
behind each community reveals regional specialisation, potential collaboration gaps, and whether
emerging communities are geographically narrow or broad.

## What it adds
Adds an **affiliation/geography** layer to the semantic map — complementing the content structure
with where the work comes from, which citations alone do not show.

## Data required
Author affiliation fields (country, institution) from Scopus / WoS / OpenAlex. Requires affiliation
parsing/normalisation (institution name disambiguation; ROR IDs via OpenAlex help).

## Method (sketch)
For each community: top countries and institutions by paper count; a concentration measure (e.g.,
share from the top country, or an HHI-style index) to flag narrow vs broad communities. Visual:
per-community country bars, or a choropleth filtered to a selected community.

## Validation / results notes
_To be filled during testing — affiliation coverage and disambiguation quality are the main risks._

## References
—

## Status history
- 2025-01-01 💡 Example proposal added to illustrate the format
