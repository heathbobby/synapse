# Event Contract Standards

- **Status**: canonical draft
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration context**: `mvp1-iteration-03-integrations`
- **Last updated**: 2026-05-03

## Purpose

Define reusable, technology-neutral event and integration contract standards for
MVP1 and later Synapse domains. These standards describe naming, ownership,
payload, correlation, idempotency, ordering, retry, dead-letter, approval,
validation, telemetry, schema versioning, and review-gate expectations before
any concrete event transport, schema registry, runtime, storage, replay, or
telemetry implementation is selected.

## Source basis

| Source | Standard use |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp1-iteration-03-integrations.md` | Requires reusable integration standards covering synchronous, asynchronous, human-in-loop, telemetry, failure, and ownership flows. |
| `docs/MVP1/Platform/Integrations.md` | Defines MVP1 integration participants, logical contracts, human gates, telemetry references, recovery flows, and future event families. |
| `docs/MVP1/Platform/DataModel.md` | Provides logical records, identifiers, lifecycle states, validation records, readiness gates, runtime references, and future-scope boundaries. |
| `docs/architecture/TECHNICAL_SPECIFICATIONS.md` | Names conceptual event families and required future capabilities: ownership, schema versioning, idempotency, retries, dead-letter handling, trace correlation, and audit/replay reconstruction. |
| `docs/architecture/DECISIONS.md` | Records ADR-0004 hybrid event-bus direction and OAD-0004 open transport/schema/registry strategy; records ADR-0011 through ADR-0014 for CLI-assisted, Markdown-first MVP1. |

## Scope and non-commitments

These standards apply to:

- MVP1 logical integration events described in canonical Markdown, task packets,
  memos, validation results, readiness gates, and runtime references;
- future implemented platform events such as workflow, task, approval,
  validation, knowledge-loop, telemetry, and adapter events; and
- domain-specific extension events that integrate with the Synapse platform.

These standards do not select or imply:

- event transport, broker, queue, stream, or hybrid event-bus product;
- schema language, serialization format, schema registry, or compatibility tool;
- replay, audit-log, state-store, scheduler, retry engine, or dead-letter
  implementation;
- telemetry backend, tracing system, metrics store, dashboard, or alerting tool;
  or
- approval queue, policy engine, durable approval ledger, or access-control
  implementation.

Those implementation choices remain future/open until accepted by architecture
decision records and domain requirements.

## Contract levels

| Level | Meaning | MVP1 expectation |
| --- | --- | --- |
| Conceptual event | A named event family, owner, payload intent, and consumer expectation documented in Markdown. | Required for MVP1 standards, integrations, readiness gates, and future backlog. |
| Logical contract | A field-level contract for an event or integration object without serialization, transport, or storage commitments. | Required before downstream work relies on event semantics. |
| Implemented event | A transport-specific event with schema, producer, consumer, retry, idempotency, observability, and failure handling implemented. | Future/open; must pass the review gates in this standard before implementation. |

## Event family naming

Event families group related state changes or signals under a stable conceptual
namespace. Names must be understandable in Markdown and adaptable to future
schema or transport implementations.

### Naming pattern

Use this conceptual pattern:

```text
<family>.<event_action>
```

When a sub-domain is needed, use:

```text
<family>.<sub_family>.<event_action>
```

Naming rules:

- Use lowercase words separated by underscores.
- Use past-tense actions for facts that already occurred, such as
  `workflow.started` or `approval.decided`.
- Use explicit request actions for human or integration requests that are not yet
  outcomes, such as `approval.requested`.
- Avoid transport, vendor, endpoint, table, or queue names in event names.
- Avoid encoding schema version, environment, tenant, or routing destination in
  the event name.
- Keep core platform event families separate from domain-specific extension
  families.

### Core event families

| Family | Example conceptual events | Primary meaning |
| --- | --- | --- |
| `workflow` | `workflow.started`, `workflow.paused`, `workflow.completed`, `workflow.failed`, `workflow.cancelled` | Workflow-run lifecycle and terminal state changes. |
| `workflow_step` | `workflow_step.started`, `workflow_step.completed`, `workflow_step.blocked` | Step-level progress, dependency, and blocking signals. |
| `agent_task` | `agent_task.dispatched`, `agent_task.progressed`, `agent_task.completed`, `agent_task.partial`, `agent_task.blocked` | Agent or human task execution state and completion signals. |
| `handoff` | `handoff.ready_to_consume`, `handoff.ready_to_merge`, `handoff.blocked`, `handoff.consumed` | Memo/handoff availability, limits, and downstream readiness. |
| `approval` | `approval.requested`, `approval.decided`, `approval.escalated`, `approval.expired` | Human-in-the-loop review and approval checkpoints. |
| `validation` | `validation.requested`, `validation.completed`, `validation.failed`, `validation.review_needed` | Deterministic and review-only validation outcomes. |
| `telemetry` | `telemetry.signal_recorded`, `telemetry.quality_issue_detected`, `telemetry.learning_pattern_detected` | Operational, quality, and continuous-improvement signals. |
| `knowledge_asset` | `knowledge_asset.proposed`, `knowledge_asset.approved`, `knowledge_asset.superseded` | Knowledge-loop events that affect reusable context. |
| `persona` | `persona.updated`, `persona.promoted`, `persona.retired` | Persona and role-behavior changes. |
| `workflow_template` | `workflow_template.updated`, `workflow_template.promoted`, `workflow_template.retired` | Reusable workflow template changes. |
| `legacy_bridge` | `legacy_bridge.observation_captured`, `legacy_bridge.requirement_extracted`, `legacy_bridge.action_completed` | Adapter-bounded legacy integration signals. |
| `integration` | `integration.requested`, `integration.completed`, `integration.failed`, `integration.recovery_required` | Generic external or domain integration activity when no narrower family fits. |

Domain-specific events may add a domain prefix or family only after the contract
states how the domain event maps to core workflow, task, approval, validation,
or telemetry semantics.

## Ownership standards

Every event contract must name accountable owners before implementation.

| Ownership role | Responsibility |
| --- | --- |
| Contract owner | Maintains event semantics, required fields, versioning policy, compatibility decisions, and review readiness. |
| Producer owner | Owns emission rules, source-of-truth state transition, payload population, idempotency key creation, and producer telemetry. |
| Consumer owner | Owns consumption behavior, idempotency, ordering assumptions, error handling, and downstream side effects. |
| Reviewer or gate owner | Approves review-only claims, behavior-affecting changes, security/privacy concerns, and compatibility risk. |
| Recovery owner | Owns failed, partial, dead-lettered, blocked, or unprocessable events until resolution or accepted limitation. |

Ownership rules:

- One event family may have many producers, but each specific event contract must
  identify the authoritative producer for the fact being emitted.
- Consumers must not infer ownership of source state from receiving an event.
- Shared deliverables, reusable workflow/persona changes, and approval outcomes
  require explicit owner and reviewer roles.
- If the producer, consumer, reviewer, or recovery owner is unknown, the event
  remains conceptual and must not be implemented as a stable contract.

## Logical event envelope

Future implemented events should include an envelope with stable metadata.
MVP1 may represent these fields as Markdown table columns or structured
sections rather than serialized messages.

| Field | Requirement |
| --- | --- |
| `event_id` | Unique identifier for one emitted event instance. |
| `event_name` | Conceptual name following the family naming standard. |
| `event_family` | Family namespace, such as `workflow`, `agent_task`, or `approval`. |
| `event_version` | Contract version for this event shape and semantics. |
| `occurred_at` | Time the source fact occurred; format remains implementation-specific. |
| `published_at` | Time the event was emitted, when different from occurrence time. |
| `producer` | Producing component, role, workflow, task, or adapter. |
| `producer_owner` | Accountable owner for emission correctness. |
| `source_record_type` | Logical source record, such as workflow run, task packet, validation result, readiness gate, memo, or adapter action. |
| `source_record_id` | Stable identifier of the source record. |
| `correlation_id` | End-to-end correlation identifier across workflow, task, approval, validation, telemetry, and recovery flows. |
| `causation_id` | Identifier of the event, command, task, approval, or validation that caused this event, when known. |
| `idempotency_key` | Stable key consumers can use to ignore duplicate event effects. |
| `ordering_key` | Key that defines the only ordering scope consumers may rely on, when ordering matters. |
| `payload` | Event-specific logical fields. |
| `schema_ref` | Future/open reference to schema location or registry entry; not required for MVP1 Markdown-first contracts. |
| `trace_context` | Future/open trace or runtime reference for logs, command invocations, branch/SHA, or workflow run context. |

Envelope rules:

- `event_id` identifies an emission; `idempotency_key` identifies the business
  effect that should not be applied twice.
- `correlation_id` must be stable across a workflow or integration chain.
- `causation_id` links immediate cause and effect when reconstructing a flow.
- `ordering_key` must be explicit if consumers depend on ordering; otherwise
  consumers must assume events may arrive out of order or more than once.

## Logical payload field standards

Payloads must carry the minimal business fact needed by consumers plus enough
context for validation, approval, telemetry, and recovery. They must not expose
transport concerns or duplicate unrelated source records.

### Required payload categories

| Category | Fields to consider | Applies to |
| --- | --- | --- |
| Source identity | `workflow_id`, `workflow_version`, `workflow_run_id`, `phase_id`, `iteration_id`, `step_id`, `task_packet_id`, `deliverable_id`, `memo_id`, `validation_result_id`, `readiness_gate_id` | Workflow, task, handoff, validation, approval, telemetry. |
| State transition | `previous_state`, `new_state`, `status`, `completion_signal`, `decision`, `resulting_state` | Lifecycle, approval, validation, recovery events. |
| Ownership | `producer_role`, `assignee_role`, `reviewer_role`, `follow_up_owner`, `recovery_owner` | Tasks, approvals, validation, handoffs, recovery. |
| Evidence and references | `canonical_sources`, `changed_artifacts`, `evidence_reviewed`, `validation_summary`, `runtime_references`, `decision_question_ids` | Review, validation, handoff, telemetry, knowledge-loop events. |
| Dependency and impact | `dependencies`, `affected_targets`, `affected_downstream_work`, `blocking_decision_question_ids`, `impact` | Workflow, approval, validation, recovery. |
| Failure and recovery | `failure_class`, `failure_reason`, `retryable`, `attempt_count`, `dead_letter_reason`, `recovery_action`, `preserved_output` | Failed, partial, blocked, retry, dead-letter, recovery events. |
| Governance | `evidence_class`, `risk_label`, `policy_basis`, `prohibited_edits_confirmed`, `sensitive_data_flag` | Human approval, security/privacy, knowledge, adapter events. |

Payload rules:

- Required fields must be documented per event contract before implementation.
- Optional fields must state when they are expected and how consumers behave when
  absent.
- Payloads should reference large artifacts by stable path or identifier rather
  than embedding complete documents.
- Payloads must preserve evidence class where claims affect scope, architecture,
  data contracts, validation, security/privacy, dependencies, or operations.
- MVP1 events and integration records must not require modification of `raw/` or
  `research/`; promoted claims belong in canonical docs or approved extracts.

## Correlation and traceability

Every event contract must define correlation semantics.

| Identifier | Use |
| --- | --- |
| `correlation_id` | Groups all events, commands, validations, approvals, handoffs, telemetry, and recovery actions for one workflow run or integration chain. |
| `causation_id` | Links an event to the command, event, task, approval, or validation that directly caused it. |
| `source_record_id` | Links an event to the authoritative logical record that owns the fact. |
| `runtime_reference_id` | Links to operational logs, memos, task cards, command output, branch/SHA, or trace references when available. |
| `decision_question_id` | Links events to accepted decisions, open questions, assumptions, blockers, or deferred decisions. |

Correlation rules:

- A workflow run or equivalent integration chain should create the primary
  `correlation_id`.
- Task, approval, validation, handoff, and telemetry events must preserve the
  existing `correlation_id` when triggered within that chain.
- Cross-workflow or cross-domain handoffs should record both the incoming and
  outgoing correlation context when future implementation supports it.
- Missing runtime/log context must be recorded as a limitation if it affects
  trust, recovery, or downstream reliance.

## Idempotency standards

Event consumers must be idempotent. Producers must provide enough metadata for
consumers to detect duplicate business effects.

Idempotency rules:

- Every event contract must define an `idempotency_key` strategy.
- The key should be derived from stable business identity and effect, not from a
  delivery attempt.
- Consumers must tolerate duplicate delivery of the same event instance and
  duplicate delivery of equivalent business effects.
- Side-effecting consumers must record enough processing state to avoid applying
  the same effect twice.
- Events that request human approval, validation, external adapter actions, or
  knowledge promotion must define whether repeated requests create a new request
  or update/retry an existing one.

Recommended key patterns:

| Event type | Example idempotency basis |
| --- | --- |
| Workflow lifecycle | `{workflow_run_id}:{new_state}:{state_transition_sequence}` |
| Task completion | `{task_packet_id}:{completion_signal}:{artifact_revision}` |
| Approval decision | `{readiness_gate_id}:{decision}:{decision_revision}` |
| Validation result | `{target_id}:{check_class}:{run_context}` |
| Handoff readiness | `{memo_id}:{status}:{changed_artifact_revision}` |
| Adapter action | `{adapter_id}:{external_target_id}:{action}:{request_revision}` |

## Ordering standards

Ordering is never implicit. Event contracts must state whether ordering matters
and what key scopes the ordering requirement.

Ordering rules:

- Consumers must assume events can be delivered out of order unless the contract
  explicitly defines an `ordering_key` and ordering guarantee.
- Ordering should be scoped narrowly, such as one workflow run, task packet,
  readiness gate, validation target, or external adapter target.
- Events should carry enough state context for consumers to handle late or
  repeated messages safely.
- Consumers should reject, ignore, hold, or reconcile stale state transitions
  according to documented contract behavior.
- Cross-family global ordering must not be required for MVP1 and should be
  avoided in future implementations unless an accepted architecture decision
  justifies it.

## Retry and dead-letter concepts

MVP1 defines retry and dead-letter concepts only. Concrete retry engines,
queues, backoff algorithms, dead-letter stores, replay tools, and operational
runbooks are future/open.

### Retry contract fields

| Field | Requirement |
| --- | --- |
| `retryable` | Whether the failed operation may be retried without human review. |
| `attempt_count` | Number of attempts made, when known. |
| `failure_class` | Missing input, validation failure, transient dependency, permission issue, conflict, partial completion, token budget, policy gate, external adapter failure, or unknown. |
| `failure_reason` | Human-readable reason and evidence. |
| `next_retry_after` | Future/open timing hint when implementation supports it. |
| `max_attempts` | Future/open policy value when implementation supports it. |
| `recovery_owner` | Owner accountable when retry does not or should not proceed. |

Retry rules:

- Retrying must not violate idempotency or create duplicate external side
  effects.
- Validation failures, approval rejections, prohibited edits, policy blockers,
  and ambiguous ownership are not automatically retryable.
- Partial completions should preserve useful output and create bounded follow-up
  work instead of blind retries.
- Token-budget failures should be routed to recovery with remaining scope and
  preserved output.

### Dead-letter concept

A dead-lettered event is an event or requested effect that could not be
processed within the documented contract and requires recovery.

Dead-letter records should include:

- original event metadata and payload reference;
- consumer and consumer owner;
- failure class and failure reason;
- retry history or reason retry is unsafe;
- affected workflow, task, approval, validation, deliverable, or adapter target;
- impact on downstream work;
- recovery owner and recovery action; and
- validation or review needed before reprocessing or accepting the limitation.

Dead-letter rules:

- Dead-letter handling is a recovery workflow, not just a storage location.
- Dead-lettered human approval, validation, adapter, or governance events must
  not be silently dropped.
- Reprocessing dead-lettered events requires idempotency and ordering review.

## Human approval event standards

Human approval events are first-class integration boundaries. They preserve
accountability for review-only quality, architecture fit, security/privacy,
risk, dependencies, reusable behavior changes, and implementation readiness.

### Approval event types

| Event | Meaning |
| --- | --- |
| `approval.requested` | A gate requires human decision before downstream work proceeds. |
| `approval.decided` | Reviewer approved, rejected, requested changes, escalated, deferred, or marked not applicable. |
| `approval.escalated` | Review responsibility moved to another reviewer or governance path. |
| `approval.expired` | A requested approval exceeded its expected decision window, if future policy defines one. |

### Approval payload fields

| Field | Requirement |
| --- | --- |
| `readiness_gate_id` | Gate family plus target identifier. |
| `gate_family` | Product, requirements traceability, architecture/technical, quality, dependency, risk, implementation, security/privacy, agent-output, or reusable-asset. |
| `target_type` | Workflow, iteration, task packet, deliverable, work item, reusable config, handoff, validation result, or adapter action. |
| `target_id` | Identifier of the gated target. |
| `reviewer_role` | Role accountable for the decision. |
| `evidence_reviewed` | Deliverables, validation results, runtime summaries, decisions, assumptions, risks, or policy basis reviewed. |
| `decision` | Approve, reject, request changes, escalate, defer, or not applicable. |
| `rationale` | Reason for decision and limits of approval. |
| `affected_downstream_work` | Work that may proceed or must wait. |
| `recovery_action` | Required follow-up when not approved. |
| `resulting_state` | Workflow, task, gate, or deliverable state after decision. |

Approval rules:

- Lack of a named reviewer blocks review-only approval.
- Approval decisions must include evidence reviewed and rationale.
- Approval events must correlate back to the blocking workflow step, task,
  validation result, or deliverable.
- Approval requests should be idempotent: repeated requests for the same gate and
  target should not create duplicate unresolved decisions unless the contract
  intentionally creates a new revision.
- Security/privacy, governance, reusable workflow/persona changes, and
  validation exceptions require explicit review before downstream reliance.

## Validation and telemetry event standards

Validation and telemetry events make readiness and continuous improvement
visible without committing to a telemetry backend.

### Validation events

Validation events must distinguish deterministic checks from review-only checks.

Required validation payload fields:

- `validation_result_id`
- `target_type`
- `target_id`
- `check_class`
- `criteria`
- `status`
- `evidence`
- `run_context`
- `follow_up_owner`
- `related_decision_question_ids`

Validation status values should align with MVP1 logical data contracts:

- `not-run`
- `passed`
- `failed`
- `review-needed`
- `not-applicable`

Validation rules:

- Failed validation creates a recovery obligation.
- Review-needed status creates a human gate rather than deterministic approval.
- Validation events must not imply subjective acceptance unless a reviewer
  decision is also recorded.
- Repeated validation gaps should produce telemetry or backlog signals for
  standards, workflow templates, task packets, or validator improvements.

### Telemetry events

Telemetry events capture operational and quality signals. They are not durable
product truth unless summarized into canonical docs, decisions, work items, or
handoff packages.

Telemetry payloads should include:

- signal family;
- related workflow, task, approval, validation, deliverable, or adapter target;
- correlation and runtime references;
- summary;
- impact;
- recurrence or count when known;
- limitation; and
- candidate promotion target when the signal may update standards, validators,
  workflow templates, personas, or backlog.

Telemetry rules:

- Repeated agent failures, token-budget issues, blocked approvals, validation
  gaps, and quality issues should be visible as telemetry/process-learning
  signals.
- Logs and traces should distinguish core platform behavior from domain-specific
  adapter behavior.
- Operational-only logs must be summarized before downstream implementation
  relies on them as durable evidence.

## Schema versioning and compatibility

Schema language, serialization, and schema registry implementation are
future/open. Contract versioning is still required conceptually.

Versioning rules:

- Every implemented event contract must have an `event_version`.
- Version changes must describe semantic changes, required field changes,
  compatibility impact, producer changes, consumer migration expectations, and
  review outcome.
- Additive optional fields may be compatible only if existing consumers can
  safely ignore them.
- Changing event meaning, required fields, identifier semantics, idempotency
  keys, ordering keys, or state-transition semantics is a breaking change unless
  proven otherwise by review.
- Removing fields, changing field type/meaning, or changing ownership semantics
  requires a new version or accepted migration plan.
- Domain-specific extensions must not change core event semantics.

Recommended conceptual version format:

```text
v<major>
```

Use a new major version for breaking semantic or payload changes. More detailed
versioning may be selected later with the schema registry decision.

## Review gates before implementation

No event should move from conceptual/logical contract to implemented event until
the following gates are satisfied or explicitly deferred with owner and impact.

| Gate | Required evidence |
| --- | --- |
| Naming and family gate | Event name follows standards; family boundary is clear; domain extension does not alter core semantics. |
| Ownership gate | Contract owner, authoritative producer, consumer owners, reviewer/gate owner, and recovery owner are named. |
| Payload gate | Required and optional logical fields are documented; source record and state transition semantics are clear. |
| Correlation gate | `correlation_id`, `causation_id`, source record, runtime reference, and decision/open-question linkage are defined where applicable. |
| Idempotency gate | Idempotency key strategy and consumer duplicate-handling behavior are documented. |
| Ordering gate | Ordering assumptions and `ordering_key` are documented, or consumers explicitly assume out-of-order delivery. |
| Retry/dead-letter gate | Retryability, failure classes, recovery ownership, and dead-letter concept are documented. |
| Human approval gate | Human gates name reviewer role, evidence, decision values, downstream effect, and recovery behavior. |
| Validation/telemetry gate | Deterministic vs review-only validation and telemetry/process-learning signals are documented. |
| Versioning gate | Initial version and compatibility expectations are documented. |
| Security/privacy/governance gate | Sensitive data, prohibited edits, access, retention, compliance, and policy assumptions are marked accepted, open, or not applicable. |
| Implementation-decision gate | Event transport, schema registry, replay, and observability choices are either accepted in architecture decisions or explicitly marked future/open. |

## Event contract template

Use this template for future event contracts or Markdown-first MVP1 logical
events:

```markdown
### `<event_name>`

- **Family**:
- **Contract status**: conceptual | logical | implemented
- **Version**:
- **Contract owner**:
- **Authoritative producer**:
- **Producer owner**:
- **Consumers**:
- **Consumer owners**:
- **Reviewer/gate owner**:
- **Recovery owner**:

**Purpose**

**Trigger/source-of-truth transition**

**Logical envelope fields**

**Logical payload fields**

**Correlation and causation**

**Idempotency strategy**

**Ordering assumptions**

**Retry and dead-letter behavior**

**Human approval behavior, if applicable**

**Validation and telemetry behavior**

**Compatibility/versioning notes**

**Security/privacy/governance notes**

**Open decisions and implementation non-commitments**
```

## MVP1 application guidance

For MVP1, events may be represented as:

- integration-contract sections in `docs/MVP1/Platform/Integrations.md`;
- logical records in `docs/MVP1/Platform/DataModel.md`;
- task-packet metadata and completion signals;
- agent-sync memos and handoff summaries;
- validation result tables or command-output summaries;
- readiness gate decisions; and
- runtime/log references summarized into canonical docs.

MVP1 event-like records should still follow these standards for naming,
ownership, correlation, validation, approval, failure, and recovery even though
no event bus, schema registry, replay mechanism, or telemetry backend is
implemented.

## Assumptions

- Markdown-first structured sections and tables are sufficient for MVP1 logical
  event contracts until validator work proves a concrete schema need.
- The orchestration framework's task cards, memos, validation summaries, and
  runtime references provide enough operational context for MVP1 integration
  contracts.
- Future Synapse runtime work will need implemented events, but implementation
  choices should follow accepted architecture decisions rather than this
  standard selecting a stack.
- Human reviewers remain accountable for review-only quality, approval gates,
  governance concerns, and compatibility risk.

## Open decisions

| ID | Decision needed | Current guidance |
| --- | --- | --- |
| OQ-ECS-001 | Which event transport, broker, queue, stream, or hybrid event-bus implementation should Synapse use? | Future/open; follow these logical standards until throughput, latency, durability, and operating constraints are known. |
| OQ-ECS-002 | Which schema language, serialization format, and schema registry should be used? | Future/open; use Markdown-first logical fields for MVP1 and require versioned contracts before implementation. |
| OQ-ECS-003 | What replay, audit reconstruction, and dead-letter tooling should be implemented? | Future/open; document conceptual replay and recovery needs per contract before selecting tooling. |
| OQ-ECS-004 | What telemetry backend, trace context format, metrics store, dashboard, or alerting system should be used? | Future/open; preserve correlation and runtime references without choosing observability technology. |
| OQ-ECS-005 | What approval policy thresholds, expiration rules, escalation paths, and durable approval ledger are required? | Future/open; MVP1 records reviewer role, evidence, decision, rationale, downstream effect, and recovery action. |
| OQ-ECS-006 | Which fields require machine-readable extraction for MVP1 validators? | Keep Markdown-first contracts; introduce schemas only after a bounded validator spike proves the need. |
