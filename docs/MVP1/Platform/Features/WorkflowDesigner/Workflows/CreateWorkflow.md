# Create Workflow

- **Status**: draft MVP1 workflow specification
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-04-feature-specifications`
- **Feature area**: WorkflowDesigner
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

Create Workflow describes the MVP1 path for turning an approved Synapse
concept-to-implementation intent into a launch-ready, CLI-assisted workflow
iteration. MVP1 creation is Markdown-first and repository-first: operators work
with canonical docs, orchestration configuration, an iteration input packet,
generated task cards or equivalent role packets, runtime memos, validation
summaries, and human review gates.

This workflow does not define a visual workflow canvas, hosted runtime,
workflow-run database, event bus, telemetry backend, product API, approval
automation, or provider-specific agent runtime.

## Source register

| Source | Use in this workflow |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp1-iteration-04-feature-specifications.md` | Iteration goal, tech-writer source references, and completion criteria for workflow docs. |
| `docs/MVP1/Platform/Features/WorkflowDesigner/Overview.md` | Feature scope, MVP1 capabilities, acceptance expectations, risks, and future visual/runtime exclusions. |
| `docs/MVP1/Platform/Integrations.md` | CLI command boundaries, integration participants, validation, human review, telemetry, recovery, and logical future event families. |
| `docs/MVP1/Platform/Infrastructure.md` | Repository-first infrastructure, canonical paths, task-packet fields, validation scope, concurrency rules, and deferred infrastructure. |
| `docs/MVP1/Platform/DataModel.md` | Logical records, identifiers, lifecycle states, relationships, data quality rules, and runtime-reference posture. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Required task-packet inputs, evidence discipline, completion signals, validation, handoff, and governance rules. |
| `docs/standards/EVENT_CONTRACT_STANDARDS.md` | Conceptual event families, ownership, correlation, validation, telemetry, approval, retry, and recovery standards for future implementation. |

## Scope

### In scope for MVP1

- Authoring or confirming a workflow creation contract for the
  orchestration-framework domain.
- Using workflow configuration, canonical docs, and an iteration input packet to
  bound CLI-assisted task generation.
- Creating or updating task cards or equivalent role packets with required
  fields before assignment.
- Recording deterministic validation, review-only gates, runtime references,
  blockers, and handoff state.
- Preserving future visual/runtime transition semantics without implementing
  those systems.

### Out of scope for MVP1

- Visual workflow designer UI, graph serialization, drag-and-drop modeling, or
  template publication UI.
- Hosted workflow execution runtime, scheduler, retry engine, pause/resume
  service, workflow-run persistence, or product API.
- Concrete event transport, schema registry, replay, dead-letter, telemetry,
  trace, metrics, dashboard, or alerting implementation.
- Automated approval queues, policy engine, durable approval ledger, tenancy,
  compliance, sensitive-data handling, retention, access control, provider
  runtime, or legacy adapters.

## Actors and ownership

| Actor | Owns in this workflow | Must produce or confirm |
| --- | --- | --- |
| Orchestrator / operator | Workflow start intent, source packet selection, task generation boundary, recovery routing | Scoped command intent, workflow/phase/iteration IDs, launch readiness, generated task-card references, blockers. |
| Configuration owner | Commit-able workflow and persona configuration | Workflow identity, role bindings, reusable config changes, review for behavior-affecting updates. |
| Specialist role agent | Assigned deliverables and handoff signal | Updated artifacts, validation performed/not performed, assumptions/open questions, completion signal. |
| Integrator | Shared-artifact convergence and downstream readiness | Conflict resolution, accepted limitations, ready-to-consume status, material runtime-context promotion. |
| Validator owner | Deterministic validation and result summaries | Required-file, section, trace-marker, ID-format, source-immutability, and completion-signal checks. |
| Reviewer / gate owner | Review-only quality and approval decisions | Decision, rationale, evidence reviewed, affected downstream work, recovery action. |

## Preconditions and launch inputs

Before a workflow is treated as launch-ready, the operator confirms:

| Input | Required MVP1 expectation |
| --- | --- |
| Workflow identity | `workflow_id`, `phase_id`, and `iteration_id` are stable and match canonical references. |
| Domain scope | Scope is orchestration-framework / CLI-assisted concept-to-implementation. |
| Source packet | Iteration input packet exists and names goal, role sources, and completion criteria. |
| Canonical sources | Required `docs/` sources are available; `raw/` and `research/` are not direct write targets. |
| Role bindings | Each role has objective, boundaries, deliverables, reviewers, and handoff audience. |
| Deliverables | Exact paths or artifact classes are listed with write-target ownership. |
| Dependencies | Upstream decisions, blockers, gates, and unsafe parallelism are recorded. |
| Validation expectations | Deterministic checks and review-only checks are named. |
| Completion criteria | Expected completion state and handoff signal are explicit. |

If any required input is missing, the workflow remains `draft` or `blocked`
until the missing source, owner, write target, dependency, or review authority is
resolved.

## Happy path

1. **Frame creation intent**
   - Operator states the workflow creation request in CLI/document terms:
     workflow ID, phase, iteration, domain, source packet, and expected outputs.
   - Creation intent is correlated to a runtime/log reference when available.

2. **Load canonical context**
   - Operator or orchestrator reads workflow configuration, persona/role
     references, standards, and the iteration input packet.
   - Canonical docs under `docs/` are treated as durable truth; runtime files are
     operational references only.

3. **Confirm launch readiness**
   - Required sources, role bindings, deliverables, prohibited edits,
     dependencies, validation expectations, and handoff audiences are checked.
   - Shared write targets either have one owner or an explicit merge contract.

4. **Run CLI-assisted workflow start or task-generation intent**
   - The existing orchestration framework is invoked through the approved
     command boundary for workflow start or task generation.
   - MVP1 documents command intent and required inputs/outputs; it does not
     freeze a product API or final CLI interface.

5. **Generate task cards or equivalent role packets**
   - Each task packet includes role/objective, canonical sources, deliverables,
     prohibited edits, dependencies, acceptance criteria, validation
     expectations, handoff audience, and expected completion signal.
   - Generated task-card paths or equivalent packet references become runtime
     references for downstream traceability.

6. **Dispatch bounded work**
   - Specialist agents or reviewers execute only the assigned deliverables and
     respect prohibited edits.
   - Agents classify material claims as source-backed, inferred, assumed, or
     open where that affects scope, architecture, validation, governance,
     dependencies, or operations.

7. **Validate outputs**
   - Deterministic checks cover expected file presence, required sections,
     trace markers, ID format, source immutability, and completion-signal
     format where applicable.
   - Review-only checks are routed to named reviewer roles.

8. **Record human review and approval decisions**
   - Gate owners approve, reject, request changes, escalate, defer, or mark not
     applicable with evidence and rationale.
   - Downstream work proceeds only within the accepted scope and limitations.

9. **Publish handoff outputs**
   - Agent or integrator handoff identifies changed artifacts, validation
     performed/not performed, assumptions/open questions, runtime references,
     blockers, follow-up owner, and completion signal.
   - Material runtime-only findings are promoted into canonical docs, work
     items, decisions, or handoff packages before downstream reliance.

## Alternate paths

| Path | Trigger | Required behavior | Resulting state |
| --- | --- | --- | --- |
| Discovery-only creation | Sources or requirements are incomplete but useful refinement is safe | Narrow task packet to discovery/refinement, name open questions, avoid implementation claims | `draft`, `partial-complete`, or `needs-spike` |
| Partial launch | Some roles are ready and others are blocked | Launch only disjoint, dependency-safe work; record blocked roles and owner | `running` with blocked task packets |
| Shared artifact coordination | Multiple agents may update one deliverable | Assign one owner or merge contract before dispatch | `ready` only after ownership is explicit |
| Validation exception | Deterministic check fails or is unavailable | Record failed/not-run status, limitation, reviewer role, and recovery action | `review-needed` or `blocked` |
| Review request changes | Reviewer rejects or requests changes | Create revised packet, recovery task, or open decision with affected downstream work | `needs-revision` or `blocked` |
| Token budget split | Agent cannot complete assigned scope within capacity | Emit `TOKEN_BUDGET_LOW` or `PARTIAL_COMPLETE`, preserve output, list remaining paths | `partial-complete` |
| Future-scope detection | UI, runtime, storage, event, telemetry, provider, tenancy, compliance, or legacy specifics appear without accepted decision | Reframe as technology-neutral contract or open/future decision | `blocked`, `deferred`, or `needs-spike` |

## Errors, blockers, and recovery

| Error or blocker | Detection point | Impact | Recovery expectation |
| --- | --- | --- | --- |
| Missing source packet or canonical source | Launch readiness check | Workflow cannot be safely scoped | Block launch, assign source owner, update packet or canonical doc. |
| Ambiguous role boundary or reviewer | Task-generation check | Generated packet is not assignable | Keep packet `draft` or `blocked`, name role/reviewer owner. |
| Missing deliverable or write target | Launch or task-packet validation | Agent may edit wrong artifact or produce unusable output | Add exact path, owner, and prohibited edits before dispatch. |
| Unsafe parallelism | Concurrency review | Merge conflicts or contradictory canonical truth | Assign single owner, sequence work, or split deliverables. |
| Command/task generation failure | CLI-assisted start | No reliable task cards or runtime context | Preserve command/log reference, identify failure class, rerun only after cause is addressed. |
| Invalid task packet | Packet validation | Downstream work may be incomplete or unsafe | Correct required fields before assignment. |
| Prohibited edit risk or violation | Source-immutability check or handoff | Source integrity and trust are compromised | Stop downstream reliance, identify impact, assign recovery owner; `raw/` and `research/` remain prohibited. |
| Failed deterministic validation | Validation result | Artifact cannot be accepted as complete | Record failed criterion, evidence, owner, and recovery task. |
| Review-only gate lacks reviewer | Human approval checkpoint | Approval cannot be granted | Block the gate until reviewer role is named. |
| Runtime/log reference unavailable | Handoff or telemetry review | Reproducibility or trust may be limited | Record limitation; summarize available evidence into durable docs if material. |
| Open architecture/governance decision | Review or future-scope check | Implementation-specific claims are unsafe | Mark open/deferred, assign decision owner, avoid stack/runtime/policy commitment. |

Recovery records should include trigger, affected targets, current state,
preserved output, downstream impact, owner, recovery action, and validation or
review needed before reliance resumes.

## Human review and approval gates

| Gate | Trigger | Reviewer role | Required evidence | Downstream effect |
| --- | --- | --- | --- | --- |
| Launch readiness | Workflow creation inputs are complete enough to generate tasks | Orchestrator, integrator, or tech lead | Source packet, workflow IDs, role bindings, deliverables, dependencies, validation expectations | Creation proceeds, narrows, or blocks. |
| Shared artifact ownership | One deliverable has multiple potential editors | Integrator | Write-target list, dependency notes, merge contract | Parallel work proceeds only after owner/contract exists. |
| Task-packet assignability | Generated packet may be incomplete | Orchestrator or validator owner | Required task-packet fields and prohibited edits | Packet becomes assignable or remains draft/blocked. |
| Deliverable acceptance | Agent output is ready for downstream use | Domain reviewer, architect, or integrator | Changed artifacts, validation summary, assumptions/open questions, runtime references | Output becomes ready-to-consume, needs revision, or remains blocked. |
| Validation exception | Check fails, is unavailable, or cannot judge quality | Validator owner or gate-specific reviewer | Failed/not-run result, limitation, recovery recommendation | Recovery task, accepted limitation, or review-only approval is recorded. |
| Reusable behavior change | Workflow template, persona, standard, or validator rule changes future agents | Configuration/standards owner | Proposed change, rationale, compatibility impact, affected workflows | Accepted, rejected, deferred, or escalated. |
| Security/privacy/governance concern | Sensitive data, retention, access, compliance, approval policy, or tenancy affects claims | Security/privacy or governance reviewer | Claim, evidence class, open decision, affected implementation work | Claim is blocked, deferred, or escalated. |

Approval decisions must include decision, rationale, evidence reviewed, affected
downstream work, and recovery action. Lack of a named reviewer blocks
review-only approval.

## Validation points

| Point | Check class | MVP1 evidence |
| --- | --- | --- |
| Pre-launch | Required files and metadata | Workflow/input packet exists; workflow, phase, iteration, role, deliverable, dependency, validation, and handoff fields are present. |
| Pre-dispatch | Task-packet completeness | Each packet includes required AI Agent Standards inputs and expected completion signal. |
| Concurrency review | Shared artifact ownership | Disjoint write targets or one owner/merge contract is recorded. |
| Source safety | Source immutability | `raw/` and `research/` are not edited or required as write targets. |
| Deliverable review | Required sections/headings | Workflow docs include happy path, alternates, errors, approvals, observability, validation, handoff, and future transitions. |
| Traceability | Trace markers and stable IDs | Workflow/phase/iteration IDs, task packet IDs, gate IDs, validation IDs, and runtime references are citeable. |
| Completion | Completion-signal format | Handoff uses `TASK_COMPLETE`, `TOKEN_BUDGET_LOW`, `BLOCKED`, or `PARTIAL_COMPLETE` when specialist-agent standards apply. |
| Readiness | Review-only quality | Reviewer role, rationale, limitation, and follow-up owner are recorded for subjective criteria. |

Validation statuses align to the logical data model: `not-run`, `passed`,
`failed`, `review-needed`, or `not-applicable`.

## Observability and telemetry references

MVP1 observability is reference-based. The workflow should preserve enough
context for recovery and future implementation without selecting a telemetry
backend.

| Reference or signal | MVP1 representation | Consumer |
| --- | --- | --- |
| CLI invocation | Command label, workflow/phase/iteration arguments, runtime/log path when available | Orchestrator, integrator, validator |
| Generated task card | Task-card path or task-packet ID | Specialist agent, reviewer, validator |
| Agent completion | Completion signal and memo/handoff status | Integrator, downstream agent, recovery owner |
| Validation result | Validation result ID, check class, status, evidence, run context | Reviewer, integrator, orchestrator |
| Human review | Gate ID, reviewer role, decision, rationale, affected downstream work | Orchestrator, downstream owner |
| Process learning | Repeated blocker, validation gap, token-budget issue, quality issue | Standards owner, workflow-template owner, backlog owner |

Conceptual signal families may align with `workflow`, `agent_task`, `handoff`,
`approval`, `validation`, and `telemetry` event families. For MVP1 these are
Markdown/log/memo references, not implemented events. Missing runtime references
must be recorded as limitations when they affect trust or reproducibility.

## Handoff outputs

A complete or partial Create Workflow handoff includes:

- workflow ID, phase ID, iteration ID, and source packet path;
- generated task-card or role-packet references;
- changed deliverables and allowed write targets;
- validation performed, validation not performed, and review-needed items;
- human review decisions or pending gates;
- assumptions, open questions, risks, blockers, and recovery actions;
- runtime/log references, branch/SHA, or command labels when available;
- confirmation that prohibited files and directories were not edited;
- downstream consumers that may proceed and work that must wait; and
- completion signal:

```text
TASK_COMPLETE: <completed>/<target> artifacts generated
TOKEN_BUDGET_LOW: Completed <n>/<target>; remaining: <paths>
BLOCKED: <blocking decision/source/dependency>; impact: <affected deliverables>
PARTIAL_COMPLETE: Completed <n>/<target>; remaining: <paths>; recovery: <recommended split>
```

## Future visual and runtime transitions

MVP1 deliberately captures semantics that a future visual designer or runtime
could consume, while keeping implementation choices open.

| MVP1 contract | Future transition candidate | Required future decision before implementation |
| --- | --- | --- |
| Workflow definition fields | Visual workflow/template model or workflow API | Graph format, diff/version strategy, template publication model, and UX ownership. |
| Iteration and task-packet records | Runtime workflow-run and task-dispatch model | State store, scheduler, retry behavior, pause/resume semantics, and API protocol. |
| Memo/handoff records | Runtime handoff or notification service | Durable messaging/audit needs, access model, retention, and consumer behavior. |
| Validation result records | Validator service or CI-style readiness checks | Machine-readable schema, check runner, evidence storage, and failure policy. |
| Human review gates | Approval workflow | Policy thresholds, escalation, expiry, durable approval ledger, and governance model. |
| Runtime/log references | Observability platform | Telemetry backend, trace context, metrics/log retention, alerting, and SLO model. |
| Conceptual event families | Implemented platform events | Transport, schema registry, versioning, idempotency, ordering, retry, dead-letter, replay, and security/privacy gates. |

Future transitions must preserve MVP1 ownership, validation, approval, recovery,
and source-immutability semantics. They must not infer UI, runtime, storage,
event, telemetry, provider, tenancy, compliance, or legacy-adapter commitments
from this Markdown workflow alone.

## Acceptance expectations

This workflow specification is acceptable for MVP1 when:

- it remains scoped to Markdown/CLI and the orchestration-framework domain;
- happy path, alternate paths, errors/blockers, approvals, observability,
  validation, handoff, and future transition notes are explicit;
- required task-packet fields and completion signals align with AI Agent
  Standards;
- validation and review-only gates are separated;
- telemetry/event language stays conceptual and technology-neutral;
- `raw/` and `research/` remain prohibited edit targets; and
- assumptions and open decisions are visible rather than converted into
  implementation commitments.

## Assumptions and open decisions

| ID | Item | Current MVP1 handling |
| --- | --- | --- |
| OQ-CW-001 | Which workflow/task-packet fields must become machine-readable for validators? | Keep Markdown-first structured sections and tables until a bounded validator spike proves schema extraction is needed. |
| OQ-CW-002 | Who is the named accountable approver for each gate family? | Use role-based reviewer ownership until named individuals or teams are accepted. |
| OQ-CW-003 | Which CLI command intents become stable product APIs? | Treat current boundaries as repository-first command intents; defer product API/runtime choices. |
| OQ-CW-004 | Which runtime/log references must be retained after workflow creation? | Summarize material findings into canonical docs or handoff packages; leave retention policy open. |
| OQ-CW-005 | How should the future visual designer represent MVP1 workflow/task contracts? | Defer graph/canvas representation until the Markdown-first model is validated. |
| OQ-CW-006 | What event, telemetry, approval, tenancy, compliance, and provider infrastructure should support future execution? | Keep future/open and require accepted architecture/governance decisions before implementation. |

