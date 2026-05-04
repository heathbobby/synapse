# MVP1 Platform Infrastructure

- **Status**: draft MVP1 domain infrastructure
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-01-domain-infrastructure`
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

This document defines the infrastructure boundaries for MVP1. In this iteration,
infrastructure means the repository, canonical documentation, orchestration
configuration, CLI-assisted workflow mechanics, task packets, memos, validation
scope, and handoff conventions needed to run the first Synapse
concept-to-implementation domain. It does not define production runtime
infrastructure for the future Synapse product.

## Source register

| Source | Infrastructure use |
| --- | --- |
| `docs/MVP1/Platform/Overview.md` | MVP1 domain boundary, in-scope areas, deferred areas, and downstream readiness criteria. |
| `docs/architecture/ARCHITECTURE.md` | Canonical truth principle, logical component concepts, data/state concepts, assumptions, and open decisions. |
| `docs/architecture/TECHNICAL_SPECIFICATIONS.md` | Technology-neutral task dispatch, conceptual contracts, event-family expectations, and non-functional requirements. |
| `docs/architecture/DECISIONS.md` | ADR-0011 through ADR-0014: CLI-assisted MVP1, orchestration-framework domain, Markdown-first metadata, and initial validator scope. |
| `docs/planning/EXECUTION_ORCHESTRATION.md` | G1/G2 gates, MVP1 launch order, recovery paths, and deferred work. |
| `docs/planning/CONCURRENCY_ANALYSIS.md` | Safe parallelism, unsafe sequencing, artifact ownership rules, and conflict recovery. |
| `docs/work_items/INDEX.md` | E01-E05 MVP1 epic and story scope. |
| `docs/work_items/DEPENDENCY_MAP.md` | Dependency order, blockers, safe parallelism, and gate alignment. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Required task-packet inputs, role boundaries, evidence discipline, validation, and completion signals. |

## Infrastructure principles

1. **Repository-first execution**: MVP1 runs through repository artifacts,
   orchestration configuration, CLI workflows, task packets, and memos.
2. **Canonical docs as infrastructure**: canonical `docs/` files are treated as
   operating infrastructure because they define source truth, contracts,
   readiness gates, and downstream handoff state.
3. **Technology-neutral contracts**: MVP1 infrastructure describes required
   fields, states, gates, and validation behavior without selecting storage,
   event transport, runtime, tenancy, provider, or deployment technology.
4. **Bounded agent work**: every role-agent task needs explicit sources,
   deliverables, prohibited edits, dependencies, acceptance criteria, validation
   expectations, and handoff audience.
5. **Validation before handoff**: deterministic checks and review checks must be
   recorded before downstream work treats a deliverable as ready.

## MVP1 infrastructure components

| Component | MVP1 responsibility | Not an MVP1 commitment |
| --- | --- | --- |
| Canonical documentation repository | Store implementation-ready requirements, architecture, planning, standards, work items, MVP1 platform docs, assumptions, and open decisions. | A runtime knowledge store or retrieval service. |
| Orchestration configuration | Define workflow and persona configuration used by the existing orchestration framework. | A product workflow-definition service. |
| CLI orchestration entrypoint | Support CLI-assisted workflow launch and task-card generation for the internal orchestration-framework domain. | A hosted workflow execution runtime or API. |
| Workflow/task packets | Encode phase, iteration, role, sources, deliverables, dependencies, prohibited edits, acceptance criteria, validation expectations, and handoff audience. | A persisted workflow graph schema for production runtime. |
| Runtime memos | Coordinate multi-agent handoffs, blockers, ready-to-consume outputs, and integrator context during framework runs. | Durable product messaging, notification, or audit infrastructure. |
| Deterministic validators | Check MVP1 artifact presence, required sections/headings, trace/ID format, source immutability, and completion-signal format. | Full quality automation, event replay, compliance validation, or runtime monitoring. |
| Backlog and dependency maps | Sequence E01-E05, identify blockers, define readiness gates, and prevent unsafe parallelism. | A product project-management backend. |
| Handoff package | Package accepted contracts, validation results, recovery paths, launch order, and unresolved blockers. | A release pipeline or deployment system. |

## Canonical paths

| Path family | MVP1 use |
| --- | --- |
| `docs/architecture/` | Architecture boundaries, technology-neutral specifications, accepted decisions, and open decisions. |
| `docs/planning/` | Execution orchestration, concurrency guidance, gates, and recovery paths. |
| `docs/requirements/` | Product and functional trace sources for backlog and workflow contracts. |
| `docs/standards/` | Agent, engineering, event, and quality standards used by task packets and review gates. |
| `docs/work_items/` | E01-E05 MVP1 epics/stories, dependency map, readiness gates, blockers, and implementation order. |
| `docs/refinement/iteration-inputs/` | Reviewed input packets that bound agent work. |
| `docs/MVP1/Platform/` | MVP1 platform overview and infrastructure artifacts. |
| `.orchestration/config/` | Commit-able orchestration framework configuration. |
| `.orchestration/runtime/` | Runtime task cards, memos, and agent logs; operational artifacts, not durable product docs. |

Raw and research inputs are immutable source material. MVP1 infrastructure may
reference canonical docs that promote material from those inputs, but task
packets and implementation handoffs should not treat raw or research files as
the direct contract.

## Workflow and task-packet infrastructure

MVP1 workflow definitions should capture:

- workflow name, phase, iteration, and domain;
- accepted upstream decisions and gate status;
- canonical source references;
- role assignments and role boundaries;
- deliverable paths and write-target ownership;
- dependencies and unsafe parallelism notes;
- completion criteria;
- validation expectations; and
- handoff audience.

MVP1 task packets should include the required inputs from
`docs/standards/AI_AGENT_STANDARDS.md`: role/objective, canonical sources,
deliverables, prohibited edits, dependencies, acceptance criteria, validation
expectations, and handoff audience. They should also preserve MVP1-specific
scope exclusions so agents do not accidentally implement future product
behavior.

## Validation infrastructure

Initial MVP1 validators are bounded to the scope accepted in ADR-0014:

| Check class | MVP1 target |
| --- | --- |
| Required files | Confirm expected canonical deliverables exist. |
| Required sections/headings | Confirm deliverables expose sections needed for review and downstream handoff. |
| Trace markers | Confirm PRD/FR, E##, and US-E##-### references where applicable. |
| ID format | Confirm work-item IDs use the accepted Markdown-first conventions. |
| Source immutability | Confirm `raw/` and `research/` were not modified by MVP1 tasks. |
| Completion signal format | Confirm agent handoffs use `TASK_COMPLETE`, `TOKEN_BUDGET_LOW`, `BLOCKED`, or `PARTIAL_COMPLETE` as defined by standards. |

Review-only criteria should remain labeled when they cannot be checked
deterministically. Examples include whether an assumption is sufficiently
evidence-backed, whether a risk needs security/privacy review, and whether an
open decision blocks implementation.

## State and event posture

MVP1 may use architecture concepts such as workflow states, task status,
completion signals, event families, audit records, and approval decisions as
reference language. It does not implement the production runtime state machine
or hybrid event bus. For MVP1:

- workflow/task state is represented in task packets, generated artifacts,
  memos, validation outputs, and handoff summaries;
- event-family concepts remain technology-neutral guidance for future
  contracts;
- auditability is provided by committed canonical docs plus runtime memos/logs
  where available; and
- approval semantics are represented as readiness/review gates, not automated
  approval services.

## Concurrency and ownership

MVP1 infrastructure supports parallel work only when upstream context is stable,
write targets are disjoint or explicitly owned, and validation/review gates are
defined. The unsafe patterns from the dependency map remain binding:

- do not run E03 before E02 task-packet contracts stabilize;
- do not package E05 before E02-E04 validate;
- do not run shared-file parallel edits without a single owner;
- do not convert open stack, storage, event, tenancy, compliance, UI, provider,
  or legacy-adapter questions into implementation claims; and
- do not modify `raw/` or `research/`.

When conflicts or partial completions occur, the recovery path is to preserve
the useful output, record the blocker or partial state, assign one owner for
shared artifacts, and create a bounded follow-up or recovery task.

## Security, privacy, and governance posture

MVP1 has no accepted tenancy, compliance, retention, provider, or access-control
model beyond repository and agent-task boundaries. Therefore:

- sensitive-data, compliance, tenancy, and retention requirements remain open;
- task packets must state prohibited edits and tool boundaries;
- future behavior-affecting changes to standards, workflow templates, personas,
  or validation expectations require review before promotion; and
- human reviewers remain accountable for accepting readiness gates and resolving
  open decisions.

## Deferred infrastructure

| Future area | Reason deferred |
| --- | --- |
| Runtime-backed workflow service | MVP1 is CLI-assisted; production runtime and persistence are open architecture decisions. |
| Visual designer UI and graph format | MVP1 uses Markdown and CLI task packets; visual template representation remains open. |
| Concrete storage and knowledge retrieval | Source inventory, confidence, freshness, tenancy, retention, and retrieval needs are not yet accepted. |
| Concrete event transport or schema registry | Event contract standards exist, but throughput, latency, replay, deployment, and compliance constraints are open. |
| Agent runtime provider integration | MVP1 uses existing CLI-assisted agents and role packets; provider strategy remains open. |
| Human approval automation | MVP1 uses review/readiness gates; approval policy and automation are future MVP3 work. |
| Legacy adapters | No customer/domain/corpus or adapter boundary is validated for MVP1. |

## Assumptions

- The existing orchestration framework can provide enough CLI-assisted execution
  mechanics for MVP1 workflow/task-packet refinement.
- Markdown-first metadata is reviewable and sufficient for initial validators.
- Runtime memos are adequate for MVP1 handoff coordination, while durable product
  audit infrastructure remains future scope.
- E01-E05 sequencing in the work-item index and dependency map is the controlling
  order for downstream MVP1 infrastructure work.

## Open decisions

| Decision | Current MVP1 handling |
| --- | --- |
| Workflow runtime and state persistence | Open; do not select or imply a runtime in MVP1 infrastructure. |
| Event transport, schema format, and registry | Open; use event standards as future contract guidance only. |
| Storage for workflow state, audit, knowledge assets, personas, and telemetry | Open; keep data models conceptual. |
| Tenancy, access control, sensitive data handling, compliance, and retention | Open; block implementation-specific claims. |
| Human approval policy model | Future; represent current review needs as readiness gates. |
| Visual workflow template representation | Future/open; use Markdown/CLI task-packet definitions for MVP1. |
| Legacy adapter scope | Future/open; validate a concrete legacy scenario before adapter work. |

## Downstream handoff criteria

Downstream MVP1 iterations can consume this infrastructure document when they:

- keep work bounded to CLI-assisted orchestration over the orchestration
  framework domain;
- define deliverables and write targets explicitly;
- mark runtime, UI, storage, event, tenancy, provider, compliance, and legacy
  adapter choices as open or future unless a later accepted decision changes
  them;
- use the standard task-packet inputs and completion signals; and
- record deterministic validation, review-only validation, assumptions, blockers,
  and recovery needs in the handoff.
