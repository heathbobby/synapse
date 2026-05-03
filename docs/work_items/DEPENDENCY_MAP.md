# Synapse Work Item Dependency Map

- **Status**: draft dependency analysis
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `backlog-refinement`
- **Role**: `dependency_analyst`
- **Last updated**: 2026-05-03
- **Primary trace**: PRD-001, PRD-002, PRD-003, PRD-005, PRD-008; FR-001, FR-002, FR-003, FR-004, FR-005, FR-006, FR-007, FR-008, FR-018, FR-019, FR-020

## Purpose

This dependency map makes Synapse backlog sequencing explicit before MVP
technical documentation or implementation begins. It maps epic and story
dependencies, current blockers, safe parallelism, unsafe sequencing, readiness
gates, and recommended refinement/implementation order for work items using the
`E##` and `US-E##-###` naming conventions.

## Source register

| Source ID | Source | How this map uses it |
| --- | --- | --- |
| S1 | `docs/refinement/iteration-inputs/backlog-refinement.md` | Iteration goal, dependency-analysis role scope, naming conventions, and completion criteria. |
| S2 | `docs/work_items/INDEX.md` | Canonical epic/story IDs, MVP placement, requirement trace, readiness status, and listed dependencies. |
| S3 | `docs/work_items/E01/INDEX.md` | Refined E01 story details, E01 assumptions, open questions, and downstream handoff conditions. |
| S4 | `docs/work_items/E01/DELIVERABLES.md` | E01 deliverables, quality gate, cross-epic handoffs, risks, and done criteria. |
| S5 | `docs/work_items/TECHNICAL_REFINEMENT_GATES.md` | Technical readiness gates, dependency/concurrency gate, and implementation-readiness decision rules. |
| S6 | `docs/planning/CONCURRENCY_ANALYSIS.md` | Safe/unsafe parallelism, artifact ownership rules, phase guidance, and conflict recovery. |
| S7 | `docs/planning/EXECUTION_ORCHESTRATION.md` | Phase/MVP sequence, G0-G5 dependency gates, recovery paths, and MVP1 launch order. |
| S8 | `docs/requirements/PRODUCT_REQUIREMENTS.md` | Product requirement trace, MVP framing, product blockers, and open questions. |
| S9 | `docs/requirements/FUNCTIONAL_REQUIREMENTS.md` | Functional requirement trace, especially FR-018, FR-019, and FR-020 for backlog generation, readiness, and dependency mapping. |

## Dependency principles

1. **Canonical docs gate all downstream work**: E01 must establish stable
   canonical paths, provenance/uncertainty rules, source immutability, open
   questions, and quality criteria before dependent epics treat artifacts as
   implementation contracts. [S2, S3, S4, S7]
2. **Workflow contracts precede validation and handoff**: E02 defines phases,
   task packets, dependencies, roles, deliverables, and write-target
   coordination before E03 and E05 can finalize validation/completion behavior or
   execution handoff. [S2, S5, S7]
3. **Backlog readiness can refine in parallel only after E01**: E04 may overlap
   with late E02 review when write targets are disjoint, but it must reconcile
   with E02 task-packet metadata before promotion. [S2, S6, S7]
4. **Open decisions constrain implementation**: unresolved MVP1 delivery mode,
   first domain/initiative, metadata format, validator scope, product mode,
   compliance, tenancy, storage, event transport, runtime, and integration
   choices must block implementation-specific claims or become bounded spikes.
   [S5, S6, S7, S8, S9]
5. **Parallelism requires disjoint ownership**: parallel work is safe only with
   stable upstream context, disjoint write targets or a single owner, bounded
   scope, and deterministic validation or review gates. [S5, S6, S9]

## Epic dependency graph

| Epic | MVP | Readiness | Upstream dependencies | Downstream unlocks | Current blockers / constraints |
| --- | --- | --- | --- | --- | --- |
| E01 Canonical Documentation Foundation | MVP1 | Refined | None | E02, E03, E04, E05, E06, E12 | Metadata format and approval-owner questions remain open but do not block E01 refinement. |
| E02 Workflow Definition and Task-Packet Model | MVP1 | Draft | E01 | E03, E05; informs E04 | Requires accepted canonical paths, metadata expectations, source/uncertainty labels, and quality gate from E01. |
| E03 Deterministic Validation and Completion Signals | MVP1 | Draft | E01, E02 | E05; supports E04 quality promotion | Blocked by stable E02 task-packet/workflow contracts and initial validator-scope decision. |
| E04 Backlog Generation and Readiness Gates | MVP1 | Draft | E01; partial E02 | E05; implementation-ready backlog candidates | Requires E01 traceability/readiness semantics; must reconcile readiness/dependency fields with E02 metadata. |
| E05 Orchestration Execution Handoff | MVP1 | Draft | E02, E03, E04 | MVP1 implementation launch decision | Blocked until E02-E04 validate and MVP1 delivery mode/first domain are decided. |
| E06 Source Inventory and Grounding Model | MVP2 | Deferred | E01, E02 | E07, E08, E12 | Deferred until MVP1 task-packet conventions are stable and first source types are prioritized. |
| E07 SME Persona and Role Template Library | MVP2 | Deferred | E02, E06 | E08, E11 | Unsafe before workflow/task-packet conventions and source grounding are stable. |
| E08 Domain Configuration Model | MVP2 | Deferred | E02, E07 | E12; supports reusable domain adaptation | Deferred until persona composition and domain configuration decisions are accepted. |
| E09 Workflow Status and Monitoring Surface | MVP3 | Deferred | E02, E03 | E10, E11 | Deferred until workflow states, task statuses, completion signals, and event families are stable. |
| E10 Human Approval Checkpoints | MVP3 | Deferred | E09 | E11; governance hardening | Deferred until monitoring/status model and approval classes/autonomy policy are defined. |
| E11 Feedback Capture and Improvement Promotion | MVP3 | Deferred | E03, E07, E09 | Continuous improvement of templates/process | Deferred until completion signals, persona templates, and monitoring surfaces are stable. |
| E12 Legacy-to-Greenfield Requirement Extraction | MVP4 | Deferred | E01, E06, E08 | E13 | Blocked by concrete legacy-transition customer/domain, source corpus, compliance posture, and adapter boundaries. |
| E13 Transition-State Planning Artifacts | MVP4 | Deferred | E12 | Legacy bridge implementation planning | Blocked until E12 validates current-state assumptions and future-state gaps. |

## MVP1 story dependency map

| Story | Epic | Upstream dependencies | Safe to refine in parallel with | Unsafe sequencing / blockers | Gate to proceed |
| --- | --- | --- | --- | --- | --- |
| US-E01-001 Define the canonical documentation registry | E01 | None | Other E01 preparation that does not depend on final metadata labels | None; this is the foundation story. | G0 canonical foundation readiness. |
| US-E01-002 Standardize source attribution and uncertainty labels | E01 | US-E01-001 | US-E01-003 after path families are clear | Unsafe before canonical path families are identified. | Product, traceability, and source/evidence gates. |
| US-E01-003 Protect raw and research inputs during canonical drafting | E01 | US-E01-001 | US-E01-002 after path families are clear | Unsafe if any task edits `raw/` or `research/` files. | Source immutability and agent-output gates. |
| US-E01-004 Maintain the open-question and validation-need register | E01 | US-E01-002 | US-E01-005 once uncertainty labels are drafted | Unsafe before open-question/assumption labels are standardized. | Product, traceability, dependency, and risk gates. |
| US-E01-005 Define canonical artifact acceptance-quality criteria | E01 | US-E01-001, US-E01-002 | US-E01-004 once labels and registry are available | Unsafe before canonical registry and uncertainty labels exist. | Quality, dependency, risk, and implementation gates. |
| US-E02-001 Define workflow phase and iteration metadata | E02 | E01 | US-E04-001 and US-E04-002 after E01 acceptance if write targets are disjoint | Unsafe before E01 metadata and canonical paths are accepted. | G1 MVP1 scope/mode gate and G2 workflow/task-packet gate. |
| US-E02-002 Define role-agent task packet structure | E02 | US-E02-001 | US-E02-003 if a single E02 owner reconciles shared metadata | Unsafe before phase/iteration metadata is stable. | G2 workflow/task-packet gate and agent-output gate. |
| US-E02-003 Define dependency and write-target coordination rules | E02 | US-E02-001 | US-E04-003 once metadata fields are aligned | Unsafe without explicit ownership for shared files and dependency fields. | Dependency/concurrency gate. |
| US-E03-001 Specify deterministic validation checks for MVP1 artifacts | E03 | E01, E02 | US-E03-002 after E02 contracts stabilize | Unsafe before workflow/task-packet fields and deliverables are known. | Validation/quality gate and G2 completion-signal prerequisites. |
| US-E03-002 Specify completion, partial-completion, and blocked signals | E03 | E02 | US-E03-001 after E02 contracts stabilize | Unsafe before task packet lifecycle and role outputs are defined. | Agent-output gate and G2 workflow/task-packet gate. |
| US-E03-003 Define recovery handling for validation and token-budget failures | E03 | US-E03-001, US-E03-002 | None until signal and validation drafts exist | Unsafe before validation failures and completion signals are specified. | Validation/quality, operations, and recovery gates. |
| US-E04-001 Generate traceable epic and story candidates from canonical requirements | E04 | E01 | US-E02-001 after E01 acceptance if write targets are disjoint | Unsafe before PRD/FR trace and canonical docs are stable. | Product and requirements traceability gates. |
| US-E04-002 Apply product, technical, quality, dependency, risk, and implementation readiness gates | E04 | E01, partial E02 | US-E02-002 or US-E02-003 only with metadata coordination | Unsafe if E02 task-packet metadata is still in flux and no reconciliation owner exists. | Technical readiness gates and E01 quality gate. |
| US-E04-003 Document dependency and concurrency notes for backlog items | E04 | E01, partial E02 | US-E02-003 with explicit field/owner coordination | Unsafe before dependency fields and write-target rules are aligned. | Dependency/concurrency gate. |
| US-E05-001 Package MVP1 implementation handoff and launch sequence | E05 | E02, E03, E04 | US-E05-002 after E02-E04 validate | Unsafe before E02-E04 validate, G1 decisions are made, and open blockers are listed. | G1, G2, validation/quality, dependency/concurrency, and agent-output gates. |
| US-E05-002 Record MVP1 assumptions, exclusions, and unresolved blockers | E05 | E02, E03, E04 | US-E05-001 after E02-E04 validate | Unsafe before upstream unresolved decisions are known and cross-linked. | Product, risk, governance, and handoff readiness gates. |

## Blocker register

| Blocker ID | Type | Affected work | Blocking impact | Recommended resolution path |
| --- | --- | --- | --- | --- |
| B-DM-001 | Product/architecture decision | E03, E05; implementation launch | MVP1 cannot be sized or handed off until delivery mode is chosen: docs-only, CLI-assisted, or runtime-backed. | Resolve during G1; if unresolved, keep E03/E05 technology-neutral and mark implementation blocked. |
| B-DM-002 | Product decision | E02, E04, E05; later E06-E08 | First domain/initiative is not selected, limiting concrete workflow templates and backlog examples. | Use this repository's concept-to-implementation workflow as the internal reference if no external adopter is ready. |
| B-DM-003 | Metadata contract decision | E02, E03, E04 | Markdown-only versus machine-readable metadata affects task packets, validators, and readiness fields. | Accept a minimum Markdown contract for backlog refinement; sequence machine-readable metadata as a later spike if needed. |
| B-DM-004 | Validation scope decision | E03, E04, E05 | Validators beyond file existence, required sections, and traceability are not yet selected. | Define initial deterministic checks and label review-only criteria. |
| B-DM-005 | Approval owner / governance decision | E04, E05, E10 | Story promotion and open-question closure lack named accountable approvers. | Assign product, architecture, quality, security/privacy, dependency, and integrator reviewers for readiness gates. |
| B-DM-006 | Runtime/stack/compliance decisions | E05 and any implementation-specific story | Storage, event transport, tenancy, compliance, runtime, UI, and provider choices remain open. | Defer implementation-specific claims or convert them into bounded architecture/security spikes. |
| B-DM-007 | Source type and grounding priority | E06, E07, E08, E12 | MVP2 and legacy bridge planning cannot commit retrieval, freshness, or source-governance behavior. | Prioritize initial source types after MVP1 task-packet conventions stabilize. |
| B-DM-008 | Legacy customer/domain/corpus | E12, E13 | Legacy bridge work cannot move past validation/refinement. | Validate a concrete transition scenario, source corpus, adapter boundaries, and compliance posture. |

## Safe parallelism map

| Timing | Safe parallel work | Preconditions | Merge / review gate |
| --- | --- | --- | --- |
| Current backlog-refinement iteration | Dependency map, technical gates, E01 deliverables, and work-item index updates by separate owners. | Fixed input packet; disjoint write targets; no edits to `raw/` or `research/`. | Integrator review for ID consistency, source trace, uncertainty labels, and dependency alignment. |
| After E01 acceptance | US-E02-001 workflow metadata refinement and US-E04-001 backlog candidate refinement. | E01 canonical registry, traceability labels, and quality gate accepted. | Both outputs use the same PRD/FR trace, readiness statuses, and dependency fields. |
| Late E02 review | US-E02-003 coordination rules and US-E04-003 backlog dependency notes. | E02 metadata owner assigned; write targets are disjoint or explicitly coordinated. | Dependency/concurrency gate confirms ownership and unsafe parallelism notes. |
| After E02 stabilizes | US-E03-001 validation checks and US-E03-002 completion signals. | Workflow/task-packet fields and deliverables are stable enough to validate. | E03 review reconciles validation, completion, partial-completion, blocked, and recovery states. |
| After E02-E04 validate | US-E05-001 handoff sequence and US-E05-002 assumptions/blockers register. | E02, E03, and E04 outputs are accepted or blockers are explicit. | Handoff review confirms G1/G2 status and unresolved implementation blockers. |
| MVP2 preparation | E06 source inventory and E07 persona template modeling. | MVP1 workflow/task-packet conventions stable. | Knowledge/persona gate confirms source types, provenance, freshness, and persona composition. |
| MVP3 preparation | E09 monitoring requirements and E10 approval-policy discovery. | Workflow states, task statuses, and completion signals stable. | Governance/feedback gate confirms state/event mapping and approval classes. |

## Unsafe sequencing map

| Unsafe sequence | Why unsafe | Required mitigation |
| --- | --- | --- |
| Starting E02, E03, E04, or E05 implementation before E01 is accepted. | Downstream agents may treat draft assumptions as canonical truth. | Complete G0 review and accept canonical paths, source labels, immutable-source rule, open-question tracking, and quality gate. |
| Starting E03 before E02 contracts are stable. | Validators and completion signals need task-packet fields, deliverables, and workflow states. | Sequence E03 after US-E02-001 through US-E02-003 reach reviewed draft status. |
| Starting E05 before E02-E04 validate. | Handoff would package unstable workflow, validation, or backlog readiness contracts. | Wait for E02, E03, and E04 review; list unresolved blockers explicitly. |
| Parallel edits to shared requirements, architecture, backlog, or gate files without one owner. | ID drift, contradictory scope, and merge conflicts can invalidate traceability. | Assign a single file owner and use review memos or disjoint files for parallel input. |
| Persona/template implementation before E02 and E06. | Persona responsibilities depend on task-packet conventions and source grounding. | Stabilize workflow/task-packet conventions, then prioritize source inventory. |
| Monitoring UI, visual canvas, event transport, storage, runtime, tenancy, or provider implementation before state/event and architecture decisions. | Open decisions may invalidate technical work and product assumptions. | Keep outputs technology-neutral or run explicit decision spikes. |
| Approval automation before autonomy and risk policy. | Agents could proceed through high-impact steps without agreed human accountability. | Define approval classes, evidence requirements, approvers, and audit records. |
| Legacy adapter implementation before a validated customer/domain/corpus. | Adapter choice, permissions, compliance, and migration constraints are unknown. | Validate E12 prerequisites before E13 planning or adapter work. |

## Gate alignment

| Gate | Required before | Applies to | Dependency-map interpretation |
| --- | --- | --- | --- |
| G0 Canonical foundation readiness | MVP1 refinement/implementation fan-out | E01, then E02-E05 | E01 must be accepted before downstream epics are promoted beyond draft refinement. |
| G1 MVP1 scope and mode gate | `mvp1-domain-infrastructure` or implementation launch | E02-E05 | Decide MVP1 delivery mode, first domain/initiative, metadata format, and initial validator scope. |
| G2 Workflow/task-packet gate | Validation/completion-signal work | E02, E03, E05 | E02 must define workflow and task-packet contracts before E03 and E05 finalize dependent behavior. |
| G3 Knowledge/persona gate | MVP2 | E06-E08 | Source inventory, persona composition, provenance, freshness, and review/promotion rules must be accepted. |
| G4 Governance/feedback gate | MVP3 | E09-E11 | Workflow state, event/status mapping, approval classes, and feedback schema must be stable. |
| G5 Legacy bridge gate | MVP4 | E12-E13 | Legacy customer/domain, corpus, adapter, auth, rate-limit, audit, and compliance boundaries must be validated. |
| Technical readiness gates | Any implementation-ready story or task | All `US-E##-###` stories | Architecture, data/integration, validation/quality, observability, security/privacy/governance, dependency/concurrency, and agent-output gates must be `ready` or `not-applicable` with rationale. |

## Recommended refinement and implementation order

### Immediate refinement order

1. **Finish E01 review**: confirm US-E01-001 through US-E01-005 and D-E01-001
   through D-E01-005 are accepted as the canonical foundation.
2. **Resolve G1 minimum decisions**: choose MVP1 delivery mode, first
   domain/initiative, minimum metadata/traceability contract, and initial
   deterministic validator scope.
3. **Refine E02**: sequence US-E02-001, then US-E02-002 and US-E02-003 with a
   single owner for shared metadata and write-target coordination.
4. **Refine E04 in controlled parallel**: begin US-E04-001 after E01 acceptance;
   run US-E04-002 and US-E04-003 alongside late E02 only when metadata ownership
   and reconciliation are explicit.
5. **Refine E03**: after E02 contracts stabilize, define US-E03-001 and
   US-E03-002, then US-E03-003 recovery handling.
6. **Refine E05 last**: package US-E05-001 and US-E05-002 only after E02-E04 are
   reviewed and unresolved blockers are cross-linked.

### Implementation launch order

1. **E01** implementation or finalization tasks only, if G0 evidence is missing.
2. **E02** workflow/task-packet contracts.
3. **E04** backlog readiness and dependency annotations, overlapping with late
   E02 only under explicit write-target ownership.
4. **E03** deterministic validation, completion signals, and recovery handling
   after E02 contract stability.
5. **E05** MVP1 handoff and launch sequence after E02-E04 validate and G1
   blockers are resolved or explicitly assigned.
6. **E06-E08** MVP2 preparation only after MVP1 workflow/task-packet conventions
   are stable.
7. **E09-E11** MVP3 preparation only after workflow states, completion signals,
   approval classes, and feedback schema dependencies are stable.
8. **E12-E13** MVP4 legacy bridge only after a concrete legacy-transition
   scenario, source corpus, compliance posture, and adapter boundaries are
   validated.

## Completion criteria

This dependency map is ready for parent/integrator review when it:

- Uses `E##` and `US-E##-###` IDs consistently.
- Lists upstream dependencies, blockers, safe parallelism, unsafe sequencing,
  readiness gates, and recommended order.
- Preserves uncertainty around MVP mode, first domain, metadata format,
  validator scope, implementation stack, compliance, source types, and legacy
  corpus decisions.
- Treats `raw/` and `research/` as immutable sources and does not require edits
  outside canonical `docs/` deliverables.
