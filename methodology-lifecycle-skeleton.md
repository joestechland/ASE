# Requirements-to-Code Methodology — Lifecycle Skeleton (v0.1)

## Purpose

A repeatable, tool-supported, AI-agent-assisted process for transforming application
requirements into architecture, detailed design, and executable code — with
traceability and automated consistency checking at every hand-off.

## Guiding Principles

0. **Methodology shape (decided 2026-08-29):** Organize around RUP's *shape* —
   phases/milestones, disciplines, defined artifacts-per-discipline — without adopting
   RUP's full prescriptive weight (its specific roles, templates, and artifact volume).
   Target: easy to understand, use, and follow. Open tension to watch: RUP's heaviness
   comes from the discipline × artifact matrix itself, not just paperwork — "borrow the
   shape, keep it light" requires actively cutting disciplines/artifacts we don't need,
   not just trimming templates. ICONIX (a deliberately lightened, use-case-driven
   descendant of RUP) is a closer reference point than RUP itself, given the workflow
   already in use here (use case → domain model → design → code).
1. **Every artifact is machine-readable, not just human-readable.** Prose descriptions
   are fine as commentary, but the authoritative content of each stage's deliverable
   should live in a structured format (YAML, JSON, JSON Schema, OpenAPI, a graph/model
   file, etc.) so scripts and agents can validate and transform it, not just read it.
2. **Every downstream artifact traces to an upstream one.** No design element without
   a requirement/architecture parent; no code module without a design parent. This is
   what makes impact analysis and consistency checking possible.
3. **Transforms are explicit and separately testable.** "Turn requirements into
   architecture" is not one big prompt — it's a defined transform with defined inputs,
   outputs, and a validation step, so we can improve or swap the transform without
   redesigning the whole pipeline.
4. **Agents are narrow and stage-specific**, each with a bounded context (only the
   artifacts relevant to its stage) rather than one generalist agent doing everything.
5. **Human review gates exist between stages**, at least initially — the goal is a
   trustworthy accelerant, not an unsupervised pipeline (though later stages could
   tighten the loop as confidence grows).
6. **The methodology is technology-agnostic in principle**, but we'll validate it
   concretely against the Web/Mobile app you'll describe.

---

## Cross-Cutting Concerns (apply to every stage)

| Concern | Description |
|---|---|
| **Artifact Registry** | A single index of every artifact ever produced (requirement R-014, component C-03, endpoint E-12, etc.) with stage, version, status, and links to parents/children. |
| **Traceability Model** | The graph connecting artifacts across stages (requirement → architecture element → design element → code unit → test case). |
| **Consistency Checking** | Scripts that validate structural rules within and across stages (e.g., "every API endpoint in the design has a corresponding requirement," "no orphaned components," "naming conventions followed"). |
| **Change Impact Analysis** | When an upstream artifact changes, identify every downstream artifact that may now be stale. |
| **Version Control** | All artifacts live in a repo; stage transforms are effectively "compilations" from one commit state to the next. |
| **Agent Orchestration** | How agents are invoked (manually per stage vs. a driver script), what context each gets, and how human review gates are inserted. |

---

## Stage-by-Stage Skeleton

### Stage 1 — Requirements Elicitation & Specification
- **Purpose:** Capture *what* the system must do, for whom, and under what constraints.
- **Inputs:** Stakeholder input (interviews, notes, existing docs), business goals.
- **Outputs:** Structured requirements set — functional (user stories / use cases),
  non-functional (performance, security, compliance), constraints, glossary of terms.
- **Candidate format:** Structured YAML/Markdown-with-frontmatter per requirement, or
  Gherkin-style scenarios for functional behavior; a glossary as a term/definition table.
- **Transform:** Elicitation agent interviews/parses raw input → drafts structured
  requirement records with IDs.
- **Validation:** Every requirement has an ID, category, acceptance criteria, and
  priority; no duplicate/conflicting requirements (semantic-similarity check); glossary
  terms used consistently.
- **Agent:** Requirements Analyst agent.
- **Human gate:** Stakeholder sign-off on requirement set.

### Stage 2 — Domain Modeling
- **Purpose:** Establish the shared conceptual model — entities, relationships, business
  rules — independent of any technical architecture.
- **Inputs:** Requirements set + glossary.
- **Outputs:** Domain model (entities, attributes, relationships, invariants/business rules).
- **Candidate format:** A model file (e.g., JSON/YAML entity-relationship spec, or a
  UML-class-diagram-as-code format like PlantUML/Mermaid source).
- **Transform:** Domain Modeling agent extracts entities/relationships from requirements.
- **Validation:** Every noun-concept in requirements maps to a domain entity or is
  explicitly excluded; no entity without at least one requirement justifying it.
- **Agent:** Domain Modeler agent.
- **Human gate:** Domain expert review.

### Stage 3 — Architecture Definition
- **Purpose:** Define the system's structural decomposition — logical components,
  technology choices, deployment topology (web + mobile + backend + data stores),
  integration points, cross-cutting concerns (auth, logging, etc.).
- **Inputs:** Requirements (esp. non-functional), domain model.
- **Outputs:** Architecture description — component/container diagrams (C4-style),
  technology stack decisions, deployment diagram, key architectural decisions (ADRs).
- **Candidate format:** C4 model as code (Structurizr DSL / Mermaid) + ADR markdown
  files + a machine-readable component registry (JSON/YAML listing components, their
  responsibilities, and interfaces).
- **Transform:** Architecture agent proposes component decomposition satisfying
  functional + non-functional requirements.
- **Validation:** Every non-functional requirement addressed by at least one
  architectural decision; every domain entity owned by exactly one component;
  no circular component dependencies (unless explicitly justified).
- **Agent:** Architect agent.
- **Human gate:** Architecture review board / lead review.

### Stage 4 — Detailed Design
- **Purpose:** Design each component to the level needed for implementation — APIs,
  data schemas, internal module structure, UI/UX screens and flows (web + mobile),
  state management, error handling.
- **Inputs:** Architecture, domain model, requirements.
- **Outputs:** API specs, data schemas, component-internal design docs, UI wireframes/flows,
  sequence diagrams for key flows.
- **Candidate format:** OpenAPI/GraphQL SDL for APIs; JSON Schema for data; Mermaid
  sequence diagrams; a structured screen/flow spec for UI (screens, components, states,
  transitions) usable by both web and mobile design.
- **Transform:** Designer agent(s) — possibly split into API Designer, Data Designer,
  UI/UX Designer — produce specs component-by-component.
- **Validation:** Every architecture component has a design; every API operation traces
  to a requirement; data schema consistent with domain model; UI flows cover all use
  cases.
- **Agent:** Detailed Designer agent(s) (API / Data / UI specializations).
- **Human gate:** Design review, esp. API contract review.

### Stage 5 — Code Generation / Implementation
- **Purpose:** Produce executable code from the detailed design.
- **Inputs:** API specs, data schemas, UI/flow specs, chosen tech stack.
- **Outputs:** Source code — backend services, web frontend, mobile app, database
  migrations, generated API clients.
- **Candidate format:** Actual source repo, organized to mirror the component structure
  from Stage 3.
- **Transform:** Code Generator agent(s) per layer (backend, web, mobile, data), using
  design specs as the authoritative contract; scaffolding tools generate boilerplate
  (e.g., OpenAPI → server stubs + client SDKs) where mechanical generation is reliable,
  agents fill in logic where judgment is needed.
- **Validation:** Generated code compiles/builds; API implementation matches spec
  (contract testing); linting/style conformance; static analysis.
- **Agent:** Code Generator agent(s), specialized per stack layer.
- **Human gate:** Code review (PR-style), even if AI-assisted.

### Stage 6 — Test Design & Generation
- **Purpose:** Derive test cases directly from requirements and design so coverage is
  traceable, not incidental.
- **Inputs:** Requirements (acceptance criteria), design specs, code.
- **Outputs:** Unit tests, integration tests, end-to-end/UI tests, test data.
- **Candidate format:** Test code in the target framework(s); a traceability matrix
  mapping requirement → test case(s).
- **Transform:** Test Generator agent derives tests from acceptance criteria + API/UI specs.
- **Validation:** Every requirement's acceptance criteria has ≥1 covering test;
  every API operation has contract tests.
- **Agent:** Test Engineer agent.
- **Human gate:** Test plan review for critical paths.

### Stage 7 — Verification, Validation & Traceability Audit
- **Purpose:** Confirm the whole chain is consistent end-to-end and that the built
  system actually satisfies the original requirements.
- **Inputs:** All artifacts from Stages 1–6.
- **Outputs:** Traceability report, gap/orphan report, test results summary,
  requirements coverage report.
- **Candidate format:** Generated report (markdown/HTML) from the artifact registry + graph.
- **Transform:** Consistency-checking scripts + a Reviewer agent that interprets results
  and flags risks.
- **Validation:** This *is* the validation stage — it's the audit layer.
- **Agent:** Reviewer/Auditor agent.
- **Human gate:** Final sign-off before release.

### (Stage 8 — Deployment/Release — likely out of scope for the methodology's core focus, but worth a placeholder for CI/CD, environment config, and release notes generation, since those also trace back to non-functional requirements.)

---

## Open Design Questions to Resolve as We Go

1. **Format choices per stage** — do we commit to specific formats now (e.g., Gherkin
   for requirements, C4/Structurizr for architecture, OpenAPI for APIs) or trial a
   couple against the real app first?
2. **Granularity of agents** — one agent per stage, or finer-grained (e.g., separate
   API/Data/UI designer agents in Stage 4)?
3. **Orchestration** — manual stage-by-stage invocation (you drive it, reviewing
   between each), or a scripted pipeline with human gates only at key checkpoints?
4. **Where "the tools" live** — a real code repo with scripts (Python/Node) we build
   alongside the methodology, versus purely prompt-based agent instructions? (My
   assumption: a real repo, since consistency-checking scripts need to actually run.)
5. **How much of this is web/mobile-specific** — Stage 4 (UI/UX) and Stage 5 (code
   generation) will need web- and mobile-specific sub-tracks once we know the app.

---

*This is a v0.1 skeleton — every stage above will get its own deep-dive spec (exact
artifact schema, exact agent prompt/persona, exact validation rules, exact tooling)
before we call it "done."*
