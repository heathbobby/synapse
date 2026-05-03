# Technical Refinement Gates

- **Status**: draft canonical foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `backlog-refinement`
- **Last updated**: 2026-05-03
- **Purpose**: Define implementation-agnostic technical readiness gates for
  Synapse epics, stories, and executable tasks before implementation begins.

## Source Register

| Source ID | Source | How this document uses it |
| --- | --- | --- |
| S1 | `docs/refinement/iteration-inputs/backlog-refinement.md` | Iteration goal, required readiness gates, naming convention, and completion criteria. |
| S2 | `docs/architecture/ARCHITECTURE.md` | Component boundaries, architecture principles, data/state concepts, integration boundaries, assumptions, and open decisions. |
| S3 | `docs/architecture/TECHNICAL_SPECIFICATIONS.md` | Required capabilities, conceptual contracts, event families, non-functional requirements, and technical open decisions. |
| S4 | `docs/architecture/DECISIONS.md` | Accepted architecture direction and open architecture decision log. |
| S5 | `docs/planning/EXECUTION_ORCHESTRATION.md` | MVP sequencing, dependency gates, recovery paths, and technology-neutral orchestration principles. |
| S6 | `docs/planning/CONCURRENCY_ANALYSIS.md` | Safe parallelism, unsafe patterns, artifact ownership, and conflict recovery rules. |
| S7 | `docs/work_items/INDEX.md` | Work item naming convention and initial story readiness expectations. |
| S8 | `docs/standards/AI_AGENT_STANDARDS.md` | Agent role boundaries, evidence discipline, completion signals, and output expectations. |

## Scope and Principles

These gates apply to backlog items that use the `E##` epic and
`US-E##-###` story convention. They are intended for product owners, technical
leads, architects, dependency analysts, implementation agents, and integrators
who need to decide whether a story or task is ready to start.

1. **Canonical docs are the contract**: implementation-ready work must trace to
   canonical `docs/` sources. Raw and research material may inform refinement
   only after relevant claims are promoted into canonical docs. [S1, S2, S4]
2. **Contracts precede stack choices**: stories must define boundaries,
   contracts, state, validation, and operational needs without inventing
   storage, runtime, transport, UI, cloud, or agent-provider commitments. [S2,
   S3, S4, S5]
3. **Open decisions block implementation claims**: unresolved architecture,
   product, compliance, tenancy, event, storage, runtime, or domain decisions
   must be captured as blockers, spikes, assumptions, or validation tasks. [S4,
   S5, S6]
4. **Dependencies are explicit before fan-out**: safe parallelism requires
   stable upstream context, disjoint write targets, bounded ownership, and a
   deterministic validation or review gate. [S5, S6]
5. **Agent outputs must be reviewable**: task results must include evidence,
   changed artifacts, validation status, limitations, and the required
   completion signal. [S3, S8]

## Gate Status Values

Use consistent status labels in story metadata, task cards, or readiness
tables:

| Status | Meaning |
| --- | --- |
| `not-started` | The gate has not been assessed. |
| `ready` | The gate is satisfied and evidence is linked. |
| `blocked` | A required decision, dependency, source, or approval is missing. |
| `needs-spike` | The item requires bounded discovery before implementation. |
| `not-applicable` | The gate does not apply; rationale is recorded. |

## Required Story and Task Metadata

Before technical refinement can be marked `ready`, each story or implementation
task should record:

| Field | Requirement |
| --- | --- |
| Work item ID | Epic or story ID using `E##` or `US-E##-###`. |
| Problem / outcome | User, operator, workflow, or platform outcome in implementation-neutral terms. |
| Canonical sources | Links to requirements, architecture, decisions, standards, planning docs, or approved work-item artifacts. |
| Evidence class | Source-backed, inferred, assumed, or open for major claims and constraints. |
| Owner / reviewer | Accountable owner and required product, architecture, security, quality, or integrator reviewers. |
| Dependencies | Upstream stories, decisions, approvals, artifacts, events, integrations, or source assets. |
| Deliverables | Expected artifact paths or implementation outputs; shared files must have one owner or a merge contract. |
| Acceptance criteria | Product and technical acceptance criteria stated without stack-specific assumptions. |
| Validation approach | Deterministic checks, review checks, tests, or inspection criteria expected before completion. |
| Observability needs | Signals, audit records, metrics, logs, traces, or completion events needed to operate the work. |
| Security/privacy review | Data classes, access boundaries, approval needs, retention concerns, and open compliance questions. |
| Agent-output criteria | Required evidence, handoff summary, completion signal, and partial-completion behavior. |

## Technical Readiness Gate Checklist

### 1. Architecture Gate

A story or task is technically ready only when:

- The affected Synapse capability or component boundary is named, such as
  workflow designer, orchestration runtime, persona registry, task dispatcher,
  knowledge grounding, event bus, approval coordinator, legacy bridge, audit
  ledger, or telemetry layer. [S2, S3]
- The work states whether it changes workflow templates, runtime state,
  persona definitions, task cards, knowledge assets, events, approvals, audit
  records, or adapter boundaries. [S2, S3]
- Any architecture decision dependency is linked to an accepted ADR or open OAD.
  Work requiring an unresolved OAD is marked `blocked` or `needs-spike`. [S4]
- The proposed behavior preserves domain-agnostic design and does not hard-code
  a single vertical, customer, model provider, event transport, persistence
  technology, UI framework, or deployment model unless a canonical decision
  exists. [S2, S4]
- Human approval behavior is specified for policy-sensitive, high-risk, release,
  SME validation, or compliance-sensitive steps. [S2, S3, S4]

### 2. Data and Integration Gate

A story or task is technically ready only when:

- Conceptual records affected by the work are identified, using current
  architecture terms where relevant: `WorkflowTemplate`, `WorkflowRun`,
  `PersonaDefinition`, `TaskCard`, `KnowledgeAsset`, `EventContract`,
  `ApprovalDecision`, and `AuditRecord`. [S2, S3]
- Required inputs, outputs, identifiers, version fields, correlation IDs,
  source references, and ownership boundaries are described at the logical
  contract level. [S3]
- Integration boundaries are explicit, including whether the work touches agent
  runtimes, knowledge stores, legacy systems, communication/approval channels,
  telemetry sinks, or canonical documentation. [S2]
- Event-producing or event-consuming work identifies event family, owner,
  producer, consumer, schema-version expectation, idempotency expectation,
  retry/dead-letter expectation, and audit/replay need without selecting a
  specific transport prematurely. [S3]
- Legacy bridge work names adapter read/write boundaries, authentication or
  permission assumptions, rate-limit concerns, audit needs, and isolation from
  domain-agnostic workflow/persona models. If the legacy corpus or adapter set
  is not selected, the work is `blocked` or `needs-spike`. [S2, S3, S4]

### 3. Validation and Quality Gate

A story or task is technically ready only when:

- Acceptance criteria are testable or reviewable, including expected success,
  failure, blocked, partial-completion, and approval-required behavior where
  applicable. [S3, S5]
- Deterministic validation opportunities are identified before relying on
  manual review, such as required artifact paths, required sections, metadata
  presence, ID traceability, schema/contract consistency, or event-contract
  checklist completion. [S5]
- Review-only criteria are labeled when deterministic checks are not yet
  feasible, with the required reviewer role named. [S5, S8]
- Recovery behavior is defined for validation failure, token-budget or partial
  agent completion, stale upstream context, unsafe parallel write collision, and
  open-decision discovery. [S5, S6]
- The work does not depend on future MVP behavior unless that dependency is
  explicitly marked as deferred, external, or a blocker. [S5, S6]

### 4. Observability and Operations Gate

A story or task is technically ready only when:

- Required workflow, task, approval, event, persona, knowledge-loop, or adapter
  state changes are observable through named logical signals. [S2, S3]
- Correlation requirements are stated for workflow runs, task cards, events,
  approval decisions, artifacts, and agent outputs. [S3]
- Metrics or operational indicators are identified where useful, such as
  completion rate, step duration, approval cycle time, partial-completion rate,
  exception class, quality issue, or knowledge-loop adoption. [S3]
- Audit requirements are explicit when the work changes workflow definitions,
  persona behavior, knowledge assets, approval decisions, event contracts, or
  integration boundaries. [S2, S3]
- Operational failure modes and resume/rollback-equivalent behavior are
  documented when the work affects long-running workflows, approvals,
  integration adapters, or durable state transitions. [S3, S5]

### 5. Security, Privacy, and Governance Gate

A story or task is technically ready only when:

- Persona permissions, tool access, adapter access, and human approval authority
  are explicit for the scope of work. [S3]
- Data classification, sensitive data handling, tenancy isolation, compliance,
  retention, and access-control impacts are identified as known, assumed, open,
  or not applicable. [S3, S4]
- Knowledge promotion or persona/template changes that affect future agent
  behavior include review and attribution requirements. [S2, S3]
- Human approval records preserve approver, decision, rationale, evidence
  reviewed, timestamp, and resulting state transition when approval applies.
  [S2, S3]
- Work involving unknown compliance, tenant isolation, or sensitive integration
  boundaries is marked `blocked` or `needs-spike` rather than implementation
  ready. [S4, S5]

### 6. Dependency and Concurrency Gate

A story or task is technically ready only when:

- Upstream dependencies are linked, including canonical docs, requirement IDs,
  architecture decisions, workflow/task-packet conventions, validation gates,
  source inventories, approval policies, or external decisions. [S1, S5, S6]
- Parallel work is safe because write targets are disjoint or there is a single
  owner and explicit merge contract for shared deliverables. [S6]
- Sequencing respects current gates: G0 canonical foundation, G1 MVP1 scope and
  mode, G2 workflow/task-packet, G3 knowledge/persona, G4 governance/feedback,
  and G5 legacy bridge. [S5]
- The story names downstream impacts so dependent agents know what can and
  cannot launch after completion. [S5, S6]
- If implementation needs a stack, tenancy, compliance, storage, event transport,
  runtime, visual template, or agent integration decision that is still open,
  the work is reframed as technology-neutral refinement or a decision spike.
  [S4, S5, S6]

### 7. Agent-Output Gate

A story or task assigned to an agent is technically ready only when:

- The task packet names role, scope, allowed deliverables, prohibited edits,
  canonical source references, expected output paths, and completion criteria.
  [S3, S5, S8]
- Agent output expectations include changed artifacts, source/evidence summary,
  assumptions, open questions, validation performed, validation not performed,
  risks, and handoff notes for reviewers or downstream agents. [S8]
- The required completion signal is one of the standard signals in
  `docs/standards/AI_AGENT_STANDARDS.md`, and partial completion must identify
  completed target count, remaining paths, blockers, and recommended recovery
  split. [S8]
- Agent work that creates reusable learning states whether the learning should
  update canonical docs, workflow templates, persona definitions, standards,
  validators, or backlog items after review. [S2, S3, S8]
- The task forbids edits to `raw/` and `research/` files unless a future
  canonical rule explicitly grants that role authority. [S1, S2]

## Ready-for-Implementation Decision

A story or task may be marked technically `ready` when all required gates above
are `ready` or `not-applicable` with rationale. If any gate is `blocked` or
`needs-spike`, implementation should not start except for the bounded spike or
decision task named by the gate.

Recommended final readiness record:

| Gate | Status | Evidence / rationale | Owner |
| --- | --- | --- | --- |
| Architecture |  |  |  |
| Data and integration |  |  |  |
| Validation and quality |  |  |  |
| Observability and operations |  |  |  |
| Security, privacy, and governance |  |  |  |
| Dependency and concurrency |  |  |  |
| Agent-output |  |  |  |

## Accepted MVP1 Backlog Refinement Decisions

- **Metadata format**: Markdown-first structured headings and tables are
  canonical for MVP1 epics, stories, task cards, readiness gates, source links,
  and validation status. Machine-readable schemas are deferred until an E03
  validator spike proves the need.
- **Delivery mode**: MVP1 is CLI-assisted orchestration using
  `orchestration-framework/cli.py`, generated task cards, memos, and canonical
  docs. Runtime-backed product behavior is deferred.
- **First domain/initiative**: the orchestration framework itself drives the
  first concrete workflow templates and task-packet examples.
- **Initial validators**: required files, required sections/headings, PRD/FR
  trace markers, E##/US-E##-### ID format, prohibited `raw/`/`research/`
  modifications, and completion-signal format.

## Remaining Open Questions for Backlog Refinement

- Who approves each gate family for MVP1? Proposed defaults are product owner
  for product/value, architect or tech lead for architecture/technical, QA or
  standards curator for quality, dependency analyst for sequencing, security
  architect when sensitive data or approval policy is involved, and integrator
  for final ready-to-consume/merge status.
