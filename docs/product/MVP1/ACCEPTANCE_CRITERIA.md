# Synapse Product MVP1 Acceptance Criteria

- **Status**: QA lead draft
- **Product slice**: MVP1 AI coworker workspace for one approved expert workflow
- **Last updated**: 2026-05-03

## Purpose

This document defines product acceptance criteria for the Synapse MVP1 AI
coworker workspace. MVP1 acceptance is measured by whether a human operator can
define a destination, select the approved product concept-to-implementation
workflow, attach approved knowledge, dispatch bounded AI coworker work, monitor
progress, review and approve outputs, assemble an implementation handoff,
capture learning, and preserve audit/governance accountability.

These criteria are product-facing and tool-agnostic. They may use the current
CLI-assisted orchestration artifacts as prototype evidence, but the accepted
product behavior is the Synapse workspace experience, logical runtime contract,
and human decision model.

## Source basis

| Source | Acceptance use |
| --- | --- |
| `docs/refinement/iteration-inputs/product-mvp1-ai-coworker-workspace.md` | Defines MVP1 as a product workspace and separates Synapse from prototype scaffolding. |
| `docs/product/MVP_STRATEGY.md` | Defines the MVP1 product goal and capability scope. |
| `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md` | Provides SYN-PRD trace IDs for knowledge, workflow coordination, review, learning, accountability, and product boundary. |
| `docs/product/PRODUCT_CAPABILITY_MAP.md` | Provides CAP trace IDs for workflow authoring, task packets, governance, monitoring, and learning. |
| `docs/product/MVP1/AI_COWORKER_WORKSPACE.md` | Provides MVP1 requirements, objects, review gates, outputs, learning, and non-goals. |
| `docs/product/MVP1/OPERATOR_JOURNEY.md` | Provides the end-to-end operator journey and journey success criteria. |
| `docs/product/MVP1/WORKSPACE_UX_SPEC.md` | Provides UX surfaces, state labels, actions, error states, and readiness checklist. |
| `docs/product/MVP1/RUNTIME_CONTRACTS.md` | Provides logical objects, states, validation rules, governance rules, audit concepts, and open decisions. |
| `docs/MVP1/Platform/AcceptanceCriteria.md` | Provides acceptance status values, deterministic/review-only classification, handoff, recovery, and source immutability patterns. |
| `docs/MVP1/Platform/TestingStrategy.md` | Provides quality gates, readiness blockers, validation evidence, review-only checks, and recovery expectations. |

## Acceptance status values

Use these values when recording MVP1 product acceptance, review gates, handoff
readiness, learning disposition, or validation summaries.

| Status | Meaning | Blocks product acceptance? |
| --- | --- | --- |
| `not-run` | Required validation or review has not been performed. | Yes, unless explicitly `not-applicable` with rationale. |
| `passed` | Deterministic criterion passed with evidence. | No. |
| `failed` | Deterministic criterion failed. | Yes, until recovered or accepted as a limitation by the right reviewer. |
| `review-needed` | Human judgment is required. | Yes, until approved, rejected, deferred, or marked not applicable with rationale. |
| `approved` | Named reviewer or approver accepted the criterion within recorded limits. | No, within those limits. |
| `request-changes` | Revision is required. | Yes, until changes are completed and accepted. |
| `blocked` | Missing source, decision, owner, dependency, reviewer, approval, or safe path prevents reliance. | Yes. |
| `needs-spike` | Bounded discovery is required before acceptance. | Yes, except for the spike itself. |
| `not-applicable` | Criterion does not apply and rationale is recorded. | No. |

## Classification model

| Classification | Meaning | Required evidence |
| --- | --- | --- |
| Deterministic | The criterion can be checked by repeatable inspection of required fields, states, sections, object relationships, or changed paths. | Target object or surface, rule, status, evidence, owner for failures. |
| Review-only | Human judgment is required for product fit, evidence sufficiency, risk, governance, readiness, or learning promotion. | Reviewer role, evidence reviewed, decision, rationale, downstream effect, recovery action. |
| Both | Objective completeness can pass while human judgment is still required. | Deterministic evidence plus named review decision. |

## MVP1 product acceptance matrix

All applicable criteria must be `passed`, `approved`, or `not-applicable` with
rationale before the MVP1 AI coworker workspace is accepted as product-ready for
the scoped workflow. Any row with `failed`, `blocked`, `needs-spike`,
`request-changes`, unresolved `review-needed`, or required `not-run` status
blocks acceptance for the affected scope.

| AC ID | Area | Trace | Acceptance criterion | Classification | Validation evidence | Blocks acceptance when |
| --- | --- | --- | --- | --- | --- | --- |
| MVP1-AC-001 | Product/tooling boundary | SYN-PRD-009, SYN-PRD-010; CAP-001, CAP-002 | Given any MVP1 workspace surface, contract, handoff, or artifact, when it describes product behavior, then Synapse is presented as the product workspace and current CLI, Cursor rules, runtime memos, generated task cards, workflow YAML, and orchestration framework internals are treated only as prototype scaffolding or internal evidence. | Both | Product boundary review plus future-scope guard against customer-facing prototype mechanics. | Prototype tooling is required as a customer concept or treated as the product contract. |
| MVP1-AC-002 | Destination definition | SYN-PRD-009; CAP-001 | Given an operator creates a workspace, when destination setup is evaluated, then workspace name, operator, destination/outcome, initiative summary, scope, non-goals, success criteria, assumptions, open decisions, and handoff audience are present or explicitly blocked with owner. | Deterministic | Workspace or setup checklist showing required destination fields and owner. | Destination, scope, non-goals, success criteria, accountable operator, or handoff audience is missing or ambiguous. |
| MVP1-AC-003 | Launch readiness gate | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given destination setup is complete enough to review, when G0 launch readiness is decided, then the operator records launch, revise setup, or block with evidence, rationale, limitations, downstream effect, and recovery owner. | Review-only | G0 review/approval record. | A workflow run starts without an explicit human launch decision or blocked setup lacks owner and recovery path. |
| MVP1-AC-004 | Approved workflow selection | SYN-PRD-009, SYN-PRD-010; CAP-001 | Given the workspace offers workflow selection, when the operator selects a workflow, then only the approved product concept-to-implementation workflow is selectable for MVP1 and its purpose, version, stages, required inputs, roles, gates, expected outputs, knowledge requirements, completion criteria, and known limits are visible. | Deterministic | Workflow selection surface or `WorkflowTemplate` field check. | Multiple unapproved workflows are presented as MVP1-ready, or required template details are missing. |
| MVP1-AC-005 | Scope and non-goals gate | SYN-PRD-009, SYN-PRD-010; CAP-001 | Given the approved workflow is selected, when G1 scope and non-goals are reviewed, then the operator confirms the run fits the MVP1 boundary or records scope narrowing, workflow mismatch, escalation, or blocked launch with owner. | Review-only | G1 decision record with scope/non-goal rationale. | The run drifts into deferred capabilities without review, limitation, or recovery. |
| MVP1-AC-006 | Knowledge attachment completeness | SYN-PRD-001, SYN-PRD-009; CAP-003 | Given knowledge is attached to the workspace or task, when the context is inspected, then each source or extract shows stable reference, source posture, evidence use, confidence, freshness, owner/reviewer role, applicability, limitations, and exclusions or gaps. | Deterministic | Knowledge attachment checklist or `KnowledgeContext` field check. | A source grounds coworker work without posture, provenance, applicability, confidence/freshness, or limitations. |
| MVP1-AC-007 | Knowledge approval and gap handling | SYN-PRD-001, SYN-PRD-005, SYN-PRD-009; CAP-003, CAP-005 | Given sources are incomplete, stale, low-confidence, operational-only, rejected, or unavailable, when evidence sufficiency is evaluated, then G2 records whether work may proceed with caveat, requires source-backed revision, stays assumption/open question, narrows scope, or blocks launch/task acceptance. | Both | Knowledge state plus G2 evidence sufficiency review. | Low-confidence, stale-risk, rejected, raw, research, operational-only, or unavailable material is treated as accepted product truth without review. |
| MVP1-AC-008 | Coworker roster and role boundaries | SYN-PRD-002, SYN-PRD-009; CAP-004 | Given the operator staffs the run, when coworker selection is inspected, then each AI coworker has role summary, responsibilities, assigned stages/tasks, allowed context, expected outputs, prohibited actions, dependencies, review/escalation triggers, completion signal, and handoff audience. | Deterministic | Coworker roster or `AgentCoworker` field check. | A coworker can be dispatched with unclear role, source context, output expectation, review gate, prohibited actions, or handoff audience. |
| MVP1-AC-009 | Human reviewer and approver accountability | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given a review, approval, recovery, handoff, or learning-promotion action is required, when accountability is inspected, then a human operator, reviewer, approver, or recovery owner role is named and unavailable reviewers are delegated, escalated, or blocked. | Both | Human operator/reviewer roster plus gate ownership review. | Review-only approval is implied without a named accountable human role. |
| MVP1-AC-010 | Work packet generation | SYN-PRD-004, SYN-PRD-009; CAP-002 | Given launch readiness is approved, when Synapse generates or displays work packets, then each packet includes objective, assignee, approved sources, deliverables, dependencies, prohibited/deferred topics, validation expectations, approval/review triggers, handoff requirements, and completion signal. | Deterministic | Task/work packet field-completeness check. | Any packet lacks fields needed for bounded assignment or downstream review. |
| MVP1-AC-011 | Dispatch control | SYN-PRD-004, SYN-PRD-005, SYN-PRD-009; CAP-002, CAP-005 | Given work packets exist, when dispatch is attempted, then no AI coworker task starts until the operator can review task readiness and choose dispatch, edit, hold, cancel, or block with rationale. | Both | Dispatch decision record and task state transition evidence. | Tasks start without operator-visible objective, source context, deliverables, dependencies, and review expectations. |
| MVP1-AC-012 | Dependency and partial dispatch safety | SYN-PRD-004, SYN-PRD-009; CAP-002 | Given some tasks are blocked or dependent, when dispatch proceeds, then only independent ready tasks can be dispatched and blocked tasks preserve dependency, impact, owner, recovery action, and downstream limits. | Both | Dependency map/task status plus recovery record. | Partial launch proceeds without dependency safety, owner, or limitation. |
| MVP1-AC-013 | Monitoring status visibility | SYN-PRD-004, SYN-PRD-009; CAP-006 | Given a workflow run is active, when the operator opens monitoring, then stage, task, coworker, blocker, review, approval, output, and handoff readiness states are visible in product language using allowed state values or plain-language equivalents. | Deterministic | Run monitor state checklist against `Workspace`, `WorkflowRun`, `Task`, `AgentCoworker`, `Approval`, `Review`, `OutputArtifact`, and `Handoff` states. | Operator cannot tell what is done, active, blocked, waiting for review/approval, partial, cancelled, or ready for handoff. |
| MVP1-AC-014 | Monitor intervention actions | SYN-PRD-004, SYN-PRD-005, SYN-PRD-009; CAP-005, CAP-006 | Given a run is active, blocked, partial, failed, or waiting, when intervention is required, then the operator can provide context, pause/resume, revise task, reassign/delegate, request revision, resolve blocker, escalate, cancel, or continue with accepted limitation. | Both | Monitor action and recovery records. | Blocked, unsafe, or partial work has no visible next action or accountable owner. |
| MVP1-AC-015 | Output evidence display | SYN-PRD-001, SYN-PRD-004, SYN-PRD-009; CAP-002, CAP-003 | Given an AI coworker submits an output, when it enters review, then output summary, producing task/coworker, source references, evidence split into source-backed/inferred/assumed/open claims, validation status, assumptions, risks, open questions, confidence limits, and handoff eligibility are visible. | Both | Output review checklist plus evidence sufficiency review. | Material claims are accepted without source/evidence posture or uncertainty labels. |
| MVP1-AC-016 | Review and approval decisions | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given an output, risk, validation exception, product-fit issue, or handoff requires human judgment, when reviewed, then the reviewer can approve, reject, request changes, defer, escalate, or mark not applicable with rationale, evidence reviewed, downstream effect, limits, and recovery action. | Review-only | Review/approval record for G2-G5 or equivalent gate. | Downstream reliance proceeds after missing, rejected, deferred, or request-changes review without recovery. |
| MVP1-AC-017 | Product fit gate | SYN-PRD-009, SYN-PRD-010; CAP-001, CAP-005 | Given outputs may enter the handoff package, when G3 product fit is reviewed, then accepted outputs express user value, product behavior, requirements, non-goals, and implementation implications for Synapse rather than internal tooling mechanics. | Review-only | G3 product-fit review decision. | Handoff outputs describe prototype internals as the customer product or omit user/product value. |
| MVP1-AC-018 | Risk and governance gate | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given risks, sensitive data concerns, access/tenancy/compliance questions, source limitations, approval policy issues, or governance impacts are present, when G4 risk and governance is reviewed, then each item is classified known, assumed, open, not applicable, blocked, accepted with limitation, or needs-spike with owner. | Review-only | G4 risk/governance record. | Governance or risk concerns are unresolved but treated as accepted or implementation-ready. |
| MVP1-AC-019 | Output acceptance state | SYN-PRD-004, SYN-PRD-005, SYN-PRD-009; CAP-002, CAP-005 | Given an output is submitted, when acceptance is evaluated, then it cannot move to `accepted` or `handed-off` until required validation and reviews are passed, approved, or not applicable with rationale. | Deterministic | `OutputArtifact` state transition check and linked validation/review records. | Submitted or draft output appears in handoff as accepted without resolved gates. |
| MVP1-AC-020 | Handoff package completeness | SYN-PRD-004, SYN-PRD-005, SYN-PRD-009; CAP-001, CAP-002 | Given accepted outputs exist, when the handoff is assembled, then it includes destination and workflow summary, accepted outputs, decisions, validation summary, assumptions/open questions, risks, blockers, dependencies, source/evidence summary, review/approval decisions, learning signals, follow-up owners, and recommended next steps. | Deterministic | Handoff field-completeness checklist. | The handoff lacks accepted outputs, limitations, evidence, review/approval state, owners, blockers, or next steps. |
| MVP1-AC-021 | Handoff readiness and consumer acceptance | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given a handoff is ready for downstream use, when G5 handoff readiness is decided, then the package is marked ready to consume, partial/conditional, blocked, accepted, or superseded with receiving owner, limitations, open items, and recovery owners. | Both | G5 handoff readiness record and consumer view/acceptance evidence. | Downstream consumers cannot distinguish actionable, conditional, blocked, or prohibited work. |
| MVP1-AC-022 | Learning signal creation | SYN-PRD-006, SYN-PRD-009; CAP-007 | Given outputs, reviews, blockers, revisions, source gaps, validation gaps, role ambiguity, recovery patterns, or handoff defects produce learning, when captured, then each learning signal records summary, source runtime/reference, evidence class, confidence, freshness, proposed promotion target, owner role, reviewer role, promotion state, rationale, and limitations. | Deterministic | Learning capture field-completeness check. | Learning is unowned, untraceable, lacks target/reviewer, or cannot be reviewed later. |
| MVP1-AC-023 | Learning promotion governance | SYN-PRD-006, SYN-PRD-009; CAP-005, CAP-007 | Given a learning signal could change future knowledge, workflow template, coworker persona, validator, backlog gate, standard, or canonical artifact, when G6 learning promotion is evaluated, then the human reviewer decides promote, investigate, defer, reject, or operational-only with rationale and limits. | Review-only | G6 learning promotion record. | Reusable behavior changes automatically or from runtime evidence without review. |
| MVP1-AC-024 | Audit event coverage | SYN-PRD-004, SYN-PRD-005, SYN-PRD-006, SYN-PRD-009; CAP-005, CAP-006, CAP-007 | Given material workspace actions occur, when auditability is inspected, then destination setup, workflow selection, knowledge attachment, task dispatch, state transitions, output submission, validation, review, approval, handoff, recovery, and learning disposition are reconstructable through audit events or equivalent audit trail entries with correlation to affected objects. | Deterministic | Audit trail or activity summary checklist. | Material decisions or transitions cannot be traced to actor, target, state, evidence, rationale, and correlation. |
| MVP1-AC-025 | Governance and source immutability | SYN-PRD-001, SYN-PRD-009; CAP-003, CAP-005 | Given MVP1 product criteria or related artifacts are changed, when repository changes are inspected, then `raw/` and `research/` remain unmodified and raw/research content is used only through reviewed promotion into `docs/` artifacts or recorded as operational/reference context. | Deterministic | Repository diff or changed-path summary. | `raw/` or `research/` files are edited, or unpromoted source material is treated as durable product truth. |
| MVP1-AC-026 | Non-goals and deferred capabilities | SYN-PRD-009, SYN-PRD-010; CAP-001, CAP-003, CAP-004, CAP-005, CAP-006, CAP-007, CAP-008, CAP-009, CAP-010 | Given MVP1 scope is reviewed, when product claims are inspected, then visual workflow designer, workflow marketplace, arbitrary workflow authoring, broad knowledge registry, SME persona registry, production workflow-run database, event bus, product API, telemetry backend, approval automation, provider/runtime choice, multi-tenant administration, billing, compliance implementation, external source connectors, and legacy bridge adapters are marked deferred, future, or open. | Both | Future-scope guard plus product/architecture review. | MVP1 acceptance depends on an unsupported deferred capability or commits implementation technology without accepted decision. |
| MVP1-AC-027 | Runtime contract alignment | SYN-PRD-004, SYN-PRD-005, SYN-PRD-006, SYN-PRD-009; CAP-002, CAP-005, CAP-006, CAP-007 | Given workspace behavior is specified or reviewed, when compared to runtime contracts, then the accepted product objects use stable identifiers, allowed states, required relationships, validation rules, governance rules, and handoff/learning/audit correlations defined for `Workspace`, `WorkflowTemplate`, `WorkflowRun`, `HumanOperator`, `AgentCoworker`, `KnowledgeContext`, `Task`, `Approval`, `Review`, `OutputArtifact`, `LearningSignal`, `AuditEvent`, and `Handoff`. | Both | Contract-field and state alignment checklist plus reviewer decision for review-only gaps. | Product acceptance relies on object states, transitions, or relationships that are missing, contradictory, or unreviewed. |

## End-to-end journey acceptance

An MVP1 run is accepted only when the following journey-level criteria are met:

1. The operator can start from an initiative and create a structured workspace
   without touching prototype orchestration internals.
2. The operator can confirm the approved product concept-to-implementation
   workflow and understand its stages, gates, roles, outputs, and limits.
3. The operator can attach approved knowledge, mark source gaps, and see which
   claims remain assumptions or open questions.
4. The operator can review coworker roles and dispatch only bounded work packets
   with objective, sources, deliverables, dependencies, review expectations, and
   completion signals.
5. The operator can monitor stage, task, coworker, blocker, approval, review,
   output, handoff, and learning status in product language.
6. The operator or named reviewer can approve, reject, request changes, defer,
   escalate, or mark gates not applicable with rationale and downstream effect.
7. The operator can produce a handoff package that distinguishes accepted output
   from conditional output, blockers, risks, assumptions, open decisions, and
   follow-up owners.
8. The operator can capture learning candidates without automatically changing
   reusable product behavior.

## Required review gates

| Gate | Acceptance decision | Required record | Related criteria |
| --- | --- | --- | --- |
| G0: Launch readiness | Launch, revise setup, or block. | Destination, operator, evidence, rationale, limitations, downstream effect, recovery owner. | MVP1-AC-002, MVP1-AC-003 |
| G1: Scope and non-goals | Approve scope, narrow scope, escalate, or block. | Selected workflow, scope/non-goals, deferred capabilities, reviewer rationale. | MVP1-AC-004, MVP1-AC-005, MVP1-AC-026 |
| G2: Evidence sufficiency | Accept, request source-backed revision, mark assumption/open question, narrow, or block. | Sources reviewed, evidence class, confidence/freshness, limitations, affected outputs. | MVP1-AC-006, MVP1-AC-007, MVP1-AC-015 |
| G3: Product fit | Accept, revise, or block product-facing handoff. | Product value, user behavior, non-goals, tooling-boundary rationale. | MVP1-AC-001, MVP1-AC-017 |
| G4: Risk and governance | Accept, mitigate, defer, escalate, needs-spike, or block. | Risk/governance classification, owner, recovery or mitigation. | MVP1-AC-018, MVP1-AC-025 |
| G5: Handoff readiness | Ready to consume, partial/conditional, blocked, accepted, or superseded. | Accepted outputs, limitations, open items, receiving owner, follow-up owners. | MVP1-AC-020, MVP1-AC-021 |
| G6: Learning promotion | Promote, investigate, defer, reject, or keep operational-only. | Learning target, evidence, owner, reviewer, rationale, promotion limits. | MVP1-AC-022, MVP1-AC-023 |

## Readiness blocker summary

Any of the following blocks MVP1 product acceptance for the affected scope:

- Acceptance criteria are not testable or reviewable.
- Required SYN-PRD or CAP trace is missing for a product acceptance claim.
- Destination, operator, scope, non-goals, success criteria, workflow, knowledge
  context, coworker roles, reviewers, or handoff audience are missing.
- The run starts or a task dispatches before human launch/dispatch approval.
- A coworker task lacks objective, allowed context, deliverables, dependencies,
  review gates, prohibited actions, handoff requirements, or completion signal.
- Source-backed, inferred, assumed, and open claims are conflated.
- Low-confidence, stale-risk, rejected, operational-only, raw, or research
  material grounds accepted product truth without review.
- Review-only gates lack reviewer role, evidence reviewed, decision, rationale,
  downstream effect, or recovery action.
- Outputs move to accepted or handed-off state before required validation and
  review gates are resolved.
- Blocked, partial, failed, rejected, request-changes, or escalated work lacks
  owner, impact, preserved output, recovery action, and follow-up validation or
  review.
- Handoff packages omit accepted outputs, limitations, risks, blockers,
  assumptions, open decisions, review/approval status, or owners.
- Learning changes reusable product behavior without human promotion review.
- Material actions cannot be reconstructed through audit trail or equivalent
  correlated records.
- `raw/` or `research/` files are modified, or raw/research content is promoted
  without review into product truth.
- MVP1 acceptance depends on deferred tooling, UI, runtime, event, API,
  telemetry, provider, tenancy, compliance, external connector, marketplace,
  broad registry, or legacy bridge capabilities.

## Non-goals and tooling boundary

MVP1 acceptance does not require and must not imply acceptance of:

- a visual drag-and-drop workflow designer;
- arbitrary workflow creation or a workflow marketplace;
- a broad knowledge ingestion pipeline, knowledge registry, or source connector
  platform;
- a reusable SME/persona registry beyond role-scoped coworker definitions for
  the approved workflow;
- production workflow runtime infrastructure, workflow-run database, scheduler,
  event bus, telemetry backend, schema registry, product API, or approval
  automation;
- model/provider/runtime selection, prompt-service design, IDE integration, or
  tool integration as the customer-facing contract;
- multi-tenant administration, billing, deployment model, access-control,
  sensitive-data handling, retention, deletion, or compliance implementation;
- external legacy-system adapters or domain-specific migration automation; or
- exposing Cursor, repository runtime memos, generated task cards, workflow YAML,
  slash commands, local worktrees, or orchestration framework internals as
  required customer concepts.

Prototype tooling may remain useful as internal evidence, but accepted product
behavior must be stated through Synapse workspace objects, human decisions,
governed knowledge, review gates, handoff records, learning signals, and audit
concepts.

## Acceptance evidence template

Use this table when recording acceptance for a workspace run, artifact, gate, or
handoff.

| Field | Requirement |
| --- | --- |
| `acceptance_target` | Workspace, workflow run, task, output, review gate, handoff, learning signal, or artifact. |
| `criteria_ids` | Applicable `MVP1-AC-###` rows. |
| `trace_ids` | Applicable `SYN-PRD-###` and `CAP-###` IDs. |
| `status` | One of the accepted status values in this document. |
| `classification` | Deterministic, review-only, or both. |
| `evidence` | Field check, state transition, review record, handoff package, audit entry, or limitation. |
| `reviewer_or_owner` | Accountable operator, reviewer, approver, recovery owner, or learning owner. |
| `rationale` | Why the decision is acceptable, limited, blocked, or not applicable. |
| `downstream_effect` | What can proceed, what is conditional, and what must wait. |
| `follow_up` | Recovery action, owner, due condition, spike, review, or promotion path. |

## Open acceptance decisions

| ID | Decision needed | Current MVP1 handling |
| --- | --- | --- |
| OQ-PAC-001 | Which customer-facing surface should first implement the workspace: local, web, hybrid, guided document workspace, or embedded console? | Keep acceptance technology-neutral and validate product semantics, not UI stack. |
| OQ-PAC-002 | Which reviewer roles are mandatory for each gate in the first productionized workflow? | Use role-based reviewer/approver accountability until named roles are accepted. |
| OQ-PAC-003 | What exact evidence display is sufficient for customer-facing source-backed outputs? | Require source references, evidence class, confidence/freshness, assumptions, open questions, and reviewer rationale. |
| OQ-PAC-004 | Which fields must become machine-readable for automated validation? | Keep Markdown-first/product-contract acceptance and add schemas only after validator needs are accepted. |
| OQ-PAC-005 | What handoff artifact format should implementation leads receive first? | Validate handoff content, readiness, limitations, and consumer acceptance; defer file/tool format. |
| OQ-PAC-006 | What audit detail is visible to operators, reviewers, and implementation leads? | Require logical auditability and correlation; defer access, redaction, retention, and compliance rules. |
| OQ-PAC-007 | Which learning targets can be promoted in MVP1 without implementing MVP2/MVP3 registries? | Capture learning signals and require human promotion review; defer registry implementation. |
