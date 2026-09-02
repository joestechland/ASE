# Pending Data Model Changes

Attributes/entities/relationships identified during use case work that need to be
**proposed to the colleague managing the ERD (Vasily)**, not applied directly. This
project doesn't own that model — this file is a request queue, not a registry.
Nothing here is real until Vasily confirms it and it actually appears in the model.

This file is meant to converge toward **empty** over the life of the project — every
row is a temporary state, not a permanent record. An entry leaving `Pending`/`Proposed`
and reaching `Applied` is success; a large, long-lived list here would mean the
use-case work and the data model are drifting apart faster than they're being
reconciled.

| ID | Entity | Change | Marker | Rationale / Source | Status |
|---|---|---|---|---|---|
| PDM-001 | HYPERLOGUE | Add attribute: **Hyperlogue Details Image**: "Becomes Thumbnail Picture: Image (e.g. jpg) (becomes part of title and description part of summary/screen)" | `o` (optional, per original use case) | Surfaced in UC-001 ("Create a Hyperlogue"); absent from colleague's current ERD screenshot — see OI:UC-001-17. To be raised with **Vasily**. | Pending |
| PDM-002 | AGREEMENT (candidate new entity) | Add entity: represents an Initiator-definable Participation Agreement — either selected from an existing list or uploaded — currently conflated with a plain confirmation flag on HYPERLOGUE in the use case. Needs its own entity with a relationship to HYPERLOGUE, distinct from the yes/no confirmation itself. | n/a (new entity) | Surfaced in UC-001; not present in colleague's ERD at all — see OI:UC-001-13 | Pending |
| PDM-003 | HYPERLOGUE | Resolve conflict: use case marks Participant/Initiator Token Contribution as mandatory (`*`, BR4, default = 0); colleague's ERD marks `initiator contribution` / `participant contribution` as optional (`o`). Needs a single agreed answer, not two sources disagreeing. | Conflict — `*` vs `o` | Surfaced in UC-001 / data model cross-check — see OI:UC-001-15 | Pending |
| PDM-004 | HYPERLOGUE / Hyperlogue Configuration | Resolve modeling approach for "Type of Hyperlogue": use case treats it as a flat attribute; project convention (DMR-001) defers subtype/supertype split to Logical; colleague's ERD instead folds `hyperlogue type` into the **Hyperlogue Configuration** entity's identifier — a third, config-driven approach. Needs a deliberate choice among the three. | n/a (structural approach, not a single field) | Surfaced in data model cross-check — see OI:UC-001-16 | Pending |

## Conventions

- ID prefix `PDM-###`, sequential, never reused.
- **Status values:** `Pending` (identified, not yet raised) → `Proposed` (raised with
  colleague) → `Accepted` / `Rejected` (colleague's decision) → `Applied` (confirmed
  present in an updated model export/screenshot).
- When a change is `Applied`, cross-reference the use-case-level issue it resolves
  (e.g., an `OI:UC-xxx-##` entry) so both sides of the link are traceable.
- This file records *proposed* changes only — it is never a substitute for the real
  ERD, and nothing here should be treated as authoritative model content.
