# Concurrency Analysis

- **Status**: draft canonical foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `concept-extraction`
- **Last updated**: 2026-05-03
- **Purpose**: Define safe and unsafe parallelism for Synapse planning,
  refinement, and implementation preparation while preserving dependency gates
  and source uncertainty.

## Source Register

| Source ID | Source | How this document uses it |
| --- | --- | --- |
| S1 | `docs/refinement/iteration-inputs/concept-extraction.md` | Completion criterion requiring concurrency analysis and immutable-source handling. |
| S2 | `docs/requirements/PRODUCT_REQUIREMENTS.md` | Product-level requirements, MVP hypotheses, open questions, and uncertainty policy. |
| S3 | `docs/requirements/FUNCTIONAL_REQUIREMENTS.md` | FR-006 task packets, FR-007 validation, FR-008 completion signaling, FR-019 readiness gates, and FR-020 dependency mapping. |
| S4 | `docs/planning/DELIVERY_BACKLOG.md` | Candidate MVPs, epics, sequential dependencies, safe parallelism candidates, and blocking open questions. |
| S5 | `docs/planning/EXECUTION_ORCHESTRATION.md` | Phase/MVP sequence, dependency gates, recovery paths, and next-action recommendations. |
| S6 | `docs/architecture/ARCHITECTURE.md` | Component boundaries, workflow/persona/knowledge/event dependencies, and open architecture decisions. |
| S7 | `docs/architecture/TECHNICAL_SPECIFICATIONS.md` | Runtime states, task dispatch constraints, event contract families, and non-functional requirements. |
| S8 | `docs/architecture/DECISIONS.md` | Accepted architecture directions and open architecture decisions. |
| S9 | `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md` | Prescriptive within-iteration and across-iteration concurrency rules, deterministic validation, and recovery patterns. |

## 1. Concurrency Posture

Concurrency is supported when work has **stable upstream context**, **disjoint
write targets**, **bounded role responsibilities**, and **deterministic validation
or review gates**. It is unsafe when agents need each other's in-flight outputs,
write the same deliverable, depend on unresolved sponsor/architecture decisions,
or could convert assumptions into committed scope. [S3, S4, S5, S9]

The current repository is still in concept extraction. Treat the guidance below
as a planning baseline, not proof that all listed work is implementation-ready.
MVP boundaries, first customer/domain, product mode, compliance, source systems,
runtime, storage, event transport, and visual designer format remain open. [S2,
S4, S6, S8]

## 2. Concurrency Invariants

1. **No shared-file parallel writes without an owner**: if two roles need the same
   document, one owns the canonical edit and the other provides review input or a
   memo. [S3, S7, S9]
2. **Launch gates outrank throughput**: preparing downstream context while
   upstream agents run is encouraged, but launching dependent work waits for the
   relevant validation gate. [S5, S9]
3. **Canonical docs beat raw inputs**: raw and research files may be read as
   sources but must not be modified; implementation agents should consume
   reviewed canonical docs as the working contract. [S1, S2, S8, S9]
4. **Open decisions constrain concurrency**: work requiring unresolved decisions
   should become a validation task, spike, or explicit assumption rather than an
   implementation branch. [S2, S4, S8]
5. **Recovery is scoped and traceable**: partial completions, token-budget issues,
   or validation misses should be split into bounded recovery tasks with clear
   deliverables and resume gates. [S3, S5, S9]

## 3. Safe Parallelism Matrix

| Timing | Parallel work | Preconditions | Why safe | Validation / merge gate |
| --- | --- | --- | --- | --- |
| Phase 0 canonical foundation | Requirements, architecture, and backlog drafting by separate owners. | Source packet is fixed; write targets are disjoint canonical files. | Outputs can cross-reference after drafting without concurrent edits to the same file. | Integrator review for source attribution, uncertainty labels, and ID consistency. |
| After G0 foundation acceptance | E02 workflow/task-packet template drafting and E04 backlog readiness-gate refinement. | E01 metadata and canonical requirement IDs accepted. | Workflow schema and backlog gate documents can evolve separately, then be reconciled. | Both trace to PRD/FR IDs and agree on dependency/readiness fields. |
| Within MVP iteration 2 | Conceptual entity modeling by domain, if each domain writes separate files or sections with a single integrator. | Iteration 1 domain boundaries accepted. | Domains can document local models independently when shared records are predefined. | Cross-domain terminology and shared record review. |
| Within MVP iteration 3 | API/integration contract work and event-family detail work. | Entity/data model validated; contract ownership assigned. | REST/tool boundaries and event contracts are separable concerns when shared identifiers are stable. | Contract review for ownership, schema versioning, idempotency, retries, and audit needs. |
| Within MVP iteration 5 | QA strategy and acceptance criteria drafting. | Feature specifications validated. | Strategy and acceptance matrices can be drafted in separate outputs and reconciled at quality gate. | Product, architecture, quality, dependency, risk, and implementation gates pass. |
| MVP2 preparation | E06 source inventory and E07 persona template modeling. | MVP1 workflow/task-packet conventions stable. | Source grounding and persona shape are related but can be explored independently. | Knowledge/persona gate confirms source types, composition model, provenance, and freshness. |
| MVP3 preparation | Monitoring requirements and approval-policy discovery. | Workflow states, task statuses, and event families are stable. | Status visibility and approval classes can be analyzed separately. | Governance gate confirms state/event mapping and autonomy policy. |
| Across iterations | Prepare next iteration `README`, `CONTEXT`, completion criteria, and prompt inputs while current agents run. | Next iteration structure is unlikely to change based on current outputs. | Preparation does not mutate upstream deliverables or launch dependent work. | Upstream validation passes before launch; prepared context is refreshed from actual outputs. |

## 4. Unsafe Parallelism Matrix

| Unsafe pattern | Why unsafe | Required sequencing or mitigation |
| --- | --- | --- |
| Launching MVP1 before G0 canonical foundation review. | Downstream agents may treat draft assumptions as committed implementation truth. | Complete and review canonical docs, source registers, uncertainty labels, and backlog gates first. |
| Feature specifications before entities and integration contracts. | User workflows would invent records, APIs, or events that architecture has not bounded. | Run infrastructure, entities/models, and integrations before features. |
| Operations/runbooks before quality and acceptance gates. | Operational guidance would lack validated success/failure criteria and recovery thresholds. | Sequence operations after quality/acceptance. |
| Parallel edits to `PRODUCT_REQUIREMENTS.md`, `FUNCTIONAL_REQUIREMENTS.md`, backlog, or architecture without a single owner. | ID drift and contradictory scope assumptions can break traceability. | Assign one writer per file; use review memos for parallel input. |
| Persona template implementation before workflow/task-packet conventions. | Persona responsibilities and completion signals depend on task-packet shape and workflow states. | Stabilize E02/E03 before E07 implementation. |
| Knowledge retrieval/storage implementation before source-type and governance decisions. | Retrieval, freshness, confidence, and compliance requirements are open. | Run source inventory and governance decisions first; keep work technology-neutral until decided. |
| Monitoring UI or visual canvas implementation before workflow state/event contracts. | UI state and graph representation may be invalidated by runtime/event decisions. | Define state model, event families, and template representation first. |
| Approval automation before autonomy and risk policy. | Agents may proceed through high-impact steps without agreed human accountability. | Define approval classes, evidence requirements, and audit records first. |
| Legacy bridge adapter implementation before customer/domain validation. | Adapter choice, permissions, compliance, and source corpus are unknown. | Validate a concrete legacy-transition scenario and adapter boundaries first. |
| Work requiring stack, tenancy, compliance, event transport, storage, or LLM/runtime choices before decisions are accepted. | Architecture decision log explicitly leaves these open. | Record/resolve the open decision or frame the output as a technology-neutral specification. |

## 5. Phase and MVP Parallelism Guidance

### Phase 0: Canonical foundation

- **Safe**: role agents can draft disjoint canonical docs from the same fixed
  source packet.
- **Unsafe**: simultaneous edits to the same canonical file or any edits to
  `raw/` or `research/`.
- **Gate**: G0 passes when canonical docs exist, cite sources, preserve
  uncertainty, and align on MVP/backlog IDs. [S1, S5]

### MVP1: Concept-to-implementation pipeline

- **Safe**: after E01, E02 workflow/task-packet drafting can overlap with E04
  readiness-gate drafting; after E02 stabilizes, E03 validation/completion
  signal work proceeds.
- **Unsafe**: E03 before E02, E05 handoff before E02-E04 validate, or any
  implementation commitment before MVP1 mode is selected.
- **Gate**: MVP1 G1 decisions are accepted: CLI-assisted delivery, the
  orchestration-framework domain, Markdown-first metadata, and initial validator
  scope. [ADR-0011, ADR-0012, ADR-0013, ADR-0014]

### MVP2: Knowledge grounding and SME/persona templates

- **Safe**: E06 source inventory and E07 persona modeling can run in parallel
  once task-packet conventions exist.
- **Unsafe**: building retrieval, storage, inheritance, or domain configuration
  as committed runtime behavior before source types and persona composition are
  accepted.
- **Gate**: knowledge/persona gate confirms source inventory, confidence labels,
  review/promotion flow, and persona composition approach. [S3, S5, S6, S7]

### MVP3: Monitoring, approvals, and feedback

- **Safe**: monitoring requirements and approval policy analysis can run in
  parallel once workflow statuses and event families are stable.
- **Unsafe**: visual designer/canvas implementation before workflow template
  representation, event/state model, and operator needs are decided.
- **Gate**: governance/feedback gate confirms workflow state model, event
  mapping, approval classes, feedback schema, and improvement-promotion owner.
  [S5, S6, S7]

### MVP4: Legacy bridge

- **Safe**: domain discovery, source-corpus inventory, and adapter risk analysis
  can run in parallel as validation work.
- **Unsafe**: adapter implementation, migration workflow commitments, or
  compliance-sensitive handling before a concrete customer/domain and corpus are
  validated.
- **Gate**: legacy bridge gate confirms adapter boundaries, read/write access,
  auth, rate limits, audit, compliance, and isolation from the core. [S5, S6,
  S8]

## 6. Artifact Ownership Rules

| Artifact type | Parallel input allowed? | Parallel writing allowed? | Owner / merge recommendation |
| --- | --- | --- | --- |
| Product and functional requirements | Yes, via review notes or memos. | No. | Requirements owner maintains IDs, source labels, and open questions. |
| Architecture and technical specifications | Yes, via architecture review notes. | No for shared docs; yes for separate domain files after structure exists. | Architect owns shared boundaries and open decisions. |
| Delivery backlog and work items | Yes, if story/epic paths are disjoint. | Yes only after ID ranges and metadata fields are assigned. | Product/backlog owner reconciles priority, dependencies, and readiness gates. |
| Workflow/task-packet templates | Limited. | No until schema ownership is clear. | Orchestrator/architect owner merges role needs into a stable template. |
| Event contracts | Yes by event family after entity model exists. | Yes if each family has an owner and schema version. | Integration/event owner validates shared correlation and audit fields. |
| Persona templates | Yes by role/domain after base template accepted. | Yes for separate persona files; no for base persona without owner. | Persona registry owner protects inheritance/composition consistency. |
| Validation criteria | Yes by artifact class. | Yes in disjoint files; shared validator changes need owner. | Quality owner reconciles deterministic checks and thresholds. |
| Operational runbooks | Yes after quality criteria exist. | Yes by domain/component. | SRE/operations owner checks cross-domain incident and rollback consistency. |

## 7. Recovery and Conflict Handling

| Concurrency issue | First response | Recovery action | Prevention for next run |
| --- | --- | --- | --- |
| Two agents edited the same file differently. | Stop downstream dependent work and preserve both diffs for review. | Assign one owner to reconcile; convert the other contribution into review notes if needed. | Use disjoint write targets or explicit ownership in task packets. |
| Agent started from stale upstream context. | Mark output provisional. | Refresh from canonical upstream output and rerun only impacted sections. | Do not launch dependent iteration until validation gate passes. |
| Parallel outputs use conflicting IDs or terminology. | Block promotion to ready state. | Integrator normalizes IDs/terms and updates shared glossary or metadata contract. | Stabilize metadata before fan-out. |
| Partial completion leaves uneven artifact coverage. | Do not expand scope to hide gaps. | Create recovery iteration split by remaining files/domains. | Reduce role complexity or file count in future prompts. |
| Open decision discovered mid-work. | Freeze implementation-specific claims. | Record or update open decision; reframe output as technology-neutral or sequence a decision spike. | Scan OAD/OQ blockers before launch. |
| Validator misses a concurrency-related defect. | Treat as process gap. | Add deterministic check or review checklist for the defect class. | Apply feedback to template, role guidance, or validator. |

## 8. Next-Action Recommendations

1. Before additional fan-out, complete parent/integrator review of the Phase 0
   canonical foundation and explicitly accept G0.
2. Assign single-file owners for each canonical doc family; allow parallel input
   through memos or disjoint work-item files.
3. Use the accepted MVP1 delivery mode and first domain/initiative before
   launching `mvp1-domain-infrastructure`: CLI-assisted orchestration over the
   orchestration-framework domain.
4. Use the Markdown-first work-item/task-packet metadata contract before
   parallelizing backlog expansion.
5. Use parallel preparation for the next iteration, but refresh prepared context
   from validated upstream outputs immediately before launch.
6. Defer visual UI, storage, event transport, tenancy, compliance-sensitive
   handling, and legacy adapter implementation until their open decisions are
   resolved or bounded as spikes.

## 9. Completion Criteria for This Concurrency Analysis

This document is ready for parent/integrator review when it:

- Distinguishes safe and unsafe parallelism by dependency, artifact ownership,
  and MVP phase.
- Preserves uncertainty around MVP scope, stack, compliance, and customer/domain
  decisions.
- Defines conflict recovery paths for shared-file edits, stale context, partial
  completion, and open-decision blockers.
- Provides concrete next actions for controlled fan-out after G0 review.
