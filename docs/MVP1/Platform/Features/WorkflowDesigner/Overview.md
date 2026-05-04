# Workflow Designer Feature Overview

- **Status**: draft MVP1 feature specification
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-04-feature-specifications`
- **Feature area**: WorkflowDesigner
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

Workflow Designer defines the MVP1 product experience for creating and refining
Synapse workflow definitions and role-agent task packets. Despite the feature
name, MVP1 does not include a visual canvas, hosted runtime, or production
workflow execution service. The MVP1 experience is CLI-assisted and
Markdown-first: operators use canonical docs, workflow configuration, input
packets, task cards, runtime memos, and validation/review gates to make
orchestration work explicit, bounded, traceable, and safe for downstream handoff.

## Source register

| Source | How this feature overview uses it |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp1-iteration-04-feature-specifications.md` | Feature-specification goal, product-owner source references, MVP1 scope guardrails, and completion criteria. |
| `docs/work_items/INDEX.md` | MVP1 epic/story scope, especially E02 Workflow Definition and Task-Packet Model, E03 validation, E04 readiness, and E05 handoff dependencies. |
| `docs/work_items/DEPENDENCY_MAP.md` | Sequencing rules, G1/G2 gates, resolved MVP1 decisions, blockers, safe parallelism, and unsafe future-scope claims. |
| `docs/MVP1/Platform/Overview.md` | MVP1 platform thesis, repository-first boundary, in-scope/deferred areas, and downstream readiness expectations. |
| `docs/MVP1/Platform/Infrastructure.md` | CLI-assisted infrastructure components, workflow/task-packet required fields, validation scope, and source immutability rule. |
| `docs/MVP1/Platform/Integrations.md` | Command/document integration contracts, participant ownership, validation/review flows, telemetry references, and recovery behavior. |
| `docs/MVP1/Platform/BusinessEntities.md` | Conceptual entities, ownership, lifecycle states, invariants, and readiness gate responsibilities. |
| `docs/MVP1/Platform/DataModel.md` | Logical fields, identifier conventions, relationship model, data quality rules, and retention/audit posture. |
| `docs/requirements/PRODUCT_REQUIREMENTS.md` | Product vision, target personas, PRD-003, PRD-005, PRD-006 conceptual review visibility, PRD-008 backlog traceability, and MVP framing. |

## Product value

Workflow Designer helps Synapse users turn an ambiguous concept-to-implementation
initiative into a reviewable orchestration contract. For MVP1, value comes from:

1. **Repeatable orchestration**: workflows expose phase, iteration, role, source,
   deliverable, dependency, validation, and handoff expectations before agents
   start work. This supports PRD-003 and PRD-005.
2. **Bounded agent execution**: task packets give specialized agents enough
   context to produce useful deliverables without editing prohibited sources,
   inventing future-scope behavior, or leaving handoff status implicit.
3. **Traceable readiness**: workflow outputs connect to PRD/FR trace, E## and
   US-E##-### work items, validation evidence, review-only gates, assumptions,
   risks, blockers, and recovery actions.
4. **Human-operable control**: orchestrators, reviewers, and integrators can see
   where decisions are missing, which work is safe to run in parallel, and which
   outputs are ready-to-consume, blocked, or partial.
5. **Future-proof contract foundation**: the Markdown-first contracts define the
   semantics a later visual designer or runtime service would need without
   prematurely choosing UI, storage, event, provider, tenancy, or compliance
   technology.

## Personas and jobs

| Persona | Primary job in MVP1 | Needs from Workflow Designer |
| --- | --- | --- |
| Human operator / orchestrator | Start a bounded concept-to-implementation iteration and generate role-agent work. | A workflow definition with phase/iteration metadata, role bindings, sources, deliverables, dependencies, validation expectations, and launch criteria. |
| Specialist role agent | Execute one scoped assignment and produce or update canonical deliverables. | A complete task packet with objective, canonical sources, prohibited edits, allowed write targets, acceptance criteria, validation expectations, and handoff audience. |
| Integrator | Reconcile completed, partial, or blocked outputs into downstream-safe handoff context. | Stable identifiers, memo/handoff references, changed artifacts, validation status, open questions, and shared-write ownership rules. |
| Reviewer / gate owner | Accept, reject, request changes, defer, or escalate review-only criteria. | Evidence, rationale, validation result summaries, affected downstream work, and recovery actions for product, architecture, quality, dependency, risk, security/privacy, and implementation gates. |
| Validator owner | Define or run deterministic checks that can be trusted before downstream reliance. | Required-file, section, trace-marker, ID-format, source-immutability, and completion-signal expectations from workflow and task-packet contracts. |
| Product/strategy stakeholder | Understand whether the workflow supports the initiative's value, scope, and readiness. | Clear in-scope/out-of-scope boundaries, PRD/work-item trace, risks, assumptions, and open decisions. |

## In-scope MVP1 capabilities

### WF-DES-001: Workflow definition authoring contract

MVP1 must define workflow authoring as a Markdown/configuration contract that
captures:

- `workflow_id`, phase IDs, iteration IDs, and domain scope;
- accepted upstream decisions and gate status;
- canonical source references and approved input packets;
- role/persona bindings and reviewer expectations;
- deliverable paths and write-target ownership;
- dependencies, blockers, and unsafe parallelism notes;
- completion criteria and handoff audience; and
- deterministic and review-only validation expectations.

### WF-DES-002: Role-agent task-packet authoring contract

MVP1 must define task packets as executable work contracts. A ready task packet
includes:

- task or packet identifier and parent workflow/iteration;
- assigned role/persona and objective;
- canonical sources and evidence expectations;
- exact deliverables and allowed write targets;
- prohibited edits, including `raw/` and `research/`;
- dependencies, shared-artifact coordination, and blockers;
- acceptance criteria and validation expectations;
- handoff audience and expected completion signal; and
- explicit scope exclusions for visual/runtime/product infrastructure work.

### WF-DES-003: CLI-assisted workflow launch and task generation semantics

MVP1 supports command-and-document boundaries rather than product APIs. The
feature should make it clear how a workflow start intent consumes configuration
and an iteration input packet, then produces generated task cards or equivalent
role packets with sufficient metadata for safe assignment.

### WF-DES-004: Dependency and write-target coordination

Workflow Designer must require explicit dependencies and write-target ownership.
Parallel work is safe only when upstream context is stable and target files are
disjoint or one owner/merge contract is named. Shared requirements, architecture,
backlog, standards, or feature-spec artifacts must not be edited in parallel
without a single convergence owner.

### WF-DES-005: Handoff, memo, and completion-state expectations

The feature must preserve completion status through standard signals and runtime
handoff context:

- `TASK_COMPLETE`
- `PARTIAL_COMPLETE`
- `BLOCKED`
- `TOKEN_BUDGET_LOW`

Ready-to-consume memos and handoff summaries should identify changed artifacts,
validation performed/not performed, assumptions, open questions, blockers,
runtime/log references where material, follow-up owner, and downstream safety.

### WF-DES-006: Validation and readiness support

Workflow Designer must expose the validation hooks accepted for MVP1:

- required deliverable files exist or are marked blocked/partial;
- required sections/headings are present;
- PRD/FR, E##, and US-E##-### trace markers appear where applicable;
- local ID formats are stable enough for Markdown cross-reference;
- `raw/` and `research/` remain unmodified; and
- completion-signal format is valid.

Review-only quality, evidence sufficiency, risk acceptance, architecture fit,
security/privacy impact, and open-decision impact must name reviewer roles and
limitations rather than pretending to be deterministic.

### WF-DES-007: Backlog and handoff traceability

MVP1 workflow and task-packet authoring must connect to E02, E03, E04, and E05:

- E02 defines workflow phases, iteration metadata, task-packet structure, and
  coordination rules.
- E03 consumes stable E02 contracts to define deterministic validation and
  completion signals.
- E04 uses workflow/task-packet metadata to keep backlog readiness gates,
  dependency notes, risks, and acceptance-quality criteria consistent.
- E05 packages accepted workflow, validation, backlog, recovery, and blocker
  context into the implementation handoff.

## Out of scope and future work

The following are explicitly outside MVP1, even though the feature name may imply
them:

| Future area | MVP1 disposition |
| --- | --- |
| Visual workflow designer UI or canvas | Future. MVP1 authoring is Markdown/configuration plus CLI-assisted task generation. |
| Graph serialization, diffing, template publication UI, or drag-and-drop modeling | Future/open. MVP1 only names logical workflow/task relationships. |
| Hosted workflow execution runtime, scheduler, retry engine, pause/resume service, or API | Future/open. MVP1 uses repository-first CLI orchestration. |
| Persisted workflow-run database, state store, schema registry, or migration strategy | Future/open. MVP1 defines logical records only. |
| Concrete event transport, event serialization, replay, dead-letter handling, or telemetry backend | Future/open. MVP1 may use conceptual event families and runtime references only. |
| Human approval automation, queues, policy engine, or approval ledger | Future. MVP1 records review gates and reviewer accountability. |
| Persona registry service, prompt-management runtime, provider-specific agent runtime integration | Future. MVP1 uses role/persona references in task packets and config. |
| Knowledge retrieval store, source inventory service, SME freshness scoring, or confidence-scoring implementation | Future. MVP1 uses canonical docs and approved input packets. |
| Tenancy, access control, sensitive-data handling, compliance controls, retention, deletion, or deployment model | Open governance/architecture decisions. Do not encode implementation-specific claims. |
| Legacy bridge adapters, customer corpus, permissions, rate limits, or transition-state runtime | MVP4/future after concrete legacy scenario validation. |

## User scenarios

### Scenario 1: Author a launch-ready MVP1 workflow definition

**Given** the canonical docs and accepted MVP1 decisions are available, **when**
an orchestrator prepares a concept-to-implementation iteration, **then** the
workflow definition names the workflow/phase/iteration, domain scope, roles,
sources, deliverables, dependencies, launch gates, completion criteria,
validation expectations, prohibited future-scope claims, and handoff audience.

**Alternate path**: If sources, roles, write targets, or dependencies are unclear,
the workflow remains `draft` or `blocked` and records the recovery owner.

### Scenario 2: Generate a bounded task packet for a specialist role

**Given** a ready workflow definition and iteration input packet, **when** task
generation occurs, **then** each role receives a packet with objective, sources,
deliverables, prohibited edits, dependencies, acceptance criteria, validation
expectations, completion signal, and handoff audience.

**Error path**: If a generated task packet lacks required fields or has ambiguous
write targets, it must not be treated as assignable until corrected or narrowed.

### Scenario 3: Execute and hand off role-agent work

**Given** a specialist agent has a ready task packet, **when** the agent updates a
deliverable, **then** the handoff identifies changed artifacts, assumptions/open
questions, validation performed/not performed, prohibited-edit confirmation,
completion signal, and downstream audience.

**Partial path**: If token budget, missing inputs, or unresolved decisions prevent
completion, the agent emits `PARTIAL_COMPLETE`, `TOKEN_BUDGET_LOW`, or `BLOCKED`
with preserved output and recovery guidance.

### Scenario 4: Validate workflow and task-packet outputs

**Given** workflow/task-packet deliverables and handoffs exist, **when** validation
is run or reviewed, **then** required files, headings, trace markers, ID format,
source immutability, and completion signals are recorded as passed, failed,
not-run, review-needed, or not-applicable with evidence and follow-up owner.

**Review path**: Criteria such as product fit, risk acceptance, architecture
fitness, security/privacy impact, and implementation readiness require named
reviewer roles and rationale.

### Scenario 5: Prevent unsafe future-scope implementation

**Given** a task or feature spec mentions visual designer, runtime, storage,
events, approvals, telemetry, providers, tenancy, compliance, or legacy adapters,
**when** the claim is not backed by an accepted MVP1 decision, **then** Workflow
Designer marks it future/open, reframes the task as technology-neutral contract
definition, or creates a bounded spike/open question.

## Integration points

| Integration point | Producer | Consumer | MVP1 contract |
| --- | --- | --- | --- |
| Workflow configuration to iteration input packet | Orchestrator / configuration owner | Task generator, specialist agents, validators, reviewers | Required metadata, role bindings, source references, deliverables, dependencies, completion criteria, validation expectations. |
| Input packet to generated task card | Orchestrator / task generator | Specialist agent, reviewer, validator, integrator | Task packet includes objective, sources, allowed deliverables, prohibited edits, dependencies, acceptance criteria, validation, handoff audience, completion signal. |
| Agent execution to deliverable and memo | Specialist agent / reviewer | Integrator, downstream agents, validators | Changed artifacts, assumptions/open questions, validation summary, completion signal, runtime references, follow-up owner. |
| Validation result flow | Validator owner / agent / reviewer | Integrator, gate owners, recovery owner | Target, check class, criteria, status, evidence, run context, limitation, follow-up owner. |
| Human review/readiness gate | Reviewer / integrator | Orchestrator, downstream owners | Gate family, evidence reviewed, decision, rationale, affected downstream work, recovery action. |
| Telemetry/log reference flow | CLI, agents, validators, reviewers | Integrator, future observability owners | Runtime path, command label, branch/SHA, summary, durability, limitations; material findings promoted to canonical docs. |
| Recovery flow | Any participant detecting failure/partial/blocker | Orchestrator, integrator, follow-up owner | Trigger, affected targets, preserved output, current state, owner, recovery action, validation needed. |

## Acceptance expectations

Workflow Designer is acceptable for MVP1 when the feature and its downstream
work products satisfy the following:

| Gate | Acceptance expectation |
| --- | --- |
| Product | Personas, user value, MVP scope, assumptions, open questions, and excluded future visual/runtime work are explicit. |
| Requirements traceability | PRD-003, PRD-005, PRD-008, related E02-E05 work items, and future PRD-006 concepts are cited where relevant. |
| Architecture/technical | The feature remains repository-first, CLI-assisted, Markdown-first, and technology-neutral; runtime, UI, storage, event, API, provider, tenancy, compliance, and legacy choices stay future/open. |
| Workflow/task-packet quality | Required workflow and task-packet fields are defined and inspectable before assignment or downstream reliance. |
| Dependency/concurrency | Upstream dependencies, safe parallelism, unsafe sequencing, shared write targets, and handoff owners are recorded. |
| Validation | Deterministic checks cover file presence, sections/headings, trace markers, ID format, source immutability, and completion signals where applicable; review-only checks are labeled. |
| Handoff readiness | Completion state, changed artifacts, validation summary, assumptions/open questions, risks, blockers, follow-up owners, and recovery paths are explicit. |
| Source immutability | `raw/` and `research/` remain unmodified by MVP1 feature work. |

## Risks and mitigations

| Risk | Impact | MVP1 mitigation |
| --- | --- | --- |
| Feature name leads stakeholders to expect a visual UI. | Scope creep and premature UX/runtime commitments. | State repeatedly that MVP1 is CLI-assisted workflow/task-packet authoring; keep visual designer work future/open. |
| Markdown-first contracts become inconsistent across workflow, task packets, backlog, and validation docs. | Validators and handoffs may fail or drift. | Use required sections/tables, stable IDs, PRD/FR and E##/US-E##-### trace, and integrator review. |
| Generated task packets omit dependencies, prohibited edits, validation, or handoff audience. | Agents may produce unsafe, unreviewable, or incomplete output. | Treat incomplete packets as `draft`/`blocked`; require correction before assignment. |
| Parallel agents edit shared artifacts without ownership. | Merge conflicts and contradictory canonical truth. | Require disjoint write targets or one named owner/merge contract before parallel execution. |
| Runtime memos/logs are treated as durable truth. | Downstream work may rely on operational-only context. | Promote material facts to canonical docs, work items, decisions, or handoff packages before reliance. |
| Deterministic validation is overclaimed. | Subjective quality, risk, or architecture issues may be missed. | Label review-only criteria and assign reviewer roles. |
| Open runtime, storage, event, tenancy, compliance, provider, or legacy decisions leak into implementation claims. | Rework and false commitments. | Mark unsupported specifics as future/open or create bounded decision spikes. |

## Open questions and decisions

| ID | Question or decision needed | Current MVP1 handling |
| --- | --- | --- |
| OQ-WFD-001 | Which workflow/task-packet fields must become machine-readable for E03 validators? | Keep Markdown-first contracts until a bounded validator spike proves schema extraction is needed. |
| OQ-WFD-002 | Who is the final accountable approver for each readiness gate family? | Use role-based gate ownership from platform docs until named approvers are accepted. |
| OQ-WFD-003 | Which CLI command intents should become stable product APIs after MVP1? | Treat current command boundaries as conceptual and repository-first; defer API/runtime choices. |
| OQ-WFD-004 | What visual designer concepts, if any, should map to the MVP1 workflow/task-packet model? | Defer visual representation until MVP1 contracts are validated. |
| OQ-WFD-005 | What runtime telemetry/log evidence should be retained or summarized after orchestration runs? | Summarize material findings into canonical docs or handoff packages; leave retention policy open. |
| OQ-WFD-006 | What approval policy, autonomy thresholds, security/privacy gates, and compliance controls apply to future workflow execution? | Keep human review as readiness gates; block implementation-specific governance claims. |
| OQ-WFD-007 | Which external systems, source types, provider runtimes, or legacy adapters become future integration targets? | Keep external/product/legacy integration future/open until a concrete domain is selected. |

## Assumptions

- The existing orchestration framework and `orchestration-framework/cli.py` are
  sufficient for MVP1 CLI-assisted workflow definition and task generation.
- The orchestration-framework domain remains the first MVP1 initiative for
  workflow/task-packet modeling.
- Markdown-first structured sections and tables are sufficient for review and
  initial validation until E03 identifies a concrete schema need.
- Human review remains accountable for accepting product fit, evidence
  sufficiency, architecture fit, risks, governance concerns, and unresolved
  decision impact.
- Workflow Designer's MVP1 output is a product and execution contract for later
  implementation handoff, not a shipped end-user visual design surface.
