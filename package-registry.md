# Package Registry (Living Document)

Central, controlled list of Use Case Packages. A package must appear here before any
use case can reference it (UCR-005). Packages reflect **business capability**, not
technical/architectural structure.

| Package | Description | Seeded By |
|---|---|---|
| Manage Hyperlogue | Business capability covering the creation, moderation, and lifecycle of Hyperlogues. | UC-001 (Create a Hyperlogue) |

## Conventions

- A new package is added here the first time a use case needs it — this registry is
  bootstrapped by real use cases, not designed up front (same pattern as the Rules
  Repository and Open Issues list).
- Package names are exact-match. A use case referencing a near-miss spelling or
  phrasing creates a phantom duplicate, not a reference to the real entry — this is
  exactly what UCR-005 exists to catch.
