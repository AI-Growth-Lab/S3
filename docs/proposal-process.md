# How analysis proposals work

This project treats **new analysis ideas as first-class contributions**. Anyone can suggest a new
way to analyse the bibliographic data with S3; the authors test promising ideas on the app and the
underlying data; validated ideas get built into [s3-bibliometric.com](https://s3-bibliometric.com/);
and the people who proposed them are credited as contributors.

## The lifecycle

Each idea moves through these stages, tracked with issue **labels**:

| Stage | Label | What happens |
|-------|-------|--------------|
| 1. **Idea submitted** | `analysis-idea` | You open an *Analysis idea* issue using the guided form. |
| 2. **Discussion** | `discussion` | The community and authors clarify the question, data, and method. |
| 3. **Testing on the app** | `testing` | The authors prototype the analysis on the app/data to see whether it produces robust, meaningful results. |
| 4a. **Accepted → in app** | `accepted`, then `in-app` | It's implemented in the app; a proposal file is added under `proposals/`; you're added to `CONTRIBUTORS.md`. |
| 4b. **Parked / declined** | `parked` / `declined` | If it isn't feasible or robust (for now), we explain why and keep the discussion for the future. |

## What makes a strong proposal

The clearest, most testable ideas move fastest. A strong proposal:

- answers a **specific question** ("Do funded papers cluster in the field's core or its periphery?")
  rather than a vague theme;
- can be computed from **data that is realistically available** — ideally fields already present in
  standard exports (Scopus / WoS / Dimensions / OpenAlex; see [`data-format.md`](data-format.md)),
  or a clearly named additional source;
- defines **how it would be computed**, at least roughly (an index, a per-community statistic, an
  overlay on the existing map …);
- is **generalisable** across fields, not specific to one corpus;
- explains **what it adds** beyond what the app already shows.

## Review criteria

When the authors evaluate an idea on the app, they look at: feasibility with available data,
robustness of the result across the two reference domains (and ideally others), interpretability,
and whether it complements (rather than duplicates) existing outputs.

## How crediting works

When your proposed analysis is validated and added to the project, you are credited as a contributor
in two ways:

1. **`CONTRIBUTORS.md`** — your name/handle and the analysis you contributed are listed.
2. **Repo contributor history** — either you open the pull request that adds your proposal file under
   `proposals/` (so you appear automatically in the contributor graph), or a maintainer adds it on
   your behalf using a `Co-authored-by:` commit trailer that names you.

Contributions of code, documentation, or review are credited the same way.

## Submitting

Open an issue from the **[💡 Analysis idea](../../issues/new/choose)** template and fill in the form.
That's it — no need to write any code to propose an idea. If you'd like to go further, you're welcome
to also draft a proposal file from [`../proposals/TEMPLATE.md`](../proposals/TEMPLATE.md) and open a
pull request.
