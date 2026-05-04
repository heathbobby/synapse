# Knowledge Grounding Standards

- **Status**: draft MVP2 source-grounding standard
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp2-iteration-01-source-grounding`
- **Last updated**: 2026-05-03

## Purpose

These standards define how Synapse sources become approved knowledge for role
agents, personas, workflow templates, standards, validators, and backlog gates.
They standardize source promotion, evidence classes, provenance, confidence,
freshness, review and approval, operational evidence handling, SME/persona
grounding, learning promotion, and validation gates.

These standards do not select or imply a runtime knowledge store, retrieval
algorithm, embedding model, search index, source connector, crawler, sync job,
tenant model, access-control mechanism, retention/deletion policy, compliance
implementation, provider runtime, or prompt-management service.

## Source basis

| Source | Standard use |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp2-iteration-01-source-grounding.md` | Defines the MVP2 source-grounding goal, deliverable scope, and future-scope exclusions. |
| `docs/MVP2/Knowledge/SourceInventory.md` | Provides source classes, source priorities, approved vs operational postures, confidence, freshness, ownership, and inventory readiness gates. |
| `docs/MVP2/Knowledge/GroundingModel.md` | Provides conceptual grounding records, promotion lifecycle, role-agent consumption contracts, persona grounding rules, and quality gates. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Provides agent evidence classes, task-packet inputs, output quality, handoff, and reusable behavior governance. |
| `docs/standards/ENGINEERING_STANDARDS.md` | Requires explicit interfaces, ownership boundaries, visible operability, and decision-needed treatment for unknown stack choices. |
| `docs/standards/EVENT_CONTRACT_STANDARDS.md` | Provides technology-neutral event, ownership, validation, approval, telemetry, and knowledge-loop contract standards. |
| `docs/refinement/APPLYING_LEARNINGS_PLAYBOOK.md` | Requires recurring learnings to update templates, personas, workflows, validators, standards, or backlog gates after review. |
| `docs/refinement/ORCHESTRATION_PLAYBOOK.md` | Defines iteration loop expectations for canonical docs, task cards, validation, feedback, and reusable improvements. |
| `docs/refinement/SCALABLE_ORCHESTRATION_PHILOSOPHY.md` | Reinforces source protection, repeatable orchestration skeletons, deterministic tools, and closed feedback loops. |
| `docs/MVP1/Platform/TestingStrategy.md` | Provides gate status values, deterministic validators, review-only checks, source immutability, future-scope guard, and runtime evidence treatment. |
| `docs/MVP1/Platform/AcceptanceCriteria.md` | Provides acceptance criteria for traceability, evidence discipline, source immutability, runtime finding promotion, review gates, and process-learning routes. |
| `docs/MVP1/Platform/OperationalRunbook.md` | Provides operational handling for runtime artifacts, source immutability issues, recovery, readiness handoffs, and escalation. |

## Standard principles

1. **Approved knowledge starts with approved or promoted sources**: Canonical
   `docs/` artifacts, reviewed `.orchestration/config/` files, and reviewed
   approved extracts may ground future agent behavior within their stated scope.
2. **Operational evidence is not durable truth**: Runtime memos, task cards,
   logs, command output, validation output, branch/SHA references, raw material,
   research notes, and future external systems require review and promotion
   before they may become reusable knowledge.
3. **Provenance travels with claims**: Source path or ID, source class, source
   posture, evidence class, confidence, freshness, owner, applicability, and
   limitations must remain attached when claims are summarized or transformed.
4. **Uncertainty must remain visible**: Inferred, assumed, low-confidence,
   stale, blocked, or open claims must not be rewritten as committed product,
   architecture, operations, persona, compliance, or implementation decisions.
5. **Promotion is a behavior-affecting change**: Any learning or source update
   that changes standards, personas, workflow templates, validators, task
   packets, backlog gates, or downstream role-agent behavior requires review.
6. **Future implementation stays open**: Source-grounding standards define
   contracts and gates only; implementation choices require later accepted
   architecture, governance, or domain decisions.

## Source promotion standards

### Promotion lifecycle

| Stage | Standard | Downstream use |
| --- | --- | --- |
| `candidate` | Source, claim, SME input, runtime finding, or learning signal is identified and assigned a source class. | Discovery only. |
| `proposed` | Claim text, source references, intended target, evidence class, confidence, freshness, owner, and limitations are recorded. | Review input only. |
| `review-needed` | Relevant reviewer, SME, standards owner, product owner, architect, integrator, validator owner, or governance role must decide. | Blocks reusable behavior changes. |
| `approved` | Reviewer accepts the claim, scope, evidence, confidence, freshness, target artifact, and limits. | May ground future agents within approved scope. |
| `operational-only` | Source remains useful for traceability, recovery, or audit-like context but is not durable knowledge. | Must not ground persona/template behavior. |
| `superseded` | A newer approved source or decision replaces the claim. | Historical reference only; cite superseding source. |
| `rejected` | Reviewer rejects the source or claim for grounding. | Do not consume except as limitation or risk context. |

### Promotion targets

| Target | Use when | Required reviewer |
| --- | --- | --- |
| Canonical docs | Claim affects product, requirements, architecture, planning, operations, implementation handoff, or work-item truth. | Relevant document owner plus integrator when downstream reliance changes. |
| Approved extract | A bounded summary of raw, research, runtime, SME, or future external evidence should become reusable without promoting the whole source. | Source owner plus SME/domain reviewer or integrator. |
| Standards | Claim changes evidence discipline, validation, documentation, event, governance, or reusable quality expectations. | Standards curator plus affected owner. |
| Persona guidance | Claim changes role responsibilities, prohibited actions, evidence requirements, or output standards. | Role owner, standards curator, and integrator. |
| Workflow template or task packet | Claim changes phase structure, role inputs, deliverables, dependencies, handoffs, or completion criteria. | Orchestrator/configuration owner. |
| Validator or quality gate | Claim creates an objective repeated check or review-only readiness gate. | Validator owner or QA lead plus relevant reviewer role. |
| Backlog gate or work item | Claim creates a dependency, spike, blocker, sequencing rule, risk, or implementation readiness condition. | Backlog owner or dependency analyst. |

Promotion must not modify `raw/` or `research/` files. Source material remains
read-only unless a future canonical rule explicitly grants authority.

## Evidence class standards

Use the AI agent evidence classes consistently:

| Evidence class | Grounding standard | Required handling |
| --- | --- | --- |
| `source-backed` | Directly supported by an approved source or approved extract. | Cite source path/ID and preserve scope, status, and limitations. |
| `inferred` | Reasonably derived from approved sources but not directly stated. | Mark inference; material behavior or implementation claims require caveat or review. |
| `assumed` | Needed to proceed but not validated. | Record assumption, validation need, owner, and downstream risk. |
| `open` | Unknown or requiring product, architecture, security/privacy, governance, source-owner, SME, or stakeholder decision. | Do not use as committed grounding; route to decision, reviewer, or spike. |

Claims that affect scope, architecture, data contracts, validation,
security/privacy, operations, dependencies, personas, or reusable behavior must
carry an evidence class.

## Provenance standards

Any reusable grounded claim, approved extract, task-packet context, persona
instruction, workflow template update, validation gate, or learning promotion
should preserve these logical fields. The fields are documentation and contract
requirements, not a physical schema commitment.

| Field | Requirement |
| --- | --- |
| `source_class` | Source class from `SourceInventory.md` or later approved extension. |
| `source_id_or_path` | Canonical path, config path, decision ID, work-item ID, runtime reference, review record, or future external source reference. |
| `source_status` | Approved source, approved extract, operational source, seed source, or future candidate source. |
| `evidence_class` | `source-backed`, `inferred`, `assumed`, or `open`. |
| `confidence` | High, medium, low, or blocked with rationale. |
| `freshness` | `current`, `recent`, `stale-risk`, `superseded`, or `unknown`. |
| `owner_role` | Role accountable for source correctness or promotion path. |
| `reviewer_role` | Role that approved, rejected, deferred, or requested changes when review is required. |
| `applicability` | Workflows, domains, personas, artifacts, decisions, or work items where the claim applies. |
| `limitations` | Source gaps, assumptions, stale markers, open decisions, future-scope exclusions, or compliance/access unknowns. |
| `promotion_state` | Candidate, proposed, review-needed, approved, operational-only, superseded, or rejected. |

Large source material should be referenced by path or stable ID rather than
embedded into prompts, events, handoffs, or persona guidance.

## Confidence standards

| Confidence | Standard | Allowed consumption |
| --- | --- | --- |
| High | Approved source or approved extract, clear applicability, current/recent freshness, no known conflicting decision. | May ground role-agent output and reusable guidance within stated scope. |
| Medium | Approved source with interpretation, dependency, partial reviewer coverage, older freshness, or bounded assumption. | May guide drafts and grounded output with caveat; reusable behavior changes may require review. |
| Low | Operational, seed, stale-risk, unknown, or future-source context that has not been promoted. | Discovery, hypothesis, or promotion proposal only. |
| Blocked | Claim depends on unresolved source, owner, SME, product, architecture, governance, compliance, access, tenancy, retention, connector, storage, retrieval, embedding, provider, or runtime decision. | Must not ground committed behavior; record open decision, blocker, or spike. |

Confidence may be lowered by source drift, conflict between docs and config,
missing reviewer role, missing source owner, unknown freshness, or unreviewed
runtime evidence.

## Freshness standards

Freshness describes review recency and applicability for the claim being made.
It does not imply automated sync, expiration, retention, or deletion behavior.

| Freshness | Standard | Required action |
| --- | --- | --- |
| `current` | Reviewed in the current iteration or explicitly confirmed valid for the target claim. | Safe to use within scope. |
| `recent` | Accepted in a prior iteration and no superseding source is known. | Confirm no later conflict before high-confidence reusable use. |
| `stale-risk` | Predates newer decisions, source drift, review gaps, or likely domain change. | Require owner/reviewer confirmation before grounding future behavior. |
| `superseded` | Replaced by a newer approved source or decision. | Use only for history; cite the superseding source. |
| `unknown` | Review date, source owner, or applicability is unclear. | Treat as low confidence or open until clarified. |

Source-grounded task packets should state whether `current` or `recent`
freshness is required and how stale-risk or unknown sources are handled.

## Review and approval standards

Review is required before any source promotion or grounding change that:

- turns runtime, raw, research, SME, or future external evidence into approved
  knowledge;
- changes persona behavior, workflow templates, task packets, validators,
  standards, or backlog gates;
- resolves or reclassifies low-confidence, blocked, stale-risk, assumed, or open
  claims;
- affects product scope, architecture, operations, dependencies, release
  readiness, security/privacy, governance, compliance, retention, tenancy,
  access, or provider posture; or
- accepts a limitation where deterministic validation was not run or failed.

Approval records must include:

| Field | Requirement |
| --- | --- |
| Reviewer role | Named accountable role; lack of reviewer blocks approval. |
| Evidence reviewed | Source paths/IDs, extracts, runtime references, validation results, assumptions, open questions, or SME notes. |
| Decision | Approve, reject, request changes, defer, escalate, supersede, or mark not applicable. |
| Rationale | Reason for decision and limits of approval. |
| Affected downstream work | What may proceed and what must wait. |
| Recovery or follow-up | Owner and action when not approved or only partially accepted. |

Deterministic checks may confirm field presence and prohibited edits, but they
must not imply subjective evidence sufficiency, SME validation, governance
approval, or implementation readiness without a review record.

## Approved vs operational source standards

| Source posture | Meaning | Direct role-agent grounding | Required handling |
| --- | --- | --- | --- |
| Approved source | Reviewed canonical doc, decision, standard, work item, roadmap, input packet, or reviewed configuration accepted for stated scope. | Yes, within scope and freshness limits. | Cite path/ID; preserve status, assumptions, open decisions, and limitations. |
| Approved extract | Reviewed summary of seed, runtime, SME, or external evidence promoted into a canonical artifact or approved review record. | Yes, within extract scope. | Cite extract plus original source reference when available; include reviewer and confidence. |
| Operational source | Runtime memo, generated task card, CLI log, command output, validation output, branch/SHA, or transient handoff. | No durable grounding. | Use for traceability, recovery, or promotion proposal; summarize material facts before reliance. |
| Seed source | Raw or research material preserving original context. | No implementation grounding. | Read-only; promote findings through canonical docs or approved extracts. |
| Future candidate source | External docs, tickets, chat, incidents, customer/legacy corpora, source systems, or ungoverned SME material. | No. | Discovery only until owner, access, provenance, freshness, compliance, and promotion rules are accepted. |

When approved docs and operational evidence conflict, downstream reliance stays
blocked or review-needed until an integrator or accountable owner resolves the
conflict through promotion, correction, supersession, or accepted limitation.

## Role-agent consumption standards

### Task-packet grounding fields

Grounding-aware task packets should identify:

| Field | Requirement |
| --- | --- |
| `required_approved_sources` | P0/P1 sources that must be read or cited. |
| `allowed_operational_references` | Runtime/log references allowed only for traceability, recovery, or promotion proposals. |
| `prohibited_sources` | Sources that must not directly ground output, including raw/research and future external sources unless source review is explicit. |
| `evidence_expectations` | Required evidence classes and where assumptions/open questions must be recorded. |
| `confidence_threshold` | Minimum confidence for committed claims. |
| `freshness_expectation` | Required freshness label and stale/unknown handling. |
| `promotion_scope` | Whether the agent may propose, draft, or directly update a promotion target. |
| `handoff_requirements` | Changed artifacts, source summary, validation status, assumptions/open questions, prohibited-edit confirmation, and promotion recommendations. |

### Consumer expectations

| Consumer | Consumption standard | Output standard |
| --- | --- | --- |
| Orchestrator | Use approved source inventory, workflow config, input packets, dependency gates, and accepted decisions. | Ground task packets with source posture, exclusions, validation expectations, and blocked/open decisions. |
| Specialist role agent | Use only assigned approved sources and allowed operational references. | Preserve evidence, confidence, freshness, provenance, assumptions/open questions, validation status, and completion signal. |
| Standards curator | Use standards, grounding model, recurring learnings, and source-promotion gaps. | Update reusable standards only within deliverable scope and with review expectations. |
| Data architect | Use source inventory, grounding model, provenance, freshness, and confidence contracts. | Keep data contracts technology-neutral and mark storage/retrieval/connectors as open. |
| Product or requirements role | Use approved requirements and product sources. | Preserve traceability and assumption/open status for product and backlog claims. |
| Architect or tech lead | Use approved architecture, decisions, and open-decision records. | Avoid stack/runtime commitments unless accepted by canonical decisions. |
| Persona or template owner | Use approved role, source, evidence, and quality guidance. | Record provenance, reviewer, rationale, confidence, freshness, and limits for behavior changes. |
| Integrator or reviewer | Use handoffs, validation status, source provenance, promotion requests, and runtime summaries. | Record decisions, accepted limitations, recovery owners, and downstream-safe consumption notes. |

Agents must report blockers rather than silently expanding source authority or
turning future/open implementation topics into commitments.

## SME and persona grounding standards

SME/domain knowledge may ground reusable behavior only when:

1. The SME source, reviewer role, domain applicability, and limits are recorded.
2. The claim is promoted into an approved extract, canonical doc, persona
   guidance, workflow template, or backlog gate.
3. Evidence class, confidence, freshness, and assumptions/open questions remain
   attached after transformation.
4. Security/privacy, sensitive data, access, tenancy, retention, compliance, and
   domain constraints are classified as known, assumed, open, blocked,
   needs-spike, or not applicable.
5. Behavior-affecting persona changes include reviewer attribution and rationale.

Persona guidance may include source-backed or reviewed inferred claims with high
or medium confidence. Low-confidence claims may appear only as caveats,
discovery prompts, validation needs, or escalation instructions. Open claims must
remain explicit prohibitions, blockers, or questions.

Persona guidance must not:

- embed raw/research, runtime, or future external claims directly without
  promotion;
- remove evidence, confidence, freshness, or limitations when converting claims
  into instructions;
- override task-packet sources, prohibited edits, deliverables, or completion
  criteria;
- imply a knowledge-store, retrieval, embedding, source-connector, tenancy,
  compliance, retention, access-control, provider, or runtime implementation.

## Learning promotion standards

Runtime evidence may create a learning signal when it shows repeated:

- task-packet defects;
- source drift or stale-source use;
- missing provenance, evidence class, confidence, or freshness;
- validation gaps;
- blocked approvals or missing reviewer roles;
- token-budget or partial-completion patterns;
- persona ambiguity or role-boundary overreach;
- unpromoted runtime reliance;
- workflow/template gaps;
- backlog readiness blockers.

Recurring learnings must name an owner and promotion target:

| Learning target | Owner | Review expectation |
| --- | --- | --- |
| Standards update | Standards curator | Affected owner confirms behavior change and limits. |
| Persona update | Role owner / standards curator | Integrator or reviewer confirms source-backed behavior. |
| Workflow template update | Orchestrator / configuration owner | Config/doc drift is checked before promotion. |
| Validator/check update | Validator owner / QA lead | Objective rule or review-only gate is clearly separated. |
| Backlog gate or work item | Backlog owner / dependency analyst | Dependency, risk, or spike impact is recorded. |
| Canonical doc update | Relevant doc owner / integrator | Durable truth changes are reviewed and traceable. |

If the same grounding failure appears twice, propose a reusable standards,
persona, template, validator, or backlog-gate update rather than treating it as
an isolated issue.

## Validation gates

Knowledge-grounding deliverables, task packets, persona updates, promotion
requests, and approved extracts are ready for downstream reliance only when all
applicable gates are `passed`, `approved`, or `not-applicable` with rationale.
Any `failed`, `blocked`, `needs-spike`, `request-changes`, unresolved
`review-needed`, or required `not-run` gate blocks reliance.

| Gate | Deterministic evidence | Review-only evidence | Blocks readiness when |
| --- | --- | --- | --- |
| Source posture gate | Each source is classified as approved, approved extract, operational, seed, or future candidate. | Reviewer confirms classification is appropriate for downstream use. | Operational, seed, raw/research, or future source evidence is treated as approved. |
| Provenance gate | Required provenance fields are present where material. | Reviewer confirms provenance is sufficient for downstream reliance. | Claims cannot be traced or limitations/open decisions are dropped. |
| Evidence gate | Claims use `source-backed`, `inferred`, `assumed`, or `open`. | Evidence sufficiency reviewer confirms material uncertainty is visible. | Assumptions or open questions become committed behavior. |
| Confidence gate | Confidence label and rationale are present for reusable claims. | Reviewer confirms low/blocked claims are routed to assumptions, open decisions, or spikes. | Low or blocked confidence grounds committed persona, product, or implementation behavior. |
| Freshness gate | Freshness label is present when claim reuse depends on review recency. | Owner confirms stale-risk or unknown sources before reusable use. | Stale, unknown, or superseded sources drive future behavior without review. |
| Promotion gate | Promotion state, target, owner, reviewer, and outcome are recorded. | Reviewer approves source promotion and limits. | Runtime, raw, research, SME, or external findings bypass promotion. |
| Approved-vs-operational gate | Operational references are labeled operational-only, summarized, canonicalized, unavailable, or not applicable. | Integrator confirms material runtime facts are promoted or limitations accepted. | Downstream trust depends on non-durable runtime evidence without summary or limitation. |
| Persona behavior gate | Persona/template changes include source references, confidence, freshness, reviewer, rationale, and limits. | Role owner/standards curator/integrator accept behavior change. | Reusable persona behavior changes without attribution or review. |
| SME/domain gate | SME/domain claims include SME/reviewer role, applicability, limits, and governance classification. | SME/domain reviewer accepts the extract or flags open decisions. | SME claims are embedded directly or governance topics are assumed. |
| Source immutability gate | Changed-path summary confirms `raw/` and `research/` were not edited. | Source owner/integrator reviews any violation before reliance. | Raw or research files are modified without explicit authority and recovery. |
| Future-scope gate | Document avoids implementation choices for storage, retrieval, embeddings, connectors, tenancy, access, retention, compliance, provider, runtime, or prompt service. | Architect/governance reviewer confirms open decisions are preserved. | Grounding standard or asset commits to future technology/governance implementation. |

## Open decisions

| ID | Decision needed | Current standard |
| --- | --- | --- |
| OQ-KGS-001 | What concrete knowledge store, retrieval, search, embedding, indexing, or prompt-context mechanism should implement grounding? | Future/open; use logical contracts and citations only. |
| OQ-KGS-002 | Which source connectors, crawlers, sync jobs, or external systems should be supported first? | Future/open; external sources remain future candidates until governed. |
| OQ-KGS-003 | What tenancy, access-control, sensitive-data, retention, deletion, compliance, provider, and audit policies apply to grounded knowledge? | Future/open governance blockers for implementation; classify concerns without selecting controls. |
| OQ-KGS-004 | Who are the named accountable reviewers for source promotion, SME validation, freshness review, persona changes, and reusable behavior changes? | Use role-based owners until named people or teams are accepted. |
| OQ-KGS-005 | What freshness cadence or expiration threshold applies by source class and domain? | Use freshness labels only; do not define automated expiration. |
| OQ-KGS-006 | Which provenance fields should become machine-readable for validators or future event contracts? | Keep Markdown-first contracts until a bounded validator/schema decision is accepted. |
| OQ-KGS-007 | What runtime/log references must be retained, summarized, or discarded after orchestration runs? | Summarize material findings into canonical docs or approved handoffs; leave retention policy open. |
| OQ-KGS-008 | What persona composition or inheritance format should consume grounded knowledge in later MVP2 work? | This standard defines grounding rules only; representation remains a future persona/template decision. |

## Assumptions

- MVP1 canonical docs, work items, standards, decisions, and reviewed
  orchestration configuration are sufficient approved sources for MVP2
  source-grounding standards.
- Markdown-first standards, tables, and review records are sufficient until a
  later validator or schema decision requires machine-readable contracts.
- Role-based owners are acceptable placeholders until named accountable people or
  teams are assigned.
- Human reviewers and SMEs remain accountable for evidence sufficiency,
  confidence/freshness disputes, source promotion, persona behavior changes, and
  governance-sensitive decisions.
- Runtime artifacts and logs are useful operational evidence but are not durable
  knowledge until summarized, reviewed, and promoted.
