# MVP1 Platform Operational Runbook

- **Status**: draft MVP1 release operations runbook
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-06-release-operations`
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

This runbook defines operational readiness for MVP1 release operations. MVP1 is a
repository-first, CLI-assisted concept-to-implementation pipeline over the
existing orchestration framework. Operations therefore mean preparing, launching,
monitoring, validating, recovering, and handing off workflow/task-packet work
using canonical documentation, orchestration configuration, runtime memos, task
cards, logs, validation summaries, and review gates.

This runbook does not define or require a hosted workflow runtime, production
deployment system, telemetry backend, event bus, schema registry, approval
automation, persistent storage layer, product API, provider runtime, tenancy
model, compliance implementation, visual UI, or legacy adapter.

## Source register

| Source | Runbook use |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp1-iteration-06-release-operations.md` | Iteration goal and completion criteria for release operations and handoff. |
| `docs/MVP1/Platform/Overview.md` | MVP1 operating boundary, in-scope repository/CLI model, deferred areas, and downstream readiness criteria. |
| `docs/MVP1/Platform/Infrastructure.md` | Canonical paths, CLI-assisted infrastructure, validation scope, runtime artifact posture, concurrency, and recovery principles. |
| `docs/MVP1/Platform/Integrations.md` | Command/document integration contracts, participants, handoff fields, telemetry/log reference discipline, and failure/recovery flow. |
| `docs/MVP1/Platform/TestingStrategy.md` | Gate statuses, deterministic validators, review-only checks, source immutability checks, reliability/recovery checks, and readiness template. |
| `docs/MVP1/Platform/AcceptanceCriteria.md` | MVP1 acceptance criteria, readiness blockers, handoff acceptance, and Create Workflow happy/alternate/error paths. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Agent role boundaries, evidence discipline, task-packet inputs, completion signals, validation, and handoff requirements. |
| `docs/standards/EVENT_CONTRACT_STANDARDS.md` | Technology-neutral ownership, correlation, validation, approval, telemetry, retry/dead-letter concepts, and non-commitments. |

## Operational stance

1. **Canonical docs are durable truth**: operational decisions that affect
   downstream implementation must be summarized into `docs/`, work items,
   decisions, or handoff packages before reliance.
2. **Runtime artifacts are operational evidence**: generated task cards, memos,
   CLI logs, command output, branch references, and SHAs support operations but
   are not durable product storage.
3. **Validation gates precede handoff**: deterministic checks and review-only
   gates must be recorded before a deliverable is treated as ready.
4. **Failures become bounded recovery work**: blocked, partial, invalid,
   conflicted, token-limited, or review-rejected work must preserve useful
   output, state impact, name an owner, and identify validation/review needed.
5. **Source immutability is a release guardrail**: MVP1 tasks must not modify
   `raw/` or `research/` files unless a future canonical rule explicitly grants
   authority.
6. **Future implementation choices remain open**: runtime, storage, telemetry,
   event transport, schema registry, approval automation, provider, tenancy,
   compliance, UI, and legacy-adapter choices must stay future/open unless
   accepted by later canonical decisions.

## Roles and ownership

| Role | Operational responsibilities |
| --- | --- |
| Orchestrator | Confirm launch inputs, start or prepare workflow iterations, generate or identify task packets, monitor progress, route blockers, and coordinate reruns or recovery. |
| Specialist agent | Execute assigned deliverables within scope, preserve evidence discipline, avoid prohibited edits, validate or state validation limits, and emit a standard completion signal. |
| Integrator | Consume ready-to-consume memos, reconcile shared artifacts, decide downstream safety, coordinate final readiness handoff, and route unresolved blockers. |
| Validator owner | Run or review deterministic checks, record evidence, classify `not-run`/`failed`/`review-needed` results, and name recovery owners. |
| Reviewer / gate owner | Decide review-only gates such as product fit, architecture fit, evidence sufficiency, security/privacy, governance, risk, and implementation readiness. |
| Configuration / standards owner | Review behavior-affecting updates to workflow templates, personas, standards, validators, and reusable process assets before promotion. |
| Recovery owner | Own failed, partial, blocked, conflicted, prohibited-edit, or review-rejected work until resolved, revalidated, or accepted as a documented limitation. |

If a required owner is unknown, the affected work remains `blocked`,
`review-needed`, or `needs-spike`; it is not implementation-ready.

## Operational states and signals

Use these statuses consistently in task packets, memos, validation summaries,
readiness records, and handoffs.

| Status | Operational meaning |
| --- | --- |
| `not-run` | Required validation or review has not been performed. |
| `passed` | Deterministic criterion passed with evidence. |
| `failed` | Deterministic criterion failed and requires recovery. |
| `review-needed` | Human review is required before acceptance. |
| `approved` | Named reviewer accepted a review-only criterion with rationale. |
| `request-changes` | Named reviewer requires revision before downstream reliance. |
| `blocked` | Missing source, decision, owner, dependency, approval, or safe path prevents reliance. |
| `partial-complete` | Useful output exists but remaining scope or recovery is required before full reliance. |
| `needs-spike` | Bounded discovery is required before implementation-specific work can proceed. |
| `not-applicable` | Criterion does not apply and rationale is recorded. |

Specialist-agent completion must use exactly one standard signal:

```text
TASK_COMPLETE: <completed>/<target> artifacts generated
TOKEN_BUDGET_LOW: Completed <n>/<target>; remaining: <paths>
BLOCKED: <blocking decision/source/dependency>; impact: <affected deliverables>
PARTIAL_COMPLETE: Completed <n>/<target>; remaining: <paths>; recovery: <recommended split>
```

## Launch readiness checklist

Before launching or preparing an MVP1 workflow iteration, the orchestrator or
release operator verifies:

| Check | Ready condition | Blocks launch when |
| --- | --- | --- |
| Workflow context | `workflow_id`, `phase_id`, `iteration_id`, domain, and source packet are known. | Parent context cannot be traced. |
| Canonical sources | Required `docs/` sources and approved input packets exist. | Required source is missing or relies only on raw/research inputs. |
| Scope boundary | Work is CLI-assisted, repository-first, Markdown/configuration based, and orchestration-framework scoped. | Scope implies future runtime, UI, storage, telemetry, event, provider, compliance, or legacy implementation. |
| Role/task packet inputs | Role/objective, deliverables, prohibited edits, dependencies, acceptance criteria, validation expectations, handoff audience, and completion signal are present. | Any required field is missing, ambiguous, or contradictory. |
| Write ownership | Deliverables are disjoint or one owner/merge contract is named. | Shared-file parallelism has no owner or contract. |
| Dependency order | Upstream gates and dependencies needed for safe execution are stable. | Downstream work depends on unstable workflow/task-packet contracts or unaccepted blockers. |
| Review ownership | Required reviewer/gate owner roles are named. | Review-only acceptance would be ownerless. |
| Runtime artifact location | Task cards, memos, logs, and iteration artifacts have expected runtime paths or limitations are known. | Material traceability depends on unavailable or unidentified runtime evidence. |
| Source immutability | `raw/` and `research/` are prohibited edit targets. | Task requires modifying immutable source directories. |

### Launch procedure

1. Read the iteration input packet and required canonical sources.
2. Confirm the task can be performed within the MVP1 scope boundary.
3. Check workflow configuration, role/persona references, deliverable paths,
   prohibited edits, dependencies, acceptance criteria, validation expectations,
   and handoff audience.
4. Confirm runtime directories are treated as operational-only:
   `.orchestration/runtime/agent-sync/` for memos and task cards and
   `.orchestration/runtime/iterations/` for iteration artifacts and agent logs.
5. Start or prepare the CLI-assisted workflow using the current orchestration
   framework command conventions for the repository. If command shorthand is
   available in runtime context, follow it; otherwise use the framework
   documented command intent for starting the workflow/phase/iteration.
6. Record the command label, workflow/phase/iteration, source packet, branch/SHA
   when applicable, generated task-card references, and log/runtime references.
7. Dispatch only task packets that pass required-field and ownership checks.
8. Mark incomplete or unsafe packets `draft`, `blocked`, or `needs-spike` and
   assign a recovery owner instead of dispatching them as ready.

## Monitoring and progress checks

MVP1 monitoring is reference-based operational monitoring. It uses available
CLI output, task-card status, runtime memos, validation summaries, branch/SHA
references, and review notes. It does not require or select a telemetry backend.

### Signals to monitor

| Signal | Evidence to check | Action when abnormal |
| --- | --- | --- |
| Workflow/task progress | Task-card state, memo status, command output, runtime/log references. | Route stalled, blocked, or missing-status work to orchestrator or recovery owner. |
| Completion signal | `TASK_COMPLETE`, `TOKEN_BUDGET_LOW`, `BLOCKED`, or `PARTIAL_COMPLETE`. | Reject non-standard signals and request corrected handoff. |
| Validation status | Required-file, section, metadata, trace, source immutability, completion-signal, and future-scope checks. | Mark failed/not-run checks with owner, impact, and revalidation needed. |
| Review gates | Reviewer role, evidence, decision, rationale, affected downstream work, recovery action. | Keep downstream reliance blocked until decision is recorded. |
| Runtime/log references | Command label, path, branch/SHA, memo path, task-card path, validation output. | Record limitation if missing; promote material findings into canonical docs before reliance. |
| Source immutability | Changed-path summary or repository diff. | Stop downstream reliance if `raw/` or `research/` changed and assign recovery review. |
| Process learning | Repeated packet defects, validation gaps, token-budget failures, blocked reviews, or quality issues. | Route to standards, workflow-template, validator, persona, or backlog owner after review. |

### Monitoring cadence

- During active CLI-assisted execution, check progress whenever command output,
  agent memos, or completion signals are produced.
- Before handoff, confirm every deliverable has validation and review status or a
  recorded limitation.
- At iteration close, review blocked/partial states, recurring defects, runtime
  limitations, and open decisions for follow-up ownership.

## Validation procedure

Validation confirms objective readiness and separates review-only judgment. For
each launched workflow, task packet, deliverable, memo, recovery record, or
handoff:

1. Identify applicable deterministic checks:
   - required files;
   - required sections/headings;
   - required metadata and task-packet fields;
   - trace markers and ID format where applicable;
   - contract-field completeness;
   - completion-signal format;
   - source immutability;
   - future-scope guard.
2. Record `target_type`, `target_id`, `check_class`, `criteria`, `status`,
   `evidence`, `run_context`, `follow_up_owner`, and related open
   decision/question IDs when applicable.
3. Label product fit, architecture fit, evidence sufficiency, security/privacy,
   governance, risk, reusable behavior changes, and implementation readiness as
   review-only unless a later standard makes them deterministic.
4. Treat `failed`, required `not-run`, unresolved `review-needed`,
   `request-changes`, `blocked`, and `needs-spike` as readiness blockers for the
   affected scope.
5. Revalidate corrected work before downstream reliance resumes, unless a named
   reviewer approves a documented limitation.

## Handling failed, partial, and blocked tasks

All failures and incomplete states become recovery records with enough context
for another operator, integrator, or agent to continue safely.

| Scenario | Required handling |
| --- | --- |
| Missing source or input packet | Block launch or affected task; name missing source, downstream impact, and source owner. |
| Invalid or incomplete task packet | Keep packet `draft` or `blocked`; correct required fields and revalidate before assignment. |
| Command or task generation failure | Preserve command label/log reference, failure class, affected targets, owner, and rerun conditions. |
| Token budget limit | Use `TOKEN_BUDGET_LOW`; preserve completed output, list remaining paths, and recommend recovery split. |
| Partial output | Use `PARTIAL_COMPLETE`; state completed artifacts, remaining work, downstream limits, and recovery owner. |
| Failed deterministic validation | Record target, failed criterion, evidence, impact, owner, corrective action, and revalidation needed. |
| Review rejection or request changes | Record reviewer role, evidence, rationale, affected downstream work, recovery action, and revised owner. |
| Shared-file conflict | Assign one owner or merge contract; sequence, split, or reconcile work before downstream reliance. |
| Missing reviewer or owner | Keep review-only gate blocked until accountable role is named. |
| Open architecture/governance decision | Mark `blocked` or `needs-spike`; avoid implementation-specific claims. |

Recovery records should include:

| Field | Requirement |
| --- | --- |
| `failure_or_recovery_id` | Stable local label, memo path, validation result, gate, or task-packet reference. |
| `trigger` | Missing source, invalid packet, command failure, token limit, partial output, failed validation, review rejection, conflict, prohibited edit, or open decision. |
| `affected_targets` | Workflow, iteration, task, deliverable, gate, decision, or handoff affected. |
| `current_state` | `blocked`, `partial-complete`, `failed`, `review-needed`, `not-run`, or `needs-spike`. |
| `impact` | What downstream work can proceed and what must wait. |
| `preserved_output` | Useful artifacts, memo context, validation evidence, or runtime references already produced. |
| `recovery_action` | Correct packet, rerun, narrow scope, assign owner, revise artifact, request review, create follow-up, or accept limitation. |
| `owner` | Role accountable for recovery. |
| `validation_needed` | Checks or reviews required before reliance resumes. |

## Source immutability issues

Raw and research files are immutable source inputs for MVP1. They may inform
canonical docs only through reviewed promotion into `docs/` artifacts.

### Prevention

- Include `raw/` and `research/` in prohibited edits for every MVP1 task packet.
- Dispatch work only to exact deliverable paths or output classes.
- Instruct agents to cite canonical docs and approved input packets rather than
  editing source material.
- Treat source promotion as a reviewed documentation change, not direct raw or
  research mutation.

### Detection

- Inspect the repository changed-path summary before handoff.
- Confirm handoffs state whether prohibited files/directories were edited.
- Treat any unreviewed `raw/` or `research/` change as a readiness blocker.

### Recovery

1. Stop downstream reliance on affected output.
2. Identify changed prohibited paths, producing task/agent, and affected
   deliverables.
3. Preserve evidence in a recovery record; do not silently normalize the issue.
4. Assign an integrator or source owner to review whether any useful content
   should be promoted into canonical docs through an approved path.
5. Restore source immutability through an approved remediation path and rerun
   source-immutability validation.
6. Resume downstream reliance only after remediation is reviewed or the
   limitation is explicitly accepted.

## Runtime artifact management

| Artifact class | Expected location or reference | Durability treatment |
| --- | --- | --- |
| Canonical docs | `docs/` | Durable implementation contract. |
| Orchestration configuration | `.orchestration/config/` | Commit-able process configuration when reviewed. |
| Runtime memos and task cards | `.orchestration/runtime/agent-sync/` | Operational-only unless summarized into canonical docs or handoff packages. |
| Iteration logs and generated runtime artifacts | `.orchestration/runtime/iterations/` | Operational-only; preserve references when material. |
| CLI command output | Command label, log, or run context | Operational evidence; summarize material conclusions into durable artifacts. |
| Branch/SHA references | Git branch and commit SHA when applicable | Correlation evidence; not a substitute for canonical summary. |
| Validation results | Validation table, memo, command output, or handoff | Durable when promoted into canonical docs or handoff package; otherwise operational evidence. |

Operational rules:

- Do not treat runtime directories as durable product documentation.
- Do not commit runtime task cards, logs, generated runtime artifacts, or local
  worktrees unless a future canonical rule explicitly changes the policy.
- Capture runtime paths, command labels, branch/SHA, and limitations in handoffs
  when they affect trust, reproducibility, or recovery.
- Promote material runtime-only findings into canonical docs, decisions, work
  items, standards, or handoff packages before downstream implementation relies
  on them.
- If runtime/log references are missing or inaccessible, record the limitation
  and reviewer decision when material.

## Rollback-equivalent actions

MVP1 has no production deployment rollback. Rollback-equivalent operations are
repository and handoff safety actions that prevent unsafe downstream reliance.

| Trigger | Rollback-equivalent action |
| --- | --- |
| Incorrect or unsafe canonical deliverable update | Stop reliance, assign owner, revise the deliverable, rerun validation, and record review decision. |
| Invalid task packet dispatched | Mark task blocked, withdraw or supersede packet, correct required fields, and relaunch only safe scope. |
| Failed or misleading handoff | Publish corrected handoff/memo with status, limitations, validation, owner, and affected downstream work. |
| Runtime-only finding relied on as truth | Promote material finding into canonical docs or mark reliance blocked until reviewed. |
| Prohibited source edit | Stop reliance, identify changed paths, remediate source immutability, and require integrator/source-owner review. |
| Shared artifact conflict | Assign one owner, reconcile changes, preserve useful output, rerun checks, and document merge contract. |
| Future-scope implementation claim | Reclassify as future/open or create a bounded spike; remove implementation commitment from readiness claims. |
| Review rejection | Mark affected scope `request-changes` or `blocked`; revise or defer before downstream reliance. |

When a branch or file change must be undone, preserve evidence and coordinate
with the integrator or owner. Do not discard unrelated user or agent changes.

## Dependency checks

Before launch, before dispatch, and before final handoff, verify:

1. E01 canonical documentation foundation is stable enough for the target work.
2. E02 workflow/task-packet contracts exist before validation or execution work
   depends on them.
3. E03 deterministic validation scope is applied only to objective checks and
   does not imply subjective approval.
4. E04 backlog/readiness gates have explicit dependency and concurrency status
   when implementation planning is affected.
5. E05 execution handoff packages accepted outputs, blockers, recovery paths,
   launch order, and unresolved decisions before downstream implementation.
6. Shared deliverables have one owner or an explicit merge contract.
7. Required reviewers and recovery owners are named.
8. Future runtime, event, storage, telemetry, approval, provider, tenancy,
   compliance, UI, and legacy decisions remain open/future unless accepted by a
   later canonical decision.

Unsafe sequencing blocks readiness until corrected, narrowed to discovery, or
accepted as a documented limitation by the proper reviewer.

## Incident and escalation procedure

MVP1 incidents are operational conditions that can mislead downstream work,
damage source immutability, hide blockers, or compromise handoff readiness.

| Severity | Examples | Immediate action | Escalation owner |
| --- | --- | --- | --- |
| SEV-1 readiness integrity | Prohibited `raw/`/`research/` edit, unsafe implementation claim treated as accepted, missing owner for release-blocking gate, corrupted canonical handoff. | Stop downstream reliance, create recovery record, notify integrator/orchestrator, assign owner. | Integrator plus affected gate owner. |
| SEV-2 execution blocker | Missing source packet, invalid task cards, failed validation without recovery, shared-file conflict, review rejection blocking launch. | Mark affected work blocked, preserve output, assign recovery owner, rerun or revise after fix. | Orchestrator or validator owner. |
| SEV-3 operational degradation | Missing runtime/log reference, token-budget split, partial completion, unclear memo status, repeated packet defect. | Record limitation, preserve useful output, create follow-up, route process learning if recurring. | Orchestrator or recovery owner. |

Escalation records must state affected workflow/phase/iteration, affected
deliverables, impact, owner, recovery action, validation/review needed, and what
downstream work must wait.

## Readiness handoff

An MVP1 release-operations handoff is ready only when it includes:

1. Accepted scope statement and future-scope exclusions.
2. Workflow/phase/iteration and source-packet references.
3. Launch sequence, dependency order, and unsafe sequencing notes.
4. Changed deliverables and runtime references where material.
5. Validation matrix with applicable checks `passed`, `approved`, or
   `not-applicable` with rationale; all other statuses have recovery owners.
6. Review-only decisions with reviewer role, evidence, rationale, downstream
   effect, and recovery action.
7. Source-immutability confirmation for `raw/` and `research/`.
8. Completion signal for each role output.
9. Blockers, partial outputs, accepted limitations, recovery paths, and work
   that must not proceed.
10. Ownership for orchestrator, integrator, validator owner, reviewer/gate
    owners, recovery owners, and downstream consumers.
11. Process learnings routed to standards, workflow templates, validators,
    personas, work items, or future backlog owners when applicable.

### Handoff template

| Field | Required content |
| --- | --- |
| Handoff status | `ready-to-consume`, `ready-to-merge`, `blocked`, or `partial-complete`. |
| Workflow context | Workflow, phase, iteration, source packet, task packet(s), branch/SHA when applicable. |
| Changed artifacts | Canonical deliverables created or updated. |
| Runtime references | Memo paths, task-card paths, logs, command labels, validation outputs, or limitations. |
| Validation summary | Checks performed/not performed, evidence, status, and follow-up owner. |
| Review summary | Reviewer roles, decisions, rationale, affected downstream work, recovery action. |
| Source immutability | Confirmation that `raw/` and `research/` were not edited, or violation recovery record. |
| Dependencies | Upstream dependencies satisfied, downstream work allowed, downstream work blocked. |
| Risks and blockers | Open decisions, assumptions, partial work, needs-spike items, accepted limitations. |
| Completion signal | One standard signal and required detail. |
| Follow-up owners | Named role for each unresolved item. |

## Readiness record

Use this record when deciding whether an MVP1 operational handoff or release
operation is ready for downstream implementation planning.

| Gate | Status | Evidence / rationale | Owner | Follow-up |
| --- | --- | --- | --- | --- |
| Scope boundary and future-scope exclusions |  |  |  |  |
| Launch inputs and workflow context |  |  |  |  |
| Task-packet completeness |  |  |  |  |
| Dependency and concurrency safety |  |  |  |  |
| Deterministic validation |  |  |  |  |
| Review-only quality |  |  |  |  |
| Runtime artifact references |  |  |  |  |
| Source immutability |  |  |  |  |
| Failure/recovery coverage |  |  |  |  |
| Ownership and escalation |  |  |  |  |
| Readiness handoff |  |  |  |  |

## Assumptions

- The existing orchestration framework and Cursor/agent CLI-assisted workflow
  are sufficient for MVP1 release operations.
- Markdown-first task packets, validation records, review gates, and handoffs
  are sufficient until later validator work proves a schema need.
- Runtime artifacts are operational evidence; durable conclusions belong in
  canonical docs or handoff packages.
- Human reviewers remain accountable for review-only readiness, risk,
  governance, security/privacy, and implementation-readiness decisions.

## Open decisions

| ID | Decision needed | Current MVP1 handling |
| --- | --- | --- |
| OQ-OPS-001 | Which validator checks should run in CLI, CI, task generation, or integrator review? | Define objective check behavior here; defer tooling placement to implementation planning. |
| OQ-OPS-002 | Who are the named accountable approvers for each release/readiness gate family? | Use role-based owners until named individuals or teams are accepted. |
| OQ-OPS-003 | What runtime/log references must be retained, summarized, or discarded after orchestration runs? | Summarize material findings into canonical docs or handoff packages; leave retention policy open. |
| OQ-OPS-004 | What concrete retry, dead-letter, replay, telemetry, approval, storage, and event mechanisms are needed for future runtime operations? | Treat as future/open; MVP1 records conceptual recovery, ownership, and correlation only. |
| OQ-OPS-005 | What deployment, rollback, access-control, tenancy, compliance, provider, UI, or legacy-adapter operations apply after MVP1? | Treat as future/open and block implementation-specific claims until accepted decisions exist. |
