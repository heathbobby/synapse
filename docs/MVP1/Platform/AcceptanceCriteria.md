# MVP1 Platform Acceptance Criteria

- **Status**: draft MVP1 quality and acceptance baseline
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-05-quality-testing`
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

This document defines testable MVP1 acceptance criteria and a validation matrix
for the repository-first Synapse platform slice. MVP1 acceptance is measured by
canonical documentation, workflow/task-packet completeness, deterministic
validators, review-only gates, integration and handoff contracts, completion
signals, recovery behavior, and implementation handoff readiness.

MVP1 does not accept or require a visual workflow designer UI, hosted workflow
runtime, workflow-run database, product API, event bus, schema registry,
telemetry backend, approval automation, provider runtime, tenancy model,
compliance implementation, or legacy adapter.

## Source register

| Source | Acceptance use |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp1-iteration-05-quality-testing.md` | Iteration goal, role scope, completion criteria. |
| `docs/MVP1/Platform/TestingStrategy.md` | Gate statuses, deterministic validators, review-only checks, readiness blockers. |
| `docs/work_items/TECHNICAL_REFINEMENT_GATES.md` | Story/task readiness gates, metadata, agent-output gates. |
| `docs/work_items/INDEX.md` | MVP1 PRD/FR/E##/US trace and story sequencing. |
| `docs/MVP1/Platform/Features/WorkflowDesigner/Overview.md` | Feature capabilities, personas, user scenarios, feature acceptance expectations. |
| `docs/MVP1/Platform/Features/WorkflowDesigner/Workflows/CreateWorkflow.md` | Create Workflow happy, alternate, error, validation, approval, telemetry, and handoff paths. |
| `docs/MVP1/Platform/Integrations.md` | Integration objects, logical fields, owners, states, recovery, and telemetry/reference contracts. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Task-packet inputs, evidence discipline, output quality, completion signals, handoff expectations. |
| `docs/requirements/PRODUCT_REQUIREMENTS.md` | PRD trace IDs for canonical docs, orchestration, validation, handoff, backlog, and governance. |
| `docs/requirements/FUNCTIONAL_REQUIREMENTS.md` | FR trace IDs for workflow definitions, task packets, validation, completion signals, readiness, and dependencies. |

## Acceptance status values

Use these values for MVP1 validation summaries, readiness records, task packets,
handoffs, and review gates.

| Status | Meaning | Blocks readiness? |
| --- | --- | --- |
| `not-run` | Required validation or review has not been performed. | Yes, unless explicitly not applicable with rationale. |
| `passed` | Deterministic criterion passed with evidence. | No. |
| `failed` | Deterministic criterion failed. | Yes, until recovered and revalidated. |
| `review-needed` | Human review is required. | Yes, until approved or marked not applicable with rationale. |
| `approved` | Named reviewer accepted a review-only criterion with rationale. | No, within recorded limits. |
| `request-changes` | Named reviewer requires revision. | Yes, until changes are made and accepted. |
| `blocked` | Missing source, decision, owner, dependency, approval, or safe path prevents reliance. | Yes. |
| `needs-spike` | Bounded discovery is required before implementation-specific work can start. | Yes, except for the spike itself. |
| `not-applicable` | Criterion does not apply and rationale is recorded. | No. |

## Classification model

| Classification | Meaning | Required evidence |
| --- | --- | --- |
| Deterministic | Objective check can be repeated by script, CLI, CI, or manual inspection against fixed fields. | Target, rule, status, evidence, run context, owner for failures. |
| Review-only | Human judgment is required for product fit, evidence sufficiency, architecture fit, security/privacy, risk, or implementation readiness. | Reviewer role, evidence reviewed, decision, rationale, downstream effect, recovery action. |
| Both | Objective fields can pass while subjective sufficiency still requires review. | Deterministic evidence plus named review decision. |

## MVP1 validation matrix

All applicable criteria must be `passed`, `approved`, or `not-applicable` with
rationale before MVP1 work is implementation-ready. Any row with `failed`,
`blocked`, `needs-spike`, `request-changes`, unresolved `review-needed`, or
required `not-run` status blocks readiness for the affected scope.

| AC ID | Area | Trace | Acceptance criterion | Classification | Validation evidence | Blocks readiness when |
| --- | --- | --- | --- | --- | --- | --- |
| AC-MVP1-001 | MVP1 scope boundary | PRD-003, PRD-005; FR-005, FR-022; E02, E05 | Given an MVP1 platform or Workflow Designer artifact, when it states scope, then it describes CLI-assisted, repository-first, Markdown/configuration workflow contracts for the orchestration-framework domain and marks visual UI/runtime/API/storage/event/provider/tenancy/compliance/legacy work as future or open. | Both | Required section review plus product/architecture rationale. | Unsupported future-scope behavior is treated as committed implementation scope. |
| AC-MVP1-002 | Feature acceptance | PRD-003, PRD-005, PRD-008; FR-005, FR-006, FR-007, FR-008, FR-019, FR-020; E02-E05 | Given Workflow Designer MVP1 work products, when inspected, then workflow definition, task-packet, validation, dependency, handoff, and readiness expectations are explicit and traceable. | Both | Feature acceptance table or equivalent sections with trace and review decision. | Any core feature capability is missing, untraceable, or not reviewable. |
| AC-MVP1-003 | Workflow definition authoring | PRD-003, PRD-005; FR-005; E02; US-E02-001 | Given a workflow definition, when launch readiness is assessed, then it includes `workflow_id`, `phase_id`, `iteration_id`, domain scope, source packet, role bindings, deliverables, dependencies, validation expectations, completion criteria, and handoff audience. | Deterministic | Field-completeness check against workflow/configuration and input packet. | Required identity, source, role, deliverable, dependency, validation, completion, or handoff field is absent or ambiguous. |
| AC-MVP1-004 | Workflow creation happy path | PRD-003, PRD-005; FR-005, FR-006, FR-007, FR-008; E02, E03, E05; US-E02-001, US-E02-002, US-E03-001, US-E05-001 | Given canonical docs and an iteration input packet are available, when an orchestrator creates a workflow iteration, then task cards or equivalent role packets are generated or identified with required fields and runtime references where available. | Both | Create Workflow steps 1-9 represented in handoff, task-card references, validation summary, and review decisions. | The creation path cannot connect source packet, generated tasks, validation, review, or handoff outputs. |
| AC-MVP1-005 | Workflow creation alternate paths | PRD-002, PRD-005, PRD-008; FR-004, FR-005, FR-019, FR-020; E02-E05; US-E03-003, US-E04-003, US-E05-002 | Given sources, roles, write targets, dependencies, validation, or reviewers are incomplete, when creation can continue safely, then the workflow is narrowed to discovery, partial launch, coordinated shared ownership, validation exception, review revision, token-budget split, or future-scope decision with resulting state and owner. | Both | Alternate-path record with trigger, state, owner, affected work, and validation/review need. | Partial or narrowed work proceeds without state, owner, limitation, or recovery action. |
| AC-MVP1-006 | Workflow creation error and recovery paths | PRD-002, PRD-005; FR-004, FR-007, FR-008, FR-019; E03, E05; US-E03-003, US-E05-002 | Given a missing source, invalid packet, unsafe parallelism, command failure, prohibited edit risk, failed validation, missing reviewer, unavailable runtime reference, or open architecture/governance decision, when detected, then launch or downstream reliance is blocked until recovery owner, impact, preserved output, and required validation/review are recorded. | Both | Recovery record with trigger, affected targets, current state, impact, owner, recovery action, validation needed. | Error output is consumed as complete, or recovery lacks owner/impact/validation. |
| AC-MVP1-007 | Task-packet completeness | PRD-003, PRD-005; FR-006, FR-010; E02; US-E02-002 | Given a generated role-agent task packet, when pre-dispatch validation runs, then it includes role/objective, canonical sources, deliverables, prohibited edits, dependencies, acceptance criteria, validation expectations, handoff audience, and expected completion signal. | Deterministic | Required-field checklist against task packet or generated card. | Any required task-packet field is missing, empty, contradictory, or not bounded enough for assignment. |
| AC-MVP1-008 | Task-packet assignability | PRD-003, PRD-005, PRD-008; FR-006, FR-019, FR-020; E02, E04 | Given a task packet passes required fields, when assignability is reviewed, then the role scope, allowed write targets, dependencies, reviewer expectations, and downstream consumers are small enough and safe enough to execute. | Review-only | Orchestrator, validator owner, integrator, or tech lead decision with rationale. | The packet is too broad, lacks reviewer authority, has unsafe shared writes, or depends on unresolved upstream work. |
| AC-MVP1-009 | Requirements traceability | PRD-001, PRD-002, PRD-008; FR-001, FR-002, FR-018, FR-019; E01, E04; US-E01-005, US-E04-001 | Given an MVP1 artifact, workflow, task packet, validation result, work item, or handoff, when it makes acceptance or readiness claims, then applicable PRD, FR, E##, US-E##-###, workflow, phase, iteration, gate, validation, or runtime references are present and stable enough for Markdown cross-reference. | Both | Trace-marker check plus reviewer confirmation that trace is meaningful. | Required trace markers are missing, invalid, unstable, or tied to unpromoted raw/research claims. |
| AC-MVP1-010 | Evidence and uncertainty discipline | PRD-002; FR-002, FR-004, FR-010; E01, E05; US-E01-002, US-E01-004, US-E05-002 | Given an artifact includes material claims affecting scope, architecture, validation, security/privacy, dependencies, or operations, when reviewed, then claims are distinguishable as source-backed, inferred, assumed, or open. | Review-only | Evidence summary and reviewer rationale. | Assumptions or open questions are converted into implementation commitments. |
| AC-MVP1-011 | Source immutability | PRD-001, PRD-002; FR-003; E01; US-E01-003 | Given an MVP1 task executes, when the diff or change summary is inspected, then `raw/` and `research/` files are unmodified and prohibited edits are confirmed in the handoff. | Deterministic | Repository diff or equivalent changed-path summary; handoff confirmation. | Any `raw/` or `research/` file is modified without explicit future authority and recovery review. |
| AC-MVP1-012 | Deterministic validation scope | PRD-005, PRD-008; FR-007, FR-019; E03; US-E03-001 | Given MVP1 validation is run or recorded, when deterministic checks are applicable, then required files, required sections/headings, required metadata, trace markers, ID format, source immutability, contract-field completeness, future-scope guard, and completion-signal format are checked or marked not applicable with rationale. | Deterministic | Validation result records for each applicable check class. | Required deterministic checks are `not-run`, `failed`, lack evidence, or are silently skipped. |
| AC-MVP1-013 | Review-only gate separation | PRD-006, PRD-008; FR-014, FR-019; E03, E04 | Given quality, evidence sufficiency, architecture fit, product fit, risk, security/privacy, governance, reusable behavior, or implementation readiness cannot be objectively validated, when recorded, then it is labeled review-only with reviewer role, decision, rationale, affected downstream work, and recovery action. | Review-only | Human review/readiness gate record. | Subjective approval is implied by deterministic checks or lacks a named reviewer. |
| AC-MVP1-014 | Integration contract completeness | PRD-003, PRD-005, PRD-008; FR-005, FR-006, FR-007, FR-008, FR-019, FR-020, FR-022; E02-E05 | Given a workflow config, input packet, generated task card, memo/handoff, validation result, human review gate, telemetry reference, or recovery record, when accepted as an integration contract, then required logical fields, producer, consumer, owner, status, correlation, validation, approval, telemetry/reference, failure, and recovery semantics are present. | Deterministic | Contract-field checklist for IC-001 through IC-007 object types. | Owner, required fields, state, correlation, validation, approval, telemetry/reference, failure, or recovery fields are absent. |
| AC-MVP1-015 | Technology-neutral integration | PRD-005, PRD-009; FR-022; E02, E05 | Given an integration or event-like contract, when it describes boundaries, then it stays at command/document/logical-field level and does not select API protocol, event transport, storage, schema registry, runtime, telemetry backend, provider, tenancy, compliance, or legacy adapter. | Both | Future-scope guard plus architecture/integrator review. | An implementation technology is selected without accepted canonical decision. |
| AC-MVP1-016 | Handoff contract | PRD-003, PRD-005, PRD-008; FR-006, FR-008, FR-019; E03, E05; US-E03-002, US-E05-001 | Given agent or integrator work is handed off, when downstream consumers inspect it, then it names changed artifacts, validation performed/not performed, assumptions/open questions, risks/blockers, runtime/log references where material, follow-up owner, prohibited-edit confirmation, downstream safety, and completion signal. | Deterministic | Handoff or memo checklist. | Downstream safety is unclear or changed artifacts, validation status, prohibited-edit confirmation, blockers, owner, or completion signal are missing. |
| AC-MVP1-017 | Completion signals | PRD-003, PRD-005; FR-008; E03; US-E03-002 | Given specialist-agent work ends, when completion is reported, then it uses exactly one standard signal: `TASK_COMPLETE`, `TOKEN_BUDGET_LOW`, `BLOCKED`, or `PARTIAL_COMPLETE`, with required detail. | Deterministic | Completion-signal format validation. | Signal is missing, non-standard, or omits completed count, remaining paths, blocker impact, or recovery split as applicable. |
| AC-MVP1-018 | Validation result records | PRD-005, PRD-008; FR-007, FR-019; E03 | Given a validation result is created, when consumed by a gate or handoff, then it includes `validation_result_id`, `target_type`, `target_id`, `check_class`, `criteria`, `status`, `evidence`, `run_context`, `follow_up_owner`, and related decision/question IDs when applicable. | Deterministic | Validation result field-completeness check. | Result lacks required fields, evidence, status, owner for failure/review, or correlation to target. |
| AC-MVP1-019 | Dependency and concurrency safety | PRD-003, PRD-008; FR-006, FR-020; E02, E04; US-E02-003, US-E04-003 | Given multiple agents or tasks may run in parallel, when planning or dispatching, then upstream dependencies are stable and write targets are disjoint or one owner/merge contract is named. | Both | Dependency map/task-packet review and integrator decision. | Shared deliverables lack owner/merge contract or unstable upstream dependencies are ignored. |
| AC-MVP1-020 | Human review and approval records | PRD-006; FR-014, FR-019; E03, E04 | Given review is required for launch readiness, shared artifact ownership, deliverable acceptance, validation exception, reusable behavior change, or security/privacy/governance concern, when a decision is made, then reviewer role, evidence, decision, rationale, affected downstream work, and recovery action are recorded. | Review-only | Review gate record. | Named reviewer or rationale is missing, or downstream work proceeds after reject/request-changes/defer without recovery. |
| AC-MVP1-021 | Telemetry and log references | PRD-006, PRD-007; FR-013, FR-015, FR-016; E03, E05 | Given CLI invocations, generated task cards, memos, logs, branch/SHA references, validation outputs, or review notes are material, when recorded, then they are correlated to workflow/task/artifact/gate and classified as operational-only, summarized, canonicalized, unavailable, or not applicable. | Both | Runtime/reference record with correlation, durability, limitation, and reviewer decision when material. | Downstream trust depends on missing, non-durable, or uncategorized runtime evidence. |
| AC-MVP1-022 | Material runtime finding promotion | PRD-001, PRD-002, PRD-007; FR-001, FR-004, FR-016, FR-017; E01, E05 | Given runtime-only evidence changes implementation-relevant understanding, when downstream work needs it, then the material finding is summarized into canonical docs, work items, decisions, or handoff packages before reliance. | Review-only | Integrator or standards-owner decision and promoted reference. | Runtime-only context is treated as durable truth without canonical summary or accepted limitation. |
| AC-MVP1-023 | Security/privacy/governance blockers | PRD-002, PRD-006; FR-014, FR-019, FR-022; E04, E05 | Given sensitive data, access, approval policy, retention, tenancy, compliance, provider, or governance claims affect implementation, when reviewed, then each is classified known, assumed, open, not applicable, blocked, or needs-spike. | Review-only | Security/privacy or governance review record. | Unresolved governance topics are treated as implementation-ready. |
| AC-MVP1-024 | Failure and recovery completeness | PRD-002, PRD-005; FR-004, FR-007, FR-008, FR-019; E03, E05 | Given failed validation, review rejection, token limit, partial output, conflict, missing source, invalid packet, prohibited edit, or open decision occurs, when recovery is recorded, then trigger, affected targets, current state, preserved output, impact, owner, recovery action, and validation/review needed are present. | Deterministic | Recovery-record field check. | Recovery lacks owner, impact, preserved output, or validation/review required before reliance resumes. |
| AC-MVP1-025 | Backlog readiness gates | PRD-008; FR-018, FR-019, FR-020; E04; US-E04-001, US-E04-002, US-E04-003 | Given MVP1 epics or stories are used for implementation planning, when readiness is assessed, then product, traceability, architecture/technical, quality, dependency, risk, and implementation gates are visible with status and evidence. | Both | Story readiness table or work-item gate record plus reviewer approval. | A story/task is marked ready while any required gate is missing, blocked, needs-spike, or review-needed. |
| AC-MVP1-026 | Implementation handoff readiness | PRD-005, PRD-008; FR-005, FR-007, FR-008, FR-019, FR-020; E05; US-E05-001, US-E05-002 | Given MVP1 contracts are packaged for implementation, when the handoff is accepted, then launch sequence, owners, dependencies, accepted limitations, validation status, review decisions, blockers, recovery paths, source immutability, and remaining open decisions are explicit. | Both | Implementation handoff checklist and integrator/tech lead readiness decision. | Handoff lacks owner, sequence, validation/review status, blockers, or implementation-safe scope. |
| AC-MVP1-027 | Process-learning route | PRD-007; FR-016, FR-017; E05 | Given recurring validation gaps, packet defects, token-budget issues, blocked approvals, or quality problems are found, when the iteration closes, then candidate updates to standards, workflow templates, validators, personas, or backlog gates are named for review. | Review-only | Retrospective/handoff item with target promotion path and owner. | Repeated defects have no owner or promotion/recovery path. |

## Create Workflow path criteria

### CW-AC-001: Happy path

**Trace**: PRD-003, PRD-005; FR-005, FR-006, FR-007, FR-008;
E02, E03, E05; US-E02-001, US-E02-002, US-E03-001, US-E03-002,
US-E05-001.

**Given** accepted canonical docs, workflow configuration, role/persona
references, and an iteration input packet are available, **when** an orchestrator
starts or prepares a workflow iteration, **then** the resulting workflow/task
packet set:

- names workflow, phase, iteration, domain, source packet, roles, deliverables,
  dependencies, validation expectations, completion criteria, and handoff
  audience;
- generates or identifies bounded task cards or equivalent role packets;
- records runtime/log references when available and limitations when unavailable;
- validates required files, fields, sections, trace markers, source immutability,
  and completion-signal expectations;
- routes review-only gates to named reviewer roles; and
- publishes a handoff that states downstream work that may proceed and work that
  must wait.

**Readiness blocker**: any required field, validation result, review gate,
handoff audience, owner, or recovery path is absent.

### CW-AC-002: Alternate paths

**Trace**: PRD-002, PRD-005, PRD-008; FR-004, FR-019, FR-020;
E03-E05; US-E03-003, US-E04-003, US-E05-002.

| Alternate path | Acceptance criterion | Required state |
| --- | --- | --- |
| Discovery-only creation | If source or requirement context is incomplete but refinement is safe, then the packet is narrowed to discovery and avoids implementation claims. | `draft`, `partial-complete`, or `needs-spike` |
| Partial launch | If only some roles are ready, then only dependency-safe and disjoint work is launched; blocked roles and owners are recorded. | `running` with blocked packets |
| Shared artifact coordination | If more than one agent may edit one deliverable, then one owner or merge contract is recorded before dispatch. | `ready` only after ownership is explicit |
| Validation exception | If a deterministic check fails or is unavailable, then failed/not-run status, limitation, reviewer role, and recovery action are recorded. | `review-needed` or `blocked` |
| Review request changes | If a reviewer rejects or requests changes, then revised packet, recovery task, or open decision is created with downstream impact. | `needs-revision` or `blocked` |
| Token budget split | If an agent cannot complete within capacity, then `TOKEN_BUDGET_LOW` or `PARTIAL_COMPLETE` preserves output and lists remaining paths. | `partial-complete` |
| Future-scope detection | If unsupported UI/runtime/storage/event/telemetry/provider/tenancy/compliance/legacy specifics appear, then the claim is marked future/open or converted to a spike. | `blocked`, `deferred`, or `needs-spike` |

**Readiness blocker**: alternate output is consumed as complete without accepted
limitation or recovery.

### CW-AC-003: Error paths

**Trace**: PRD-002, PRD-005; FR-003, FR-004, FR-007, FR-008,
FR-019; E01, E03, E05.

| Error or blocker | Required acceptance behavior | Blocks readiness until |
| --- | --- | --- |
| Missing source packet or canonical source | Block launch, name missing source, impact, and source owner. | Source is supplied or scope is narrowed. |
| Ambiguous role boundary or reviewer | Keep task packet `draft` or `blocked`. | Role/reviewer owner is named. |
| Missing deliverable or write target | Add exact path, owner, and prohibited edits. | Packet is revalidated. |
| Unsafe parallelism | Assign one owner, sequence work, or split deliverables. | Integrator accepts coordination. |
| Command/task generation failure | Preserve command/log reference and failure class. | Cause is addressed and rerun/recovery is accepted. |
| Invalid task packet | Correct required fields before assignment. | Packet completeness passes. |
| Prohibited edit violation | Stop downstream reliance and assign recovery owner. | Impact is reviewed and remediated. |
| Failed deterministic validation | Record failed criterion, evidence, owner, and recovery task. | Revalidation passes or limitation is approved. |
| Review gate lacks reviewer | Block review-only approval. | Reviewer role is named and decision recorded. |
| Runtime/log reference unavailable | Record limitation and summarize material facts into durable docs if needed. | Limitation is accepted or durable summary exists. |
| Open architecture/governance decision | Mark open/deferred and avoid implementation commitment. | Decision is accepted or spike completes. |

## Task packet completeness checklist

**Trace**: PRD-003, PRD-005; FR-006, FR-010; E02; US-E02-002.

A task packet is assignable only when all applicable fields below are present.

| Field | Deterministic criterion | Blocks readiness when |
| --- | --- | --- |
| `task_packet_id` or path | Stable local identifier or generated card path exists. | Missing or duplicates another packet ambiguously. |
| Parent context | Workflow, phase, iteration, and source packet are named. | Parent context cannot be traced. |
| Role and objective | Named role and bounded outcome are explicit. | Scope is unclear or silently expands role authority. |
| Canonical sources | Required `docs/` sources and approved context are listed. | Work relies on unstated or raw/research-only source truth. |
| Deliverables | Exact artifact paths or output classes are named. | Agent cannot determine allowed write targets. |
| Prohibited edits | `raw/`, `research/`, and other prohibited paths/decisions are explicit. | Source immutability or scope boundaries are absent. |
| Dependencies | Upstream docs, decisions, stories, approvals, gates, or agent outputs are listed. | Blocking dependency is unstated. |
| Acceptance criteria | Testable or reviewable done criteria are included. | Success cannot be inspected. |
| Validation expectations | Deterministic checks, review checks, tests, or limitations are named. | Validation is unspecified. |
| Handoff audience | Downstream role, integrator, reviewer, or orchestrator is named. | Output has no accountable consumer. |
| Completion signal | Expected signal format is one of the standard signals. | Completion cannot be classified safely. |

## Integration and handoff contract checklist

**Trace**: PRD-003, PRD-005, PRD-006, PRD-008; FR-005, FR-006,
FR-007, FR-008, FR-013, FR-014, FR-019, FR-020, FR-022; E02-E05.

| Contract | Required acceptance fields | Readiness blocker |
| --- | --- | --- |
| Workflow config to input packet | Workflow/phase/iteration IDs, goal, role bindings, canonical sources, deliverables, prohibited edits, dependencies, completion criteria, validation expectations. | Missing source, ambiguous write target, unresolved role boundary, or config/input conflict. |
| Input packet to task card | Task ID/path, iteration, role, objective, sources, deliverables, prohibited edits, dependencies, acceptance criteria, validation, handoff audience, completion signal. | Packet is incomplete or unsafe to assign. |
| Agent execution to deliverable/memo | Producer, audience, status, related task, changed artifacts, validation summary, assumptions/open questions, runtime references, owner, completion signal. | Handoff omits validation, owner, or downstream safety. |
| Validation result | Validation ID, target type/ID, check class, criteria, status, evidence, run context, owner, related decision/question IDs. | Status/evidence/owner/correlation is missing. |
| Human review/readiness gate | Gate ID/family, target, reviewer role, evidence, decision, rationale, affected work, recovery action. | Reviewer or rationale is missing, or rejection has no recovery. |
| Telemetry/log reference | Reference ID/type/location, creator, related targets, summary, durability, limitations. | Material runtime reference is unavailable or non-durable without limitation. |
| Failure/recovery | Recovery ID, trigger, affected targets, current state, impact, preserved output, action, owner, validation needed. | Recovery is ownerless or unsafe output is consumed as complete. |

## Implementation handoff acceptance

**Trace**: PRD-005, PRD-008; FR-005, FR-007, FR-008, FR-019,
FR-020; E05; US-E05-001, US-E05-002.

MVP1 is ready for implementation handoff only when the handoff package includes:

1. Accepted MVP1 scope statement and explicit future-scope exclusions.
2. Launch sequence and dependency order for E01-E05 and related stories.
3. Workflow, task-packet, validation, review, integration, and recovery contract
   references.
4. Required owners: orchestrator, configuration owner, validator owner,
   reviewer/gate owners, integrator, recovery owners, and downstream consumers.
5. Validation matrix with every applicable criterion `passed`, `approved`, or
   `not-applicable` with rationale.
6. Review-only decisions with named reviewer roles, rationale, downstream
   effects, and accepted limitations.
7. Source-immutability confirmation for `raw/` and `research/`.
8. Handoff status and completion signal for each role output.
9. Remaining blockers, open decisions, needs-spike items, and work that must not
   proceed.
10. Assumptions and process learnings routed to standards, workflow templates,
    validators, personas, work items, or future backlog owners where applicable.

## Readiness blocker summary

Any of the following blocks MVP1 implementation readiness:

- Required canonical source, input packet, deliverable, task packet, reviewer,
  owner, dependency, or handoff audience is missing.
- Acceptance criteria are not testable or reviewable.
- Required deterministic validation is `not-run`, `failed`, or lacks evidence
  without approved limitation.
- Review-only criteria remain `review-needed`, lack a named reviewer, or have
  unresolved `request-changes`.
- Workflow/task-packet fields are absent, ambiguous, or contradictory.
- Shared write targets lack one owner or an explicit merge contract.
- PRD/FR, E##, US-E##-###, workflow, phase, iteration, task, gate, validation,
  or runtime references are missing where required for traceability.
- Source-backed, inferred, assumed, and open claims are conflated in material
  product, architecture, validation, security/privacy, dependency, or operations
  areas.
- Runtime/log-only evidence is required for downstream work but is unavailable,
  non-durable, or not summarized into canonical docs or handoff packages.
- `raw/` or `research/` files are modified without explicit future authority and
  recovery approval.
- Security, privacy, tenancy, access, compliance, retention, approval policy, or
  provider concerns are unresolved but treated as implementation-ready.
- Product/runtime/UI/storage/event/API/telemetry/provider/legacy implementation
  choices are asserted without accepted decisions.
- Integration or event-like contracts lack ownership, logical fields,
  correlation, validation, approval, telemetry/reference, failure, or recovery
  semantics.
- Agent handoff omits changed artifacts, validation performed/not performed,
  prohibited-edit confirmation, assumptions/open questions, blockers, downstream
  safety, or a valid completion signal.

## Assumptions

- Markdown-first structured headings and tables are sufficient for MVP1
  acceptance and validation until an E03 validator spike proves machine-readable
  schemas are required.
- The orchestration framework remains the first MVP1 workflow domain and
  validation target.
- Human reviewers remain accountable for product fit, evidence sufficiency,
  architecture fit, risk acceptance, security/privacy, governance, and final
  implementation readiness.
- Runtime task cards, memos, command outputs, logs, branch references, and SHAs
  are operational evidence unless summarized into canonical docs or handoff
  packages.

## Open decisions

| ID | Decision needed | Current MVP1 handling |
| --- | --- | --- |
| OQ-AC-001 | Which acceptance fields must become machine-readable for deterministic validators? | Keep Markdown-first contracts; use bounded E03 validator spike before adding schemas. |
| OQ-AC-002 | Who is the named accountable approver for each gate family? | Use role-based reviewer ownership until named individuals or teams are accepted. |
| OQ-AC-003 | Which validator checks run in CLI, CI, task generation, or integrator review? | Define objective behavior here; defer tooling placement to implementation planning. |
| OQ-AC-004 | What runtime/log references must be retained after orchestration runs? | Summarize material findings into canonical docs or handoff packages; leave retention policy open. |
| OQ-AC-005 | What event transport, schema registry, telemetry backend, approval policy, access-control, tenancy, compliance, provider, and legacy controls apply to future runtime work? | Treat as future/open and block implementation-specific claims until accepted decisions exist. |
