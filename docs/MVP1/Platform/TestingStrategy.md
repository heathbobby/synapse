# MVP1 Platform Testing Strategy

- **Status**: draft MVP1 quality strategy
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-05-quality-testing`
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

This document defines the implementation-agnostic quality strategy for MVP1.
MVP1 is a CLI-assisted, repository-first concept-to-implementation pipeline over
the existing orchestration framework. Quality is therefore measured through
canonical documentation, workflow/task-packet completeness, deterministic
validators, review-only gates, integration contract checks, runtime reference
discipline, and explicit recovery behavior.

This strategy does not define a hosted test platform, runtime workflow service,
event bus, schema registry, telemetry backend, approval automation, visual UI,
provider integration, tenancy model, or compliance implementation.

## Source register

| Source | How this strategy uses it |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp1-iteration-05-quality-testing.md` | Iteration goal, quality scope, and completion criteria. |
| `docs/MVP1/Platform/Overview.md` | MVP1 operating boundary, in-scope validation, source immutability, and downstream readiness criteria. |
| `docs/MVP1/Platform/Infrastructure.md` | Infrastructure principles, validation scope, canonical paths, state/event posture, concurrency, and governance posture. |
| `docs/MVP1/Platform/Integrations.md` | Integration participants, validation/result flow, human review gates, telemetry/log reference flow, and recovery contracts. |
| `docs/MVP1/Platform/Features/WorkflowDesigner/Overview.md` | Workflow/task-packet feature expectations, acceptance gates, risks, and future-scope exclusions. |
| `docs/MVP1/Platform/Features/WorkflowDesigner/Workflows/CreateWorkflow.md` | Launch inputs, validation points, human review gates, observability references, handoff outputs, and recovery behavior. |
| `docs/work_items/TECHNICAL_REFINEMENT_GATES.md` | Product, technical, validation, observability, security, dependency, and agent-output readiness gate model. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Agent evidence discipline, required task-packet inputs, validation/handoff expectations, and completion signals. |
| `docs/standards/EVENT_CONTRACT_STANDARDS.md` | Logical event, validation, approval, telemetry, retry, dead-letter, correlation, and review-gate standards. |

## Quality stance

1. **Canonical docs are the quality contract**: implementation readiness is
   judged against promoted `docs/` artifacts, not raw notes, research files, or
   runtime-only logs.
2. **Deterministic checks are narrow and explicit**: validators should check
   presence, format, required sections, stable trace markers, prohibited edits,
   completion signals, and contract-field completeness where rules are objective.
3. **Human review remains accountable for judgment**: product fit, evidence
   sufficiency, architecture fit, security/privacy impact, risk acceptance,
   governance impact, and open-decision impact are review-only unless later
   standards create deterministic rules.
4. **Quality gates precede downstream reliance**: no workflow, task packet,
   deliverable, integration contract, or handoff should be treated as
   implementation-ready until deterministic checks pass or are marked
   not-applicable with rationale, and review-only gates have named decisions.
5. **Technology-neutral contracts protect MVP1 scope**: tests must not imply
   runtime, storage, API, event transport, telemetry backend, provider, visual
   UI, tenancy, compliance, or legacy-adapter decisions that remain open.
6. **Recovery is part of quality**: failed, blocked, partial, token-limited, or
   conflicted work must preserve useful output, name impact, assign an owner,
   and state validation or review needed before downstream reliance resumes.

## Gate status values

Use these status values in validation summaries, handoffs, task packets,
readiness tables, and review records.

| Status | Meaning |
| --- | --- |
| `not-run` | The check or review has not been performed. |
| `passed` | The deterministic criterion passed with evidence. |
| `failed` | The deterministic criterion failed and requires recovery. |
| `review-needed` | Human review is required before acceptance. |
| `approved` | A named reviewer accepted a review-only criterion with rationale. |
| `request-changes` | A named reviewer requires revision before downstream reliance. |
| `blocked` | A missing source, decision, owner, dependency, or approval prevents readiness. |
| `needs-spike` | Bounded discovery is required before implementation can proceed. |
| `not-applicable` | The criterion does not apply and rationale is recorded. |

## Product and readiness gates

MVP1 readiness requires all applicable gates below to be `passed`, `approved`,
or `not-applicable` with rationale. Any `failed`, `blocked`, `needs-spike`,
`request-changes`, or unresolved `review-needed` status blocks implementation
readiness except for the named recovery or spike.

| Gate | Deterministic evidence | Review-only evidence | Blocks readiness when |
| --- | --- | --- | --- |
| Product scope | Deliverable states MVP1 is CLI-assisted, repository-first, Markdown-first, and orchestration-framework scoped. Future visual/runtime/product infrastructure is marked future/open. | Product reviewer confirms user value, persona needs, MVP boundary, and assumptions are coherent. | Scope implies visual UI, hosted runtime, product API, storage, event transport, provider, tenancy, compliance, or legacy implementation without accepted decision. |
| Requirements traceability | PRD/FR, E##, US-E##-###, workflow, phase, iteration, task, gate, or validation IDs appear where applicable. | Product or integrator reviewer confirms trace is meaningful and sufficient for downstream work. | Required trace markers are missing, unstable, contradictory, or tied to unpromoted raw/research claims. |
| Workflow/task-packet readiness | Required fields are present: role/objective, canonical sources, deliverables, prohibited edits, dependencies, acceptance criteria, validation expectations, handoff audience, and completion signal. | Orchestrator, integrator, or reviewer confirms task scope is assignable and bounded. | Required fields, write-target ownership, reviewer role, dependency, or handoff audience is missing or ambiguous. |
| Dependency and concurrency | Shared deliverables have one owner or explicit merge contract; unsafe sequencing is recorded. | Integrator confirms fan-out is safe and downstream consumers understand what can proceed. | Parallel work edits shared files without owner/contract, or E03/E04/E05-style work depends on unstable upstream contracts. |
| Validation and quality | Required deterministic checks have status, evidence, target, run context, and follow-up owner when not passed. | QA/reviewer confirms review-only checks and limitations are labeled. | Validation status is absent, failed without recovery, or overclaims subjective approval. |
| Integration contracts | Logical fields, owners, producers/consumers, correlation, failure/recovery, validation, approval, and telemetry references are documented for affected flows. | Architect/integrator confirms contracts are technology-neutral and sufficient for handoff. | Contract lacks owner, required fields, correlation, recovery behavior, or introduces implementation choices prematurely. |
| Security/privacy/governance | Prohibited edits and role/tool boundaries are recorded; sensitive data, tenancy, compliance, retention, access, and approval policy are classified as known, assumed, open, or not applicable. | Security/privacy or governance reviewer accepts risk treatment or deferral. | Sensitive data, access, compliance, retention, approval policy, or tenancy claims are unresolved but treated as implementation-ready. |
| Reliability and recovery | Failure classes, partial completion, token-budget handling, conflict recovery, validation failure recovery, retryability, and recovery owner are recorded where applicable. | Integrator/reviewer confirms recovery path preserves downstream safety. | Failure behavior is unspecified for blocked, partial, invalid, conflicted, or unprocessable work. |
| Telemetry and log references | Runtime/log/memo/task-card references are correlated to workflow, task, artifact, validation, review, or handoff targets when available. | Reviewer confirms material runtime-only findings were promoted into durable docs or accepted as limitations. | Material trust or reproducibility depends on missing, inaccessible, or operational-only logs without limitation or canonical summary. |
| Agent-output handoff | Output names changed artifacts, evidence, validation performed/not performed, assumptions/open questions, blockers, prohibited-edit confirmation, downstream audience, and standard completion signal. | Integrator or downstream role confirms ready-to-consume, blocked, or partial status. | Completion signal is missing/invalid, handoff omits validation or prohibited-edit status, or downstream safety is unclear. |

## Deterministic validators

Deterministic validators should be small, repeatable, and scoped to objective
MVP1 contracts. They may be implemented as scripts, CLI checks, CI jobs, or
manual command runs later, but this strategy defines behavior without selecting
tooling.

| Validator class | Targets | Objective rule | Evidence to record |
| --- | --- | --- | --- |
| Required files | Canonical deliverables, input packets, work-item docs, standards, handoff packages | Expected paths exist or are explicitly marked blocked/partial. | Target path, existence status, run context, missing paths, owner. |
| Required sections/headings | Platform docs, feature specs, workflow docs, work items, task packets, handoffs | Required headings/tables for the artifact type are present. | Target path, missing section names, status, owner. |
| Required metadata | Workflow definitions, input packets, task cards, validation records, review gates | Required fields are present and non-empty. | Target ID, missing fields, status, owner. |
| Trace markers | Requirements, workflow specs, backlog items, gates, validation records | Applicable PRD/FR, E##, US-E##-###, workflow/phase/iteration, task, gate, and validation IDs follow local conventions. | Marker list, invalid/missing IDs, status, owner. |
| Completion-signal format | Agent handoffs, memos, task completion records | Signal is one of `TASK_COMPLETE`, `TOKEN_BUDGET_LOW`, `BLOCKED`, or `PARTIAL_COMPLETE` and includes required detail. | Signal, target task, status, remaining work or blocker. |
| Source immutability | Repository diff for MVP1 tasks | `raw/` and `research/` files are not modified; prohibited edits are not made. | Diff summary, changed prohibited paths if any, recovery owner. |
| Contract-field completeness | Integration contracts, logical event records, validation results, readiness gates | Required logical fields, owners, statuses, correlation, evidence, limitations, and follow-up owner are present. | Contract/check ID, missing fields, status, owner. |
| Future-scope guard | Platform, feature, workflow, task, and work-item docs | Unsupported implementation claims for runtime, UI, storage, event transport, telemetry backend, provider, tenancy, compliance, or legacy adapters are absent or marked future/open. | Claim location, classification, status, reviewer needed. |

Validator result records should include:

| Field | Requirement |
| --- | --- |
| `validation_result_id` | Stable label such as `{target_id}:{check_class}:{run_context}`. |
| `target_type` / `target_id` | Workflow, iteration, task packet, deliverable, memo, gate, work item, or contract being checked. |
| `check_class` | One of the deterministic validator classes above, or `review-only quality`. |
| `criteria` | Specific objective rule or review expectation. |
| `status` | `not-run`, `passed`, `failed`, `review-needed`, or `not-applicable`. |
| `evidence` | Command output summary, file/section reference, reviewer rationale, or limitation. |
| `run_context` | Date, branch, SHA, command label, reviewer, or runtime reference when available. |
| `follow_up_owner` | Owner for failures, recovery, review, or accepted limitations. |
| `related_decision_question_ids` | Linked blockers, assumptions, open decisions, or recovery questions when applicable. |

## Review-only checks

Review-only checks must never be hidden behind deterministic pass/fail language.
Each check needs a reviewer role, evidence reviewed, decision, rationale,
affected downstream work, and recovery action when not approved.

| Review family | Reviewer role | Quality question |
| --- | --- | --- |
| Product/value | Product owner, product reviewer, or integrator | Does the artifact support the MVP1 user value, personas, workflow outcome, and explicit scope boundary? |
| Evidence sufficiency | Domain reviewer, integrator, or standards owner | Are source-backed, inferred, assumed, and open claims distinguishable where they affect scope, architecture, validation, security, dependencies, or operations? |
| Architecture/technical fit | Architect, tech lead, or integrator | Does the work preserve repository-first, CLI-assisted, Markdown-first, technology-neutral contracts and avoid unsupported stack choices? |
| Integration fit | Architect, integrator, or contract owner | Are logical fields, owners, correlation, validation, approval, telemetry, and recovery semantics sufficient before downstream reliance? |
| Risk acceptance | Gate owner, integrator, or domain reviewer | Are risks, blockers, limitations, and recovery paths acceptable for the downstream use being requested? |
| Security/privacy/governance | Security/privacy reviewer or governance reviewer | Are sensitive data, tenancy, access, retention, compliance, approval policy, and prohibited-edit concerns accepted, deferred, or blocking? |
| Reusable behavior change | Configuration owner, standards owner, or reviewer | Do workflow template, persona, standard, validator, or task-packet changes need attribution and review before promotion? |
| Implementation readiness | Integrator, tech lead, QA lead, or assigned gate owner | Are all deterministic and review-only gates sufficiently resolved for the next implementation or handoff step? |

Lack of a named reviewer blocks review-only approval.

## Integration contract checks

MVP1 integration checks apply to command/document boundaries, not product APIs.
They confirm that workflow configuration, input packets, generated task cards,
agent handoffs, validation results, review gates, telemetry references, and
recovery records preserve enough context for downstream work.

| Check | Required expectation |
| --- | --- |
| Participant ownership | Producer, consumer, reviewer/gate owner, validator owner, and recovery owner are named or the contract remains blocked/conceptual. |
| Identifier stability | Workflow, phase, iteration, task, memo, validation, gate, deliverable, and runtime references are stable enough for Markdown cross-reference. |
| Required logical fields | Each contract includes required inputs, outputs, dependencies, deliverables, validation expectations, status, evidence, and handoff audience. |
| Correlation | Workflow/task/validation/review/handoff/log references can be tied to a common workflow, iteration, task, artifact, or run context when available. |
| Completion and state | Task and handoff status uses accepted states/signals and distinguishes complete, blocked, partial, review-needed, and not-run conditions. |
| Failure and recovery | Missing inputs, invalid packets, failed validation, review rejection, token budget, conflicts, prohibited edits, and open decisions produce owner-assigned recovery. |
| Human-in-loop behavior | Review gates state reviewer role, evidence, decision values, rationale, affected downstream work, and recovery action. |
| Event-standard alignment | Conceptual events and event-like records follow family, ownership, payload, validation, telemetry, retry/dead-letter, idempotency, ordering, versioning, and governance guidance when relevant. |
| Non-commitment | Contracts avoid selecting event transport, API protocol, storage, runtime, telemetry backend, schema registry, provider, tenancy, compliance, or visual implementation. |

## Telemetry and log reference checks

MVP1 telemetry is reference-based. Logs, generated task cards, memos, command
outputs, branch/SHA references, and validation outputs are operational evidence,
not durable product truth unless summarized into canonical docs, decisions, work
items, or handoff packages.

| Reference check | Acceptance expectation |
| --- | --- |
| Runtime reference captured | Material CLI invocation, generated task card, memo, validation run, review note, or command output is referenced by path, label, branch/SHA, or run context when available. |
| Correlation preserved | Reference is tied to workflow/phase/iteration, task packet, deliverable, validation result, review gate, or recovery item. |
| Durability classified | Reference is labeled operational-only, summarized, canonicalized, unavailable, or not applicable. |
| Limitations stated | Missing, inaccessible, partial, or non-durable references are recorded when they affect trust or reproducibility. |
| Material findings promoted | Runtime-only facts needed for implementation are promoted into canonical docs, work items, decisions, or handoff packages before reliance. |
| Process learning captured | Repeated validation gaps, task-packet defects, token-budget issues, blocked approvals, or quality problems are routed to standards, validators, workflow templates, personas, or backlog owners after review. |

## Security, privacy, and governance checks

MVP1 does not define final access control, tenancy, sensitive-data handling,
compliance controls, retention, provider policy, or approval automation. Quality
checks must still surface these concerns before implementation claims proceed.

| Check | Required expectation |
| --- | --- |
| Prohibited edits | Task packets, handoffs, and validation confirm `raw/` and `research/` are not edited and prohibited paths are respected. |
| Role and tool boundaries | Assigned role, allowed deliverables, prohibited decisions, tool boundaries, and handoff audience are explicit. |
| Sensitive data classification | Sensitive data, tenancy, retention, compliance, deletion, access-control, and provider concerns are marked known, assumed, open, not applicable, blocked, or needs-spike. |
| Approval accountability | Policy-sensitive, high-risk, release, SME-validation, reusable behavior, validation exception, or compliance-sensitive steps name reviewer role and decision expectations. |
| Reusable asset governance | Workflow templates, persona definitions, standards, validators, and knowledge-promotion changes that affect future agents include attribution and review before promotion. |
| Runtime evidence handling | Operational logs and memos are not treated as durable truth without review and canonical summary when material. |
| Implementation claim guard | Unresolved governance questions block implementation-specific claims rather than being silently assumed. |

## Reliability and recovery checks

Reliability for CLI-assisted MVP1 means preserving state, impact, ownership, and
safe recovery when work cannot complete cleanly. It does not imply a production
retry engine, scheduler, dead-letter store, rollback mechanism, or observability
platform.

| Scenario | Required quality behavior |
| --- | --- |
| Missing source or input packet | Mark workflow/task `blocked`; name missing source, impact, and owner. |
| Invalid or incomplete task packet | Keep packet `draft` or `blocked`; correct required fields before assignment. |
| Shared-file conflict | Assign one owner or merge contract; sequence or split work before downstream reliance. |
| Failed deterministic validation | Record target, criterion, evidence, impact, recovery owner, and validation needed after correction. |
| Review rejection or request changes | Record decision, rationale, affected downstream work, recovery action, and revised owner. |
| Token budget or partial completion | Use `TOKEN_BUDGET_LOW` or `PARTIAL_COMPLETE`; preserve completed artifacts, list remaining paths, and recommend recovery split. |
| Prohibited edit violation | Stop downstream reliance, identify affected paths, assign recovery owner, and require review before acceptance. |
| Missing runtime/log evidence | Record limitation; summarize available material facts into durable docs if needed. |
| Open architecture/governance decision | Mark `blocked` or `needs-spike`; avoid stack/runtime/policy commitments. |
| Future event or integration failure concept | Document retryability, failure class, recovery owner, idempotency/ordering assumptions, and dead-letter-equivalent recovery before implementation. |

Recovery records should include trigger, affected targets, current state,
preserved output, downstream impact, owner, recovery action, and validation or
review required before reliance resumes.

## Source immutability checks

Raw and research materials are immutable source inputs for MVP1. They may inform
canonical docs only through reviewed promotion into `docs/` artifacts.

| Checkpoint | Required behavior |
| --- | --- |
| Pre-dispatch | Task packet states `raw/` and `research/` are prohibited edit targets unless a future canonical rule grants explicit authority. |
| During execution | Agents work only on allowed deliverables and avoid direct raw/research mutation. |
| Validation | Repository diff or equivalent change summary confirms no `raw/` or `research/` paths changed. |
| Handoff | Agent or integrator confirms prohibited files/directories were not edited, or records violation and recovery owner. |
| Readiness | Any raw/research modification by MVP1 quality, feature, platform, or work-item tasks blocks readiness until reviewed and remediated. |

## What blocks implementation readiness

Implementation readiness is blocked when any applicable item below is true:

- Required canonical source, input packet, deliverable, task packet, reviewer,
  owner, dependency, or handoff audience is missing.
- Required deterministic validation is `not-run`, `failed`, or lacks evidence,
  and no accepted limitation or recovery path exists.
- Review-only criteria remain `review-needed`, lack a named reviewer, or have
  `request-changes` without recovery completion.
- Acceptance criteria are not testable or reviewable.
- Workflow/task-packet required fields are absent or ambiguous.
- Shared write targets lack one owner or merge contract.
- PRD/FR, E##, US-E##-###, workflow/phase/iteration, task, gate, validation, or
  runtime references are missing where needed for traceability.
- Source-backed, inferred, assumed, and open claims are conflated in areas that
  affect scope, architecture, validation, security/privacy, dependencies, or
  operations.
- Runtime/log-only evidence is required for downstream work but is unavailable,
  non-durable, or not summarized into canonical docs.
- `raw/` or `research/` files are modified without explicit future authority.
- Security, privacy, tenancy, access, compliance, retention, approval policy, or
  provider concerns are unresolved but treated as implementation-ready.
- Product/runtime/UI/storage/event/API/telemetry/provider/legacy implementation
  choices are asserted without accepted decisions.
- Integration or event-like contracts lack ownership, logical fields,
  correlation, validation, approval, telemetry, failure, or recovery semantics.
- Agent handoff omits changed artifacts, validation performed/not performed,
  prohibited-edit confirmation, assumptions/open questions, blockers, downstream
  safety, or a valid completion signal.

## Readiness record template

Use this table in handoffs or work items when deciding whether an artifact,
workflow, task packet, contract, or story is ready for implementation.

| Gate | Status | Evidence / rationale | Owner | Follow-up |
| --- | --- | --- | --- | --- |
| Product scope and value |  |  |  |  |
| Requirements and traceability |  |  |  |  |
| Workflow/task-packet readiness |  |  |  |  |
| Dependency and concurrency |  |  |  |  |
| Deterministic validation |  |  |  |  |
| Review-only quality |  |  |  |  |
| Integration contracts |  |  |  |  |
| Telemetry/log references |  |  |  |  |
| Security/privacy/governance |  |  |  |  |
| Reliability/recovery |  |  |  |  |
| Source immutability |  |  |  |  |
| Agent-output handoff |  |  |  |  |

## Assumptions

- Markdown-first structured sections and tables are sufficient for MVP1 quality
  gates until validator work proves that machine-readable schemas are needed.
- Human reviewers remain accountable for subjective quality, risk, governance,
  architecture fit, and implementation-readiness decisions.
- Runtime task cards, memos, logs, command outputs, and branch/SHA references are
  operational evidence; material conclusions must be summarized into canonical
  docs before downstream implementation relies on them.
- The orchestration framework remains the first MVP1 domain and validation
  target.

## Open decisions

| ID | Decision needed | Current MVP1 handling |
| --- | --- | --- |
| OQ-TEST-001 | Which fields require machine-readable extraction for deterministic validators? | Keep Markdown-first contracts and add schemas only after a bounded validator spike proves the need. |
| OQ-TEST-002 | Who is the named accountable approver for each readiness gate family? | Use role-based reviewer ownership until named individuals or teams are accepted. |
| OQ-TEST-003 | Which validator checks should run in CLI, CI, task generation, or integrator review? | Define check behavior here; defer tooling placement until implementation planning. |
| OQ-TEST-004 | What runtime/log references must be retained after orchestration runs? | Summarize material findings into canonical docs or handoff packages; leave retention policy open. |
| OQ-TEST-005 | What event transport, schema registry, telemetry backend, approval policy, access-control, tenancy, compliance, and provider controls apply to future runtime work? | Treat as future/open and block implementation-specific claims until accepted decisions exist. |
