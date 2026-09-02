# To-Do List

Quick-glance index of what's waiting on whom. Full detail lives in the trackers this
file points to — this is a summary, not a third copy of the same facts. Check things
off here as they resolve in the underlying file. Success looks like this list empty.

---

## Waiting on Joe

- [ ] Reload revised UC-001 once the current data-model cleanup pass is done
- [ ] Raise PDM-001 through PDM-004 with Vasily → `data-model/pending-changes.md`
- [ ] Decide: edit the `.dotx` template now to add the Extends/Extended-By field, or hold
      → OI-001 in `open-issues.md`
- [ ] Design Business Rules Repository structure (ID, Name, Description, Category, Source?)
      → OI-005
- [ ] Design Exception Registry structure → OI-006
- [ ] Confirm whether a dedicated DFD reference source is still coming, or the data
      modeling decks' light DFD coverage is all we're working from → OI-010
- [ ] Decide where data type assignment happens (Logical vs. later/Physical) → DMR-002
      in `rules/rules-repository.md`
- [ ] Confirm CRUDA/CRUN matrix timing: strictly post-hoc, or some interleaving while
      writing a use case? (never explicitly confirmed, currently assumed post-hoc)
- [ ] Upload all repo files to GitHub and share access/orientation with Vasily —
      where things live and how to find them (see `README.md` for the folder map)
- [ ] UC-001 header fields still blank: Version, Author, Priority
      → OI:UC-001-01/02/03 in `use-cases/examples/UC-001-issues.md`
- [ ] UC-001 content questions: does the included use case ("Fill out HL details w/o
      publishing") exist yet with an ID? → OI:UC-001-04
- [ ] UC-001: confirm Business Rules table Name/Description gaps against the real
      source doc (may just be a PDF-extraction artifact) → OI:UC-001-07
- [ ] UC-001: where the line sits between a Business Rule and a plain data constraint
      → OI:UC-001-08
- [ ] UC-001: confirm "Maximum Number of Matches" ↔ "number of evaluations per
      participant" are the same field → OI:UC-001-11
- [ ] UC-001: confirm Initiator Token Contribution's tie to BR4 → OI:UC-001-14
- [ ] Answer the three UC-001 dev notes (type-of-HL read-only behavior, submission size
      limits, inline linked-content display) → OI:UC-001-18/19/20

## Waiting on Zach

- [ ] Review the revised UC-001, once uploaded, against the current tracker
      (`use-cases/examples/UC-001-issues.md`)
- [ ] Nothing else pending right now — everything else is waiting on a decision or
      an upload from Joe

## Conventions

- This list is a **summary index**, not the source of truth — always resolve the
  underlying tracker item, then check the box here.
- New waiting-on-Joe or waiting-on-Zach items get added here the moment they're
  identified, same as everything else in this project.
