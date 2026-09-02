# Open Issues

Backlog of things surfaced during the work that are deliberately **not** being resolved
now. Nothing here gets acted on until it's pulled off this list on purpose. Anyone
picking this repo up should read this before assuming a gap is an oversight.

**This file is for global/methodological issues only.** Use-case-specific issues live
in their own per-use-case file (e.g. `use-cases/examples/UC-001-issues.md`), using the
same `OI:UC-xxx-##` ID scheme described below — just stored separately, so a
use case's tracker can shrink toward empty as it matures without cluttering this file.

| ID | Description | Raised During | Status |
|---|---|---|---|
| OI-001 | Use Case template has no field for `<<extend>>` relationships. Once added, it must be two structured sub-fields (Use Case ID + Extension Point), not one free-text field, or UCR-002b can't be automated. Decision pending: edit template now vs. after more real examples. | Use Case template review | Open |
| OI-002 | ~~No defined convention for how an Alternate Path records which Basic Flow step it branches from, or where (if at all) it rejoins.~~ | Use Case template review | **Resolved** — see UCR-006 in `rules/rules-repository.md` (Cockburn step+letter convention, e.g. `3a`) |
| OI-003 | No Package Registry exists yet. Naming convention undecided beyond "business capability, not architecture" — no actual list started. **Resolved (seeded):** registry created at `registries/package-registry.md`, first entry "Manage Hyperlogue" from UC-001. Stays Open in the sense that governance beyond the first entry (e.g., who can add a package, how near-duplicates get caught) hasn't been defined. | Use Case template review; seeded by Create a Hyperlogue package assignment | Open (seeded) |
| OI-004 | Is there a distinct transitional/elaboration layer between analysis and design models (e.g., non-1:1 use-case-to-component mappings)? Surfaced from the `<<extend>>` discussion but broader than just that. | Use Case template review | Open |
| OI-005 | Business Rules Repository structure (fields: ID, Name, Description, Category, Source?) not yet designed — only agreed that it should exist and be centralized. | Use Case template review | Open |
| OI-006 | Exception Registry structure not yet designed — same situation as OI-005; likely similar shape. | Use Case template review | Open |
| OI-007 | Where/how the project's documents ultimately get hosted (git repo vs. Claude Project vs. shared drive) is decided in principle (git repo) but not yet actually set up/pushed anywhere. | Repo location discussion | Open |
| OI-008 | How to replicate/distribute this setup (repo + Claude Project + instructions) to colleagues so they can work from the same methodology/tooling — a "deployment" concern for the methodology itself, mapped to the Stage 8 (Deployment) placeholder in the lifecycle skeleton. | Colleague-sharing discussion | Open |
| OI-009 | CRUD operations on data, identified during use case elicitation, should eventually cross-check against real entities/attributes in the data model (ERD). **Resolved (process):** a Function/Entity (CRUDA) and Function/Attribute (CRUN) matrix will be built incrementally — each use case's surfaced data gets pulled into a running, lightweight entity/attribute list (informal, no UIDs/relationships resolved yet) as it's written, and the matrices are checked against that growing list. The list itself becomes the seed of the real Conceptual ERD. | CRUD elicitation discussion; refined by data modeling deck review | Resolved (process) — mechanics only; no actual matrix or entity list exists yet |
| OI-010 | Reference books for DFD and ERD conventions named but not yet provided. **Update:** ERD conventions now provided (4 data modeling decks) — conceptual/logical ERD, normalization, and design/physical transformation are covered. DFD is only lightly touched (one slide) in that material — still open whether a dedicated DFD source is coming separately. | Analysis activities list discussion; ERD portion resolved by data modeling deck upload | Open (DFD portion only) |
| OI-011 | Field/attribute definitions embedded in "Create a Hyperlogue" (Title, Description, Participation min/max, token fields, etc., using `*`/`o` notation) confirmed to belong to a **HYPERLOGUE entity**, not the use case itself. The entity hasn't been formally defined yet. **Path forward per OI-009:** these become the first entries in the running entity/attribute list, rather than waiting for a fully-built ERD. Extraction itself not yet performed. | Create a Hyperlogue review / data modeling deck review | Open |
| OI-012 | Does an `<<include>>`d use case's completion return control to the base use case, and where in the flow does it rejoin? UCR-001/UCR-002a only require the reference to resolve to a real ID — neither says anything about return/rejoin behavior, unlike UCR-006 which covers this for Alternate Paths. Cockburn's own material (the "Save Work" sub-use-case example) shows control returning to a specific step after the included use case succeeds — worth checking whether that pattern should become a rule here too. | UC-001 review (raised alongside its own `<<include>>` reference, see UC-001's own tracker) | Open |
| OI-013 | ~~Watch-item: all use-case-specific issues living in this same file, tagged `OI:UC-xxx`, risked becoming unwieldy at scale.~~ | Tracker consolidation discussion | **Resolved** — split into per-use-case files (this file for global only), same `OI:UC-xxx-##` ID scheme retained across both |

## Conventions for this list

- New items get an ID and go here the moment something is deliberately deferred
  rather than solved in the moment.
- **Generic/methodological items** get `OI-###` (project-wide sequence) and live here.
- **Use-case-specific items** get `OI:UC-xxx-##` (the use case's ID, then a sequence
  local to that use case) and live in that use case's own tracker file — e.g.
  `OI:UC-001-05` in `use-cases/examples/UC-001-issues.md`. Same ID scheme everywhere,
  split storage by scope.
- When an item is resolved, don't delete the row — mark it **Resolved** and note where
  the resolution lives (e.g., a rule ID in `rules/rules-repository.md`, a template
  change, a decision doc).
