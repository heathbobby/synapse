# Execution Orchestration

- **Status**: draft canonical foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `concept-extraction`
- **Last updated**: 2026-05-03
- **Purpose**: Define the phase/MVP sequence, dependency gates, recovery paths,
  and next actions for moving Synapse from concept extraction into
  implementation-ready work.

## Source Register

| Source ID | Source | How this document uses it |
| --- | --- | --- |
| S1 | `docs/refinement/iteration-inputs/concept-extraction.md` | Current iteration goal, role scope, immutable-source rule, and completion criteria. |
| S2 | `docs/requirements/PRODUCT_REQUIREMENTS.md` | Product requirements, MVP framing, open questions, and uncertainty policy. |
| S3 | `docs/requirements/FUNCTIONAL_REQUIREMENTS.md` | Functional requirements for workflow definitions, validation, completion signals, readiness gates, and dependency mapping. |
| S4 | `docs/planning/DELIVERY_BACKLOG.md` | Candidate MVP sequence, epics, story seeds, readiness gates, and sequencing notes. |
| S5 | `docs/architecture/ARCHITECTURE.md` | Component boundaries, primary workflows, assumptions, and open architecture decisions. |
| S6 | `docs/architecture/TECHNICAL_SPECIFICATIONS.md` | Runtime states, conceptual data contracts, event families, and technical open decisions. |
| S7 | `docs/architecture/DECISIONS.md` | Accepted architecture direction and open architecture decision log. |
| S8 | `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md` | Prescriptive orchestration cadence, deterministic tooling model, completion gates, recovery patterns, and concurrency discipline. |

## Evidence and Confidence Policy

- **Source-backed** items are directly supported by the canonical docs or the
  playbook.
- **Assumption** items are sequencing choices needed for planning but require
  sponsor, product, or architecture confirmation before implementation.
- **Open decision** items block commitment until resolved in requirements,
  architecture, or backlog.
- Raw and research files remain immutable inputs. Implementation agents should
  cite canonical `docs/` artifacts as the working contract once this foundation
  is reviewed. [S1, S2, S7, S8]

## 1. Current State

The project is in **Phase 0: Seed Extraction and Canonical Foundation** for the
`concept-extraction` iteration. The canonical requirements, functional
requirements, architecture, technical specifications, decision log, and delivery
backlog now exist as draft foundation documents. This plan remains provisional
because first customer/domain, product mode, source systems, compliance
constraints, and MVP1 implementation depth are still open. [S1, S2, S4, S7]

## 2. Orchestration Principles

1. **Canonical truth first**: requirements, architecture, planning, standards,
   work items, and refinement docs must stabilize before implementation agents
   treat work as ready. [S2, S3, S4]
2. **Contracts before stack choices**: component boundaries, workflow state,
   event ownership, approval semantics, and traceability gates precede vendor or
   runtime selection. [S5, S6, S7]
3. **Sequential gates for dependent knowledge**: infrastructure and workflow
   definitions precede entities, integrations, features, quality, operations,
   and implementation handoff. [S4, S8]
4. **Parallel preparation, gated launch**: the orchestrator may prepare the next
   iteration while current agents run, but should not launch dependent work
   until upstream validation passes. [S8]
5. **Feedback must change future execution**: recovery and improvement work
   should update templates, workflows, role definitions, canonical docs, or
   backlog items, not only rerun failed agents. [S2, S3, S5, S8]

## 3. Candidate Phase and MVP Sequence

The MVP boundaries below are planning hypotheses. They should be used to
sequence refinement and backlog expansion, not as committed release scope until
the blocking open questions in the PRD and backlog are answered. [S2, S4]

| Sequence | Phase / MVP | Goal | Confidence | Primary backlog epics | Launch gate |
| --- | --- | --- | --- | --- | --- |
| 0 | Canonical foundation (`concept-extraction`) | Promote source inputs into canonical requirements, architecture, backlog, orchestration, and concurrency truth while preserving uncertainty. | High for process, medium for product specifics | E01 seed; planning docs | Source register complete; raw/research untouched; canonical docs distinguish source-backed facts, assumptions, open questions, and validation needs. |
| 1 | MVP1: Canonical concept-to-implementation pipeline | Support one initiative moving from canonical docs to traceable backlog, workflow definitions, deterministic validation, and execution handoff. | Medium-high | E01, E02, E03, E04, E05 | G0 foundation accepted; G1 decisions recorded: CLI-assisted delivery, orchestration framework as first domain, Markdown-first metadata, initial deterministic validator scope. |
| 2 | MVP2: Knowledge grounding and SME/persona templates | Add configurable source grounding, reusable persona templates, and domain configuration around the MVP1 pipeline. | Medium | E06, E07, E08 | MVP1 workflow/task-packet conventions stable; source types prioritized; persona composition decision made. |
| 3 | MVP3: Monitoring, approvals, and feedback-loop hardening | Add visible workflow status, approval checkpoints, feedback capture, and improvement-promotion mechanics. | Medium-low | E09, E10, E11 | Workflow state and completion signals stable; approval policy classes defined; feedback schema accepted. |
| 4 | MVP4: Legacy bridge workflow package | Apply Synapse to a validated legacy-to-greenfield transition scenario with bounded adapters and migration-planning artifacts. | Low | E12, E13 | Concrete legacy customer/domain, source corpus, compliance posture, and adapter boundaries validated. |
| 5 | Implementation handoff | Synthesize roadmap, team/workstream assignments, operational readiness, integration testing, and risk mitigation from accepted MVP docs. | Assumption | All accepted MVP epics | Target MVP set complete and audited; open implementation blockers recorded with owners. |

## 4. Standard Iteration Cadence Inside Each MVP

Use this cadence after an MVP scope and domain set are accepted. Deliverable
names may be adapted to Synapse, but the dependency order should remain stable
unless architecture records a replacement decision. [S4, S8]

| Iteration | Output focus | Primary dependencies | Gate to proceed |
| --- | --- | --- | --- |
| 1. Domain infrastructure | Domain/component overview, workflow boundaries, runtime/state assumptions, canonical paths. | Accepted MVP scope and domain list. | Infrastructure assumptions and open decisions documented; no unsupported stack commitments. |
| 2. Entities and data model | Conceptual records such as `WorkflowTemplate`, `WorkflowRun`, `PersonaDefinition`, `TaskCard`, `KnowledgeAsset`, `ApprovalDecision`, and audit/event records. | Iteration 1. | Entities map to requirements and architecture; storage choices remain open unless decided. |
| 3. Integrations and contracts | Event contract families, adapter boundaries, approval correlation, agent runtime boundaries, external systems. | Iteration 2. | Contract ownership, idempotency, retry/dead-letter, and audit needs documented. |
| 4. Feature specifications | User/operator/agent workflows, task-packet flows, backlog stories, acceptance criteria seeds. | Iterations 2 and 3. | Features trace to PRD/FR/backlog IDs and do not promote future MVP scope as current. |
| 5. Quality and acceptance | Test strategy, deterministic validation hooks, readiness gates, acceptance matrices. | Iteration 4. | Product, architecture, quality, dependency, risk, and implementation gates defined. |
| 6. Release and operations | Operational runbooks, recovery procedures, monitoring/approval operations, rollout notes. | Iteration 5. | Recovery paths, telemetry, approval queues, and rollback/rollback-equivalent actions documented. |
| 7. Implementation handoff | Roadmap, workstream ownership, risk mitigation, integration testing, open-blocker register. | Iterations 1-6. | MVP audit complete; unresolved decisions explicitly assigned and sequenced. |

## 5. Dependency Gates

### G0: Canonical foundation readiness

Required before launching MVP1 refinement:

- Product, functional, architecture, technical specification, decision, backlog,
  execution orchestration, and concurrency analysis docs exist in canonical
  `docs/` paths. [S1, S2, S3, S4]
- Each document distinguishes source-backed content, assumptions, open
  questions, and validation needs. [S1, S2, S3]
- Raw and research files remain unmodified. [S1, S3, S8]
- MVP1 hypothesis and its exclusions are visible, with uncertainty preserved.
  [S2, S4]

### G1: MVP1 scope and mode gate

Required before `mvp1-domain-infrastructure`:

- **Accepted**: MVP0/internal foundation delivery mode is CLI-assisted using the existing
  orchestration framework. Runtime-backed product behavior is deferred until
  MVP1 contracts and validators are stable. [ADR-0011]
- **Accepted**: the orchestration framework itself is the first internal
  domain/initiative that will drive workflow templates. [ADR-0012]
- **Accepted**: The internal foundation uses Markdown-first canonical metadata: structured
  headings and tables for PRD/FR IDs, E##/US-E##-### IDs, source confidence,
  readiness status, dependencies, owners/reviewers, and validation status.
  Machine-readable front matter/schema extraction is deferred to a later spike
  if E03 validators require it. [ADR-0013]
- **Accepted**: initial internal-foundation validators should check required files,
  required sections/headings, PRD/FR trace markers, E##/US-E##-### ID format,
  prohibited `raw/`/`research/` modifications, and completion-signal format.
  Review-only criteria remain labeled until automation is feasible. [ADR-0014]

### G2: Workflow/task-packet gate

Required before validation/completion-signal work:

- Workflow definitions list phases, dependencies, roles, source references,
  deliverables, and completion criteria. [S3]
- Task packets have disjoint write targets or explicit coordination contracts.
  [S3, S6]
- Completion signals cover full completion, partial completion, blocking
  decisions, and token-budget recovery. [S3, S8]

### G3: Knowledge/persona gate

Required before MVP2:

- Source types and retrieval/update mechanics are prioritized. [S2, S3, S4]
- Persona inheritance/composition representation is decided or bounded as an
  experiment. [S3, S5, S6, S7]
- Knowledge promotion includes review, confidence, freshness, and provenance.
  [S5, S6]

### G4: Governance/feedback gate

Required before MVP3:

- Workflow state model and event families are stable enough to support
  monitoring. [S5, S6]
- Approval classes and autonomy limits are defined. [S2, S3, S7]
- Feedback schema links quality issues and recurring failures to template,
  role, workflow, or process changes. [S3, S5, S8]

### G5: Legacy bridge gate

Required before MVP4:

- Validate a concrete legacy-transition customer/domain and source corpus.
  [S2, S3, S4]
- Define adapter read/write boundaries, authentication, rate limits, audit, and
  security/compliance constraints. [S5, S6, S7]
- Keep legacy adapters isolated from the domain-agnostic workflow/persona core.
  [S5, S6, S7]

## 6. Recovery Paths

| Failure or blocker | Detection signal | Recovery path | Resume gate |
| --- | --- | --- | --- |
| Missing or weak canonical source support | Requirement or backlog item lacks source/evidence or is based on unsupported specificity. | Reclassify as assumption/open question/validation need; do not promote to committed scope. | Source/evidence and confidence label added. |
| Validation failure | Deterministic checks report missing file, undersized content, missing section, or failed traceability. | Create a bounded recovery task/iteration for the failed artifact class; update completion criteria if the validator was ambiguous. | Validator passes or blocker is recorded with owner and downstream impact. |
| Token-budget or partial agent completion | Completion signal indicates partial work or missing target files. | Split remaining files by role/domain; use a recovery iteration or resumable agent session; lower future complexity allocation if repeated. | Remaining deliverables have disjoint scope and explicit completion signal. |
| Unsafe parallel write collision | Two agents modify the same deliverable or dependent artifacts without coordination. | Stop dependent work, reconcile through integrator review, assign single owner for the shared file, then relaunch downstream tasks. | Shared artifact has one owner or an explicit merge contract. |
| Open architecture decision blocks design | Work requires stack, storage, event transport, tenancy, compliance, or runtime choice not yet decided. | Add/confirm an open decision in the decision log and sequence a spike or stakeholder decision before implementation. | Decision accepted, or work is reframed as technology-neutral. |
| Approval or sponsor decision missing | Work depends on target customer/domain, autonomy level, product mode, or compliance constraints. | Park implementation; create validation task or sponsor decision request; continue only on non-dependent prep. | Decision captured in canonical docs/backlog. |
| Raw/research mutation risk | Agent edits `raw/` or `research/` or cites raw notes as implementation truth without promotion. | Revert only the unauthorized source mutation; preserve canonical derived work if valid; restate immutable-source rule in task packet. | Source file restored and canonical citation/provenance corrected. |
| Repeated quality drift | Similar formatting, scope, or evidence issues recur across iterations. | Promote the lesson into templates, role guidance, standards, or validation checks. | Future task packet includes the updated guidance. |

## 7. Next-Action Recommendations

### Immediate next actions after G1

1. Refine E02 using the accepted G1 decisions: CLI-assisted delivery, the
   orchestration framework as first domain, Markdown-first metadata, and the
   initial deterministic validator scope.
2. Draft the workflow/task-packet contract for the orchestration-framework
   domain, including required fields, source packet conventions, role ownership,
   write-target rules, and ready-to-consume memo shape.
3. Prepare E04 backlog readiness updates in controlled parallel only where
   write targets are disjoint and metadata terms are shared.
4. Keep runtime-backed product behavior, visual designer implementation, concrete
   storage/event/runtime choices, and external customer domains deferred until
   later gates.

### Recommended MVP1 launch order

1. E01: finalize canonical documentation foundation and metadata conventions.
2. E02: define workflow schema and task-packet template.
3. E04: draft backlog readiness gates in parallel with late E02 review where
   write targets are disjoint.
4. E03: implement or specify deterministic validation and completion signals
   once E02 contracts are stable.
5. E05: create the orchestration execution handoff after E02-E04 validate.

### Work to defer

- Visual drag-and-drop UI commitments until workflow template representation,
  state model, and first operator persona are validated.
- Concrete event transport, storage, model/runtime provider, tenancy, and cloud
  choices until requirements and compliance constraints stabilize.
- Legacy bridge implementation until a real transition-state corpus and adapter
  set are validated.

## 8. Completion Criteria for This Planning Document

This document is ready for parent/integrator review when it:

- Defines the candidate phase/MVP sequence without presenting it as committed
  release scope.
- Lists gates that connect product, functional, backlog, and architecture
  dependencies.
- Provides recovery paths for validation failures, partial completions, unsafe
  parallelism, and open-decision blockers.
- Recommends concrete next actions that preserve source uncertainty.
