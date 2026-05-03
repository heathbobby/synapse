# Synapse MVP1 Implementation Roadmap

- **Status**: draft MVP1 implementation-readiness roadmap
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp1-iteration-06-release-operations`
- **Domain**: orchestration-framework / CLI-assisted concept-to-implementation
- **Last updated**: 2026-05-03

## Purpose

This roadmap synthesizes MVP1 readiness for implementation planning. MVP1 is a
repository-first, CLI-assisted concept-to-implementation pipeline over the
existing orchestration framework. Implementation readiness means canonical docs,
workflow/task-packet contracts, deterministic validation scope, review-only
gates, backlog sequencing, recovery behavior, and release handoff are explicit
enough for CLI-assisted orchestration work to proceed safely.

This roadmap does not authorize a hosted Synapse runtime, visual designer UI,
workflow-run database, product API, event bus, schema registry, telemetry
backend, approval automation, provider runtime, tenancy model, compliance
implementation, deployment system, or legacy adapter.

## MVP1 readiness summary

| Area | Readiness | What is ready | What must happen next |
| --- | --- | --- | --- |
| Canonical documentation foundation | Refined / ready for review | Canonical doc paths, source immutability, uncertainty discipline, quality criteria, and work-item trace are documented. | Final G0/integrator review before dependent implementation treats E01 as accepted. |
| Workflow/task-packet model | Ready candidate | Workflow Designer and Create Workflow define phase, iteration, role, source, deliverable, dependency, validation, completion, and handoff fields. | Reconcile any field drift across workflow config, input packets, generated task cards, and backlog metadata. |
| Deterministic validation | Draft specification | Required files, sections/headings, trace markers, ID format, source immutability, completion signals, and contract-field checks are defined. | Decide validator placement and whether any fields need machine-readable extraction. |
| Backlog readiness | Draft specification | E01-E05 stories, readiness labels, gates, dependencies, blockers, and safe/unsafe sequencing are documented. | Align E04 readiness metadata with final E02 task-packet fields and assign gate reviewers. |
| Release operations and handoff | Draft handoff package | Runbook, acceptance criteria, release notes, and this roadmap define launch, monitoring, validation, recovery, incident, and handoff expectations. | Package E05 only after E02-E04 validation/review states are recorded or accepted as limitations. |

## MVP1 implementation sequence

### E01 - Canonical Documentation Foundation

| Item | Guidance |
| --- | --- |
| Readiness | `Refined`; implementation or finalization can proceed first if G0 evidence is missing. |
| Primary owner | Integrator with product/documentation reviewer support. |
| Supporting owners | Standards owner, validator owner, source/governance reviewer. |
| Depends on | No upstream MVP1 epic dependency. |
| Unlocks | E02, E03, E04, E05, and future E06/E12 work. |
| Required outputs | Canonical documentation registry, source attribution and uncertainty labels, raw/research immutability rule, open-question/validation-need register, acceptance-quality criteria. |
| CLI-assisted orchestration step | Start with canonical source review and changed-path/source-immutability checks before dispatching downstream task packets. |
| Blockers / watch items | Named approval owners remain role-based; any `raw/` or `research/` mutation blocks readiness. |

### E02 - Workflow Definition and Task-Packet Model

| Item | Guidance |
| --- | --- |
| Readiness | `Ready candidate`; should proceed after E01 review and accepted G1 scope/mode decisions. |
| Primary owner | Orchestrator / configuration owner. |
| Supporting owners | Integrator, tech lead/architect, standards owner, reviewer/gate owner. |
| Depends on | E01; ADR-0011 CLI-assisted MVP1; ADR-0012 orchestration-framework domain; ADR-0013 Markdown-first metadata. |
| Unlocks | E03 validation/completion work and E05 handoff; informs E04 readiness fields. |
| Required outputs | Workflow phase/iteration metadata, role-agent task-packet structure, dependency and write-target coordination rules. |
| CLI-assisted orchestration step | Define or confirm workflow/input-packet fields before task generation: workflow ID, phase ID, iteration ID, role/objective, canonical sources, deliverables, prohibited edits, dependencies, acceptance criteria, validation expectations, handoff audience, and completion signal. |
| Blockers / watch items | Shared deliverables require one owner or merge contract; incomplete generated task cards remain `draft` or `blocked`. |

### E04 - Backlog Generation and Readiness Gates

| Item | Guidance |
| --- | --- |
| Readiness | `Draft`; may refine in controlled parallel with late E02 only when metadata ownership is explicit. |
| Primary owner | Backlog owner / integrator. |
| Supporting owners | Product reviewer, dependency analyst, tech lead/architect, QA/validator owner, security/privacy reviewer where applicable. |
| Depends on | E01; partial E02 for task-packet and dependency metadata alignment. |
| Unlocks | E05 implementation handoff and implementation-ready story candidates. |
| Required outputs | Traceable epic/story candidates, product/technical/quality/dependency/risk/implementation gates, dependency and concurrency notes. |
| CLI-assisted orchestration step | Generate or review backlog candidates only against canonical PRD/FR and E##/US-E##-### trace, then record gate status, owner, evidence, blockers, and safe/unsafe sequencing. |
| Blockers / watch items | Gate approvers are not yet named; E04 metadata must reconcile with final E02 workflow/task-packet contracts before promotion. |

### E03 - Deterministic Validation and Completion Signals

| Item | Guidance |
| --- | --- |
| Readiness | `Draft`; sequence after E02 contract stability. |
| Primary owner | Validator owner / QA standards owner. |
| Supporting owners | Orchestrator, integrator, standards owner, reviewer/gate owners. |
| Depends on | E01, E02, ADR-0014 initial validator scope. |
| Unlocks | E05 handoff confidence and repeatable readiness checks; supports E04 quality promotion. |
| Required outputs | Required-file, required-section, trace-marker, ID-format, source-immutability, completion-signal, contract-field, and future-scope guard checks; recovery handling for failed/not-run validation and token-budget or partial work. |
| CLI-assisted orchestration step | Implement or run objective checks only where rules are deterministic; record `validation_result_id`, target, check class, criteria, status, evidence, run context, follow-up owner, and related open questions. |
| Blockers / watch items | Placement across CLI, CI, task generation, or integrator review is open; subjective quality must stay review-only. |

### E05 - Orchestration Execution Handoff

| Item | Guidance |
| --- | --- |
| Readiness | `Draft`; final implementation handoff is blocked until E02-E04 validate or limitations are accepted. |
| Primary owner | Integrator / release operator. |
| Supporting owners | Orchestrator, validator owner, reviewer/gate owners, recovery owners, downstream implementation owner. |
| Depends on | E02, E03, E04; G1/G2, validation/quality, dependency/concurrency, and agent-output gates. |
| Unlocks | MVP1 CLI-assisted implementation launch package and downstream execution planning. |
| Required outputs | Launch sequence, owners, dependencies, validation/review status, accepted limitations, blockers, recovery paths, source-immutability confirmation, runtime/log reference treatment, and remaining open decisions. |
| CLI-assisted orchestration step | Package accepted contracts and blocked/partial states into a handoff that states what may proceed, what must wait, who owns recovery, and which validations/reviews are required before reliance. |
| Blockers / watch items | Missing reviewer, owner, validation evidence, source-immutability confirmation, or unresolved future-scope implementation claim blocks handoff readiness. |

## Recommended launch order

1. **Confirm E01 / G0 readiness**: review canonical paths, source attribution,
   uncertainty labels, source immutability, open-question handling, and quality
   criteria.
2. **Finalize E02 contracts**: stabilize workflow phase/iteration fields,
   task-packet required fields, dependency/write-target rules, and completion
   signal expectations.
3. **Run controlled E04 alignment**: reconcile backlog readiness metadata with
   E02 fields; assign product, technical, quality, dependency, risk, and
   implementation gate owners.
4. **Implement or dry-run E03 validators**: start with objective checks and
   record review-only criteria separately.
5. **Package E05 handoff**: include launch sequence, accepted artifacts,
   validation/review status, blockers, recovery paths, source-immutability
   confirmation, runtime/reference limitations, and open decisions.
6. **Defer MVP2+ work**: keep E06-E13 future/deferred until MVP1 task-packet,
   validation, and handoff conventions are accepted.

## Owner matrix

| Responsibility | Accountable owner role | Supporting roles |
| --- | --- | --- |
| Workflow launch readiness | Orchestrator / release operator | Integrator, tech lead, validator owner |
| Workflow/task-packet contract | Configuration owner / orchestrator | Standards owner, specialist role owners, integrator |
| Canonical deliverable acceptance | Integrator or domain reviewer | Product reviewer, architect, tech writer |
| Deterministic validation | Validator owner | QA/standards reviewer, orchestrator, specialist agents |
| Review-only gates | Gate-specific reviewer | Integrator, product owner, architect, security/privacy reviewer |
| Backlog readiness and dependencies | Backlog owner / dependency analyst | Product reviewer, tech lead, integrator |
| Recovery and rerun decisions | Recovery owner named per blocker | Orchestrator, validator owner, reviewer |
| Final implementation handoff | Integrator / release operator | Downstream implementation owner, all gate owners |

If a required owner is unknown, the affected work remains `blocked`,
`review-needed`, or `needs-spike` and must not be treated as implementation-ready.

## Dependency and blocker register

| ID | Type | Affected work | Current handling |
| --- | --- | --- | --- |
| RB-001 | Gate owner decision | E04, E05, all review-only gates | Use role-based owners until named people or teams are assigned. |
| RB-002 | Validator placement decision | E03, E05 | Define objective validator behavior now; decide CLI/CI/task-generation/integrator placement during E03 planning. |
| RB-003 | Machine-readable metadata decision | E02, E03, E04 | Keep Markdown-first structured sections/tables; add schema extraction only after a bounded validator spike. |
| RB-004 | E02/E04 metadata alignment | E04, E05 | Reconcile backlog readiness fields with final workflow/task-packet fields before promotion. |
| RB-005 | Runtime/log retention policy | E05, future observability | Treat runtime artifacts as operational-only; summarize material facts into canonical docs or handoff packages. |
| RB-006 | Future runtime/stack/governance decisions | E05 and any implementation-specific work | Keep runtime, storage, event, API, telemetry, approval automation, provider, tenancy, compliance, UI, and legacy choices open or convert them into bounded spikes. |
| RB-007 | Source immutability | All MVP1 tasks | Any unreviewed `raw/` or `research/` edit blocks release readiness until remediated. |

## CLI-assisted orchestration implementation steps

For each implementation or refinement task launched from this roadmap:

1. **Prepare the task packet** with workflow ID, phase ID, iteration ID, role,
   objective, canonical sources, exact deliverables, prohibited edits,
   dependencies, acceptance criteria, validation expectations, handoff audience,
   and expected completion signal.
2. **Check launch safety** by confirming upstream dependencies, owner/reviewer
   assignments, disjoint write targets or merge contract, and future-scope
   exclusions.
3. **Run or simulate the CLI-assisted workflow/task-generation boundary** using
   the current orchestration framework command conventions, recording command
   label, workflow/phase/iteration, source packet, task-card references, and
   runtime/log limitations where material.
4. **Execute bounded work** only against allowed deliverables and preserve
   source-backed, inferred, assumed, and open claims distinctly.
5. **Record validation** for required files, sections/headings, trace markers, ID
   format, source immutability, completion signal, contract fields, and
   future-scope guard where applicable.
6. **Route review-only gates** to named reviewer roles for product fit, evidence
   sufficiency, architecture fit, security/privacy, governance, risk, reusable
   behavior changes, and implementation readiness.
7. **Publish handoff context** with changed artifacts, validation performed/not
   performed, assumptions/open questions, risks/blockers, runtime references,
   prohibited-edit confirmation, downstream safety, follow-up owners, and one
   standard completion signal.

## Validation expectations before implementation-ready status

MVP1 work is implementation-ready only when applicable gates are `passed`,
`approved`, or `not-applicable` with rationale:

| Gate | Required evidence |
| --- | --- |
| Scope boundary | CLI-assisted, repository-first, Markdown/configuration scope with future product/runtime choices marked open. |
| Required artifacts | Expected docs/config/task packets/handoff artifacts exist or are marked blocked/partial with recovery owner. |
| Traceability | PRD/FR, E##, US-E##-###, workflow, phase, iteration, task, gate, validation, or runtime references are present where needed. |
| Task-packet completeness | Required fields and handoff audience are present before assignment. |
| Dependency/concurrency | Upstream dependencies are stable and write targets are disjoint or owned by one merge contract. |
| Deterministic validation | Objective checks have status, evidence, run context, and follow-up owner for failures. |
| Review-only readiness | Reviewer role, evidence, decision, rationale, affected work, and recovery action are recorded. |
| Source immutability | Changed-path summary confirms no prohibited `raw/` or `research/` edits. |
| Recovery coverage | Blocked, partial, failed, token-limited, conflicted, or review-rejected work has owner, impact, preserved output, recovery action, and validation/review needed. |

## Next refinement steps

1. Assign named owner roles or people for all readiness gate families.
2. Review E01 and record G0 acceptance or remaining recovery actions.
3. Normalize E02 task-packet metadata and E04 backlog readiness metadata into one
   field vocabulary.
4. Decide the first E03 validator implementation slice and runner placement.
5. Create an E05 handoff checklist or packet from the runbook and acceptance
   criteria after E02-E04 validation/review states are available.
6. Promote repeated process learnings into standards, workflow templates,
   validator rules, personas, or backlog gates only after review.

## Open decisions

| ID | Decision needed | Current MVP1 handling |
| --- | --- | --- |
| OQ-ROAD-001 | Who are the named accountable approvers for product, architecture/technical, quality/validation, dependency, security/privacy, governance, and implementation-readiness gates? | Use role-based owners until named approvers are accepted. |
| OQ-ROAD-002 | Which deterministic checks run in CLI, CI, task generation, integrator review, or another runner? | Keep behavior defined in docs; decide placement in E03 planning. |
| OQ-ROAD-003 | Which Markdown fields must become machine-readable for reliable validation? | Keep Markdown-first metadata; run a bounded schema/validator spike before changing the contract. |
| OQ-ROAD-004 | What runtime/log references must be retained, summarized, or discarded after orchestration runs? | Treat runtime evidence as operational-only unless summarized into canonical docs or handoff packages. |
| OQ-ROAD-005 | Which runtime, storage, event, API, telemetry, approval, provider, tenancy, compliance, UI, or legacy implementation choices are required after MVP1? | Keep these future/open and block implementation-specific claims until accepted architecture/governance decisions exist. |
