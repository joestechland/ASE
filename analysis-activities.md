# Analysis Activities

Running list of the distinct analysis activities that make up this work. Each activity
gets fleshed out (conventions, template, rules) in its own time, in order — this list
just tracks what's in scope and its current state so nothing gets lost.

| # | Activity | Depends On | Status |
|---|---|---|---|
| 1 | **Use case narratives → design specifications → code.** Write use cases per the template/conventions being established, then map them forward into design specs, then into code (modular layered architecture). | Use case template finalized (in progress) | In Progress |
| 2 | **Data Flow Diagrams (DFDs).** Show system/data integration; identify data usages that appear as entities and attributes, cross-checked against the Entity Relationship Diagram. | DFD reference book (pending — OI-010) | Blocked |
| 3 | **Entity Relationship Diagram (ERD) / data model.** The relational data model itself — entities, attributes, relationships — that DFD data usages and use case CRUD findings both cross-check against. | ERD reference book (pending — OI-010) | Blocked |

## Notes

- Activity 2 and 3 are tightly coupled — DFD data usages are only meaningful once
  checked against real ERD entities/attributes, and vice versa. Likely need to work
  them close together once both reference books are available, rather than fully
  sequentially.
- CRUD findings from use case elicitation (see `docs/claude-project-instructions.md`)
  are a third thing that will eventually cross-check against the ERD — effectively a
  three-way consistency check once all three activities are underway: Use Case CRUD ↔
  DFD data usage ↔ ERD entities/attributes.
- State Transition Diagrams were mentioned earlier as also in scope but aren't yet a
  numbered activity here — add once we get to them.
