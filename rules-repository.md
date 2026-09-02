# Rules Repository (Living Document)

This document tracks the completeness and consistency rules we identify as we work
through each artifact type. Rules are grouped by artifact type (Use Case, Data Model,
etc.) and tagged by category. This is meant to grow incrementally — new rules get
appended as they surface, not designed all at once.

**Categories:**
- **Completeness** — a required element is present / filled in.
- **Consistency (Referential)** — a symbolic reference (ID, name) used in one place
  resolves to a real, defined entry elsewhere.
- **Consistency (Semantic)** — terms/concepts are used the same way across artifacts
  (not yet started — will matter once we compare use cases to the domain model/glossary).

**Status:**
- **Confirmed** — agreed and ready to implement in tooling.
- **Open** — identified but not yet fully resolved/agreed.

---

## Use Case Rules

| ID | Category | Rule | Notes | Status |
|---|---|---|---|---|
| UCR-001 | Consistency (Referential) | Every **Included Use Case** reference (`<<include>>`) resolves to a real Use Case ID in the model. | | Confirmed |
| UCR-002a | Consistency (Referential) | Every **Extends / Extended By** reference resolves to a real Use Case ID in the model. | Requires splitting the current single free-text field into two structured sub-fields: (1) Use Case ID, (2) Extension Point. See UCR-002b. | Confirmed |
| UCR-002b | Consistency (Referential) | The **Extension Point** on an `<<extend>>` relationship resolves to a real step number in the referenced base use case's Basic Flow (or Alternate Path). | Not yet checkable — template still stores this as unstructured text (`at [step # / condition]`). Template change required before this rule can be automated. | Open |
| UCR-003 | Consistency (Referential) | Every exception reference (`E#`) used in a Basic Flow, Alternate Path, or Exception Paths table resolves to a real entry in the centralized **Exception Registry**. | Exceptions are centrally defined and reusable across use cases, same pattern as Business Rules. | Confirmed |
| UCR-004 | Consistency (Referential) | Every Business Rule reference (`BR#`) resolves to a real entry in the centralized **Business Rules Repository**. | Use case's own Business Rules table becomes a reference list (BR ID + Name), not a redefinition. | Confirmed |
| UCR-005 | Consistency (Referential) | Every **Use Case Package** value resolves to an entry in a defined **Package Registry**. | Package registry/list still to be established; packages should reflect business capability, not architecture. | Confirmed |
| UCR-006 | Completeness | An **Alternate Path**'s branch point is recorded as the base Basic Flow step number, letter-suffixed (e.g. `3a`), per Cockburn Ch.8 convention. Rejoin point is implicit unless not obvious, in which case an explicit "Rejoins at step #" is required. | Resolves OI-002. Deliberate adoption of Cockburn's numbering, kept alongside (not replacing) our separate Alternate Path / Exception Path tables and centralized registries — a conscious divergence from his fully-inline Extensions model, made in favor of automatability. Watch-item: if this produces an exploding, unreadable list of near-duplicate exceptions at higher-level use cases (a failure mode Cockburn explicitly predicts), fall back to his "roll up failures into an included sub-use-case" pattern rather than the registry. | Confirmed |
| UCR-007 | Completeness | Exception/condition names describe what the **system detects**, not the actor's unobservable intent (e.g. "PIN entry time-out," not "customer forgot PIN"). | Direct adoption of Cockburn Guideline 11, no modification. | Confirmed |

## Data Model Rules

| ID | Category | Rule | Notes | Status |
|---|---|---|---|---|
| DMR-001 | Completeness | Subtype/supertype resolution (mutually exclusive entity variants, per data modeling deck 2) is a **Logical ERD** activity, not Conceptual. Conceptual ERD captures the variant as a plain attribute or an unresolved entity, without splitting into subtypes. | First concrete boundary drawn between Conceptual and Logical for this project. See DMR-002 for the general boundary statement this fits under. | Confirmed |
| DMR-002 | Completeness | **Conceptual ERD** scope: high-level entities, and only the *obvious* attributes and relationships, plus single/obvious Unique Identifiers (one straightforward `#` per entity) — no normalization, no data types, no supertype/subtype resolution (DMR-001), no resolution of many-to-many relationships, no alternative/multiple-UID validation. **Logical ERD** scope: adds reference/intersection entities (from M:M resolution), begins normalization, resolves supertypes/subtypes, and does alternative-UID validation/refactoring (multiple candidate UIDs, UID-driven discovery of missing entities). | General boundary statement, given as a deliberate project-specific definition — diverges from the source decks, which treat conceptual/logical as a single continuum. Grounded against deck 2: slides 3–14 (entities, attributes, relationships, single obvious UIDs) = Conceptual; slide 15 onward (alternative UIDs, refactoring, M:M resolution, supertypes, arcs) = Logical. Still open: where data type assignment falls (Logical vs. later/Physical) — not yet answered. | Confirmed |

---

Deferred design questions that aren't yet formal rules live in `../open-issues.md`,
not here — this file is for rules only, confirmed or open.
