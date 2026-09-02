# UC-001 (Create a Hyperlogue) — Open Issues

Package: Manage Hyperlogue
Uses the same `OI:UC-xxx-##` ID scheme as the global `open-issues.md`, just stored
here since these are specific to this one use case. This file is meant to shrink
toward empty as the use case matures — that's success, not something to fill back up.

| ID | Description | Raised During | Status |
|---|---|---|---|
| OI:UC-001-01 | Version — header field blank | UC-001 completeness review | Open |
| OI:UC-001-02 | Author — header field blank | UC-001 completeness review | Open |
| OI:UC-001-03 | Priority — header field blank (MoSCoW, per project convention) | UC-001 completeness review | Open |
| OI:UC-001-04 | Included Use Cases: "Fill out HL details w/o publishing" is a name, not a Use Case ID (UCR-001 requires resolution to a real ID). Does that use case exist yet? | UC-001 completeness review | Open |
| OI:UC-001-05 | Basic Flow table has only Step 1 and Step 4 — Steps 2 and 3 are missing | UC-001 completeness review | Open |
| OI:UC-001-06 | Step 1's System Response cell mixes 4 distinct kinds of content: (a) legitimate system prompts, (b) branching alternatives (items a–e) that belong in Alternate Paths, (c) HYPERLOGUE entity field definitions (OI-011, global) that don't belong in the use case at all, (d) open design questions/dev notes not part of the narrative | UC-001 completeness review | **In Progress** — field definitions being moved to the data model by the analyst; awaiting reload of revised use case |
| OI:UC-001-07 | Business Rules table: BR 1–4 have IDs but blank/garbled Name+Description — may be a PDF-extraction artifact; needs checking against the real source doc | UC-001 completeness review | Open |
| OI:UC-001-08 | Where the line sits between a true Business Rule and a plain data/structural constraint (e.g., "Max must be 1 greater than Min") — never resolved, analyst's call pending | UC-001 completeness review | Open |
| OI:UC-001-09 | HYPERLOGUE entity, "Type of Hyperlogue" attribute — mandatory/optional marker missing | UC-001 / data model cross-check | Superseded — see OI:UC-001-16 |
| OI:UC-001-10 | HYPERLOGUE entity, "Maximum Number of Participants" marked optional, but BR3 discusses it as if always relevant — possible contradiction | UC-001 / data model cross-check | Resolved — colleague's ERD shows `max participants` as mandatory (`*`), consistent with BR3 |
| OI:UC-001-11 | HYPERLOGUE entity, "Maximum Number of Matches" — no marker; may be a derived/read-only value | UC-001 / data model cross-check | Likely resolved — ERD shows `number of evaluations per participant`, mandatory. **Unconfirmed:** same field renamed, or different concept? |
| OI:UC-001-12 | Candidate missing entity: **TOKEN** — internal structure (Symbol+Type) and multiple values per Hyperlogue | UC-001 / data model cross-check | Resolved — Token exists as its own entity in colleague's ERD |
| OI:UC-001-13 | Candidate missing entity: **AGREEMENT** — confirmation flag conflated with a selectable/uploadable document | UC-001 / data model cross-check | **In Progress** — logged as `PDM-002` in `data-model/pending-changes.md`, to be raised with Vasily |
| OI:UC-001-14 | "Initiator Token Contribution"'s tie to BR4 is unconfirmed — source text was truncated at that point | UC-001 completeness review | Open |
| OI:UC-001-15 | **Conflict:** use case marks Participant/Initiator Token Contribution as mandatory (`*`, BR4, default = 0). Colleague's ERD marks both as optional (`o`). Two sources disagree on the same fact. | UC-001 / data model cross-check | **In Progress** — logged as `PDM-003` in `data-model/pending-changes.md`, to be raised with Vasily |
| OI:UC-001-16 | "Type of Hyperlogue" doesn't appear as a Hyperlogue attribute in colleague's ERD; instead `hyperlogue type` is part of the **Hyperlogue Configuration** entity's identifier — a config-driven approach, materially different from a flat attribute or a subtype split (DMR-001). Needs a deliberate choice, not an accident. | UC-001 / data model cross-check | **In Progress** — logged as `PDM-004` in `data-model/pending-changes.md`, to be raised with Vasily |
| OI:UC-001-17 | "Hyperlogue Details Image": "Becomes Thumbnail Picture: Image (e.g. jpg) (becomes part of title and description part of summary/screen)" — doesn't appear on Hyperlogue in colleague's ERD. Must be raised with **Vasily** (colleague managing the data model). | UC-001 / data model cross-check | **In Progress** — logged as `PDM-001` in `data-model/pending-changes.md`, to be raised with Vasily |
| OI:UC-001-18 | 8/27 note: type of HL is a "set" value, read-only based on whether started from Draft or Template. If changeable after load, what happens to body/content that changes based on HL type? | UC-001 content review | Open |
| OI:UC-001-19 | Size limit on HL submissions — how to enforce, and should images/video be stored directly or only as links? | UC-001 content review | Open |
| OI:UC-001-20 | Can linked content be displayed inline when a description is entered/loaded (dev question)? | UC-001 content review | Open |
