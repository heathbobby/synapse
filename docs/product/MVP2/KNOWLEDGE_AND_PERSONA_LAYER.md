# Synapse Product MVP2: Knowledge and Persona Layer

- **Status**: product-owner draft
- **MVP**: MVP2
- **Last updated**: 2026-05-03
- **Companion workflow spec**: `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md`
- **Primary sources**:
  - `docs/refinement/iteration-inputs/product-mvp2-knowledge-persona-layer.md`
  - `docs/product/MVP_STRATEGY.md`
  - `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
  - `docs/product/PRODUCT_CAPABILITY_MAP.md`
  - `docs/product/MVP1/AI_COWORKER_WORKSPACE.md`
  - `docs/product/MVP1/OPERATOR_JOURNEY.md`
  - `docs/MVP2/Knowledge/SourceInventory.md`
  - `docs/MVP2/Knowledge/GroundingModel.md`
  - `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`

## Product definition

Synapse Product MVP2 is the **knowledge and persona layer** that turns approved
sources, SME guidance, and reviewed workflow learnings into governed knowledge
assets and reusable persona templates that AI coworkers can safely consume.

MVP2 extends the MVP1 AI coworker workspace by making knowledge and expert role
behavior reusable across future workflow runs. Operators, SMEs, and reviewers can
see what is approved, what remains uncertain, which persona behavior is grounded,
and what learning is waiting for promotion.

MVP2 is not the repository's source-grounding documentation. Those documents
provide evidence and product inputs. The product capability is the Synapse layer
that governs knowledge assets, source approval, SME/persona templates,
confidence, freshness, provenance, and learning promotion.

## Product/tooling boundary

| Concern | MVP2 product treatment |
| --- | --- |
| Governed knowledge asset | Product object that packages approved claims, provenance, owner, applicability, confidence, freshness, review status, and consumption limits. |
| Source approval workflow | Product workflow for classifying, reviewing, approving, rejecting, deferring, or superseding sources and approved extracts. |
| SME guidance | Product-reviewed expert input that can become an approved extract, knowledge asset, persona guidance, workflow template update, validator, or backlog gate. |
| Persona template | Product object that packages role perspective, responsibilities, evidence rules, boundaries, escalation behavior, review expectations, and allowed knowledge assets. |
| Learning promotion | Product workflow that converts reviewed workflow learnings into reusable assets without silently changing future AI coworker behavior. |
| Current source-grounding docs | Product input evidence and standards. They are not the customer-facing product, registry, approval experience, or runtime by themselves. |
| Repository-only orchestration artifacts | Prototype or process evidence only. They must not become required customer concepts. |

## MVP2 product scope

### In scope

MVP2 shall define the Synapse product layer that enables:

1. A governed registry of knowledge assets available to approved workflows and
   AI coworker personas.
2. Source intake and approval decisions for sources, approved extracts, SME
   inputs, and learning candidates.
3. Reusable SME/persona templates with role behavior, evidence discipline,
   confidence/freshness/provenance requirements, and escalation controls.
4. Confidence, freshness, provenance, applicability, limitations, and review
   status visible wherever knowledge or persona behavior is consumed.
5. A learning promotion path from completed workflow outputs, review decisions,
   blockers, and repeated issues into reusable knowledge, persona guidance,
   workflow template changes, validators, or backlog gates.
6. Human review and accountability for source approval, SME validation, persona
   behavior changes, and learning promotion.

### Deferred from MVP2

- Selecting a knowledge store, retrieval mechanism, embedding model, search
  index, source connector, crawler, synchronization job, prompt-management
  service, provider, or runtime architecture.
- Selecting tenancy, access-control, retention, deletion, compliance, privacy,
  billing, deployment, or customer administration implementation.
- Automating final source approval, SME validation, risk acceptance, or learning
  promotion without human review.
- Building a broad external connector marketplace or arbitrary ingestion system.
- Productizing every expert workflow, domain pack, persona pack, or legacy
  bridge corpus.
- Treating raw, research, runtime, or repository-only process artifacts as
  durable product knowledge without reviewed promotion.

## Primary personas

| Persona | Role in MVP2 | Needs |
| --- | --- | --- |
| Knowledge owner | Owns a source family or knowledge asset and remains accountable for correctness, applicability, freshness, and limitations. | Clear approval state, review queue, ownership boundaries, and stale/conflict indicators. |
| SME / domain reviewer | Provides or validates expert guidance before it becomes reusable. | Evidence reviewed, applicability, confidence, limitations, and downstream behavior impact. |
| Persona/template owner | Maintains reusable role behavior for AI coworkers. | Source-backed persona instructions, review history, escalation rules, and safe update workflow. |
| Human operator | Selects knowledge and personas for workflow runs. | Understand which assets and persona templates are approved, current, applicable, and review-needed. |
| AI coworker | Consumes approved knowledge and persona guidance during bounded work. | Clear role, allowed assets, evidence expectations, confidence threshold, freshness rules, and escalation triggers. |
| Product/governance reviewer | Reviews product fit, risk, approval posture, and reusable behavior changes. | Traceability from source to claim to persona/workflow impact and promotion decision. |

## Jobs to be done

| ID | Job |
| --- | --- |
| JTBD-MVP2-001 | When a team has approved product, domain, or operational knowledge, I want Synapse to package it as reusable governed assets so AI coworkers do not rely on ad hoc context. |
| JTBD-MVP2-002 | When a new source or SME input appears, I want a clear approval workflow so future AI coworker behavior changes only after review. |
| JTBD-MVP2-003 | When I assign an AI coworker role, I want a reusable persona template that explains its expertise, boundaries, evidence rules, confidence limits, and escalation behavior. |
| JTBD-MVP2-004 | When knowledge is stale, uncertain, or unsupported, I want Synapse to make that visible before it is used in workflow output. |
| JTBD-MVP2-005 | When a workflow completes, I want useful lessons promoted into reusable knowledge, persona guidance, workflow templates, validators, or backlog gates without unsafe automatic updates. |

## Product capabilities

| Capability ID | Capability | MVP2 product behavior | Source alignment |
| --- | --- | --- | --- |
| MVP2-KPL-001 | Governed knowledge asset registry | Synapse shall maintain product-visible knowledge assets with owner, source references, evidence class, confidence, freshness, applicability, limitations, review status, and promotion state. | SYN-PRD-001; CAP-003 |
| MVP2-KPL-002 | Source classification and approval | Synapse shall support source states such as candidate, proposed, review-needed, approved, operational-only, superseded, and rejected. | SYN-PRD-001; CAP-003 |
| MVP2-KPL-003 | Approved extracts | Synapse shall let reviewers promote bounded summaries of raw, operational, SME, or future external evidence into approved extracts before reuse. | SYN-PRD-001; CAP-003 |
| MVP2-KPL-004 | SME guidance capture | Synapse shall capture SME guidance with reviewer role, domain applicability, evidence reviewed, limitations, confidence, freshness, and downstream impact. | SYN-PRD-002; CAP-004 |
| MVP2-KPL-005 | Persona template registry | Synapse shall maintain reusable persona templates with role purpose, responsibilities, allowed knowledge, prohibited behavior, evidence rules, quality gates, and escalation behavior. | SYN-PRD-002; CAP-004 |
| MVP2-KPL-006 | Persona grounding controls | Synapse shall require persona guidance to preserve provenance, confidence, freshness, assumptions, open questions, and reviewer rationale when knowledge becomes role behavior. | SYN-PRD-001, SYN-PRD-002; CAP-003, CAP-004 |
| MVP2-KPL-007 | Confidence controls | Synapse shall distinguish high, medium, low, and blocked confidence and prevent low or blocked claims from becoming committed reusable behavior without review. | SYN-PRD-001; CAP-003 |
| MVP2-KPL-008 | Freshness controls | Synapse shall mark knowledge as current, recent, stale-risk, superseded, or unknown and route stale-risk or unknown reusable use to owner review. | SYN-PRD-001; CAP-003 |
| MVP2-KPL-009 | Provenance controls | Synapse shall keep source path or source ID, source posture, evidence class, owner, reviewer, applicability, limitations, and promotion state visible for reusable claims. | SYN-PRD-001; CAP-003 |
| MVP2-KPL-010 | Knowledge/persona consumption guardrails | Synapse shall supply workflow runs and AI coworkers only with approved or explicitly allowed knowledge context and shall preserve exclusions and caveats in work packets. | SYN-PRD-002, SYN-PRD-009; CAP-002, CAP-004 |
| MVP2-KPL-011 | Learning promotion queue | Synapse shall collect workflow learnings as candidate updates to knowledge assets, persona templates, workflow templates, validators, standards, or backlog gates. | SYN-PRD-006; CAP-007 |
| MVP2-KPL-012 | Human review and auditability | Synapse shall require human approval, rejection, deferral, supersession, or escalation records before source promotion, SME validation, persona behavior changes, or reusable learning promotion. | SYN-PRD-005, SYN-PRD-009; CAP-005 |

## Product objects for MVP2

| Object | Description | Required product-visible properties |
| --- | --- | --- |
| Source candidate | A source, SME note, runtime finding, external reference, or learning signal proposed for review. | Source type/posture, owner, proposed use, limitations, confidence/freshness if known, requested reviewer. |
| Source approval decision | A human decision about whether a source or extract may ground future work. | Decision, reviewer, evidence reviewed, rationale, scope, limitations, follow-up owner. |
| Approved extract | A reviewed bounded summary promoted from seed, operational, SME, or external evidence. | Source references, reviewer, approved claim, applicability, confidence, freshness, limitations. |
| Knowledge asset | A reusable knowledge unit used by workflows or personas. | Asset kind, owner, claims, provenance, evidence class, confidence, freshness, applicability, review status, promotion state. |
| SME guidance record | Expert input or validation captured for product use. | SME/reviewer role, domain scope, guidance, evidence reviewed, caveats, downstream impact. |
| Persona template | Reusable role behavior for an AI coworker. | Role purpose, responsibilities, allowed knowledge, prohibited actions, evidence rules, confidence/freshness expectations, outputs, escalation behavior, reviewer. |
| Persona version/change record | Record of a persona behavior change. | Changed guidance, source/provenance, rationale, reviewer, confidence/freshness impact, affected workflows. |
| Grounding context | Bounded approved context supplied to a workflow run or AI coworker task. | Required approved assets, allowed operational references, excluded sources, evidence expectations, confidence threshold, freshness expectations. |
| Learning item | Candidate reusable improvement from workflow execution or review. | Signal, evidence, recurrence or impact, target asset type, owner, promotion state, decision. |
| Promotion request | Proposal to change reusable knowledge, persona, workflow, validator, standard, or backlog behavior. | Candidate claim/change, source references, target, owner, reviewer, confidence/freshness, decision outcome. |

## Persona template capability

MVP2 persona templates are reusable product assets, not one-off prompts. A
template should answer:

1. **Who this AI coworker is**: role purpose, expertise boundary, and intended
   workflow use.
2. **What it may use**: approved knowledge assets, approved extracts, allowed
   operational references, and prohibited source classes.
3. **How it reasons and reports**: evidence classes, confidence labels,
   freshness expectations, assumptions, open questions, and source citation
   expectations.
4. **What it produces**: output types, quality standards, handoff requirements,
   review needs, and completion signals.
5. **When it escalates**: low confidence, stale/unknown freshness, missing
   provenance, conflicting sources, prohibited source requests, sensitive/risky
   decisions, or scope drift.
6. **How it changes**: versioned behavior updates only through reviewed source,
   SME, or learning promotion.

## Confidence, freshness, and provenance controls

| Control | Product behavior | User-visible impact |
| --- | --- | --- |
| Evidence class | Claims are labeled source-backed, inferred, assumed, or open. | Operators and reviewers can tell what is supported versus uncertain. |
| Confidence | Claims and persona guidance are high, medium, low, or blocked. | Low/blocked claims cannot become committed reusable behavior without review. |
| Freshness | Knowledge is current, recent, stale-risk, superseded, or unknown. | Stale-risk or unknown knowledge prompts owner review before future reliance. |
| Provenance | Source references, source posture, owner, reviewer, applicability, limitations, and promotion state travel with the claim. | Users can trace why an AI coworker was allowed to rely on a claim or instruction. |
| Applicability | Assets state which workflows, domains, personas, or decisions they support. | Operators avoid applying knowledge outside its approved scope. |
| Review status | Assets and persona changes show whether they are candidate, proposed, review-needed, approved, rejected, deferred, or superseded. | Reusable behavior changes remain accountable and inspectable. |

## Human decisions and review gates

| Gate | Required human decision | Possible outcomes |
| --- | --- | --- |
| G0: Intake classification | What kind of source, SME input, or learning is this, and who owns it? | Candidate accepted for review, returned for clarification, rejected as out of scope. |
| G1: Source approval | Can this source or extract ground future Synapse work within a stated scope? | Approve, approve with limits, request changes, defer, reject, supersede. |
| G2: Knowledge asset promotion | Should the approved claim become a reusable knowledge asset? | Promote, revise, defer, reject, assign owner. |
| G3: SME validation | Is SME guidance accurate, applicable, and bounded enough for reuse? | Approve extract, request SME revision, limit applicability, escalate. |
| G4: Persona behavior change | Should this knowledge or learning change reusable persona behavior? | Approve version, request changes, defer, reject, escalate to role owner. |
| G5: Consumption readiness | Can a workflow or AI coworker consume this asset/template now? | Ready, ready with caveats, review-needed, blocked. |
| G6: Learning promotion | Should a workflow learning become reusable behavior or an improvement backlog item? | Promote, investigate, defer, reject with rationale. |

## MVP2 outputs

A successful MVP2 product layer should produce:

1. Governed knowledge assets with visible provenance, owner, confidence,
   freshness, applicability, limitations, review state, and promotion state.
2. Approved extracts from source, SME, operational, or learning evidence.
3. Source approval decisions with reviewer rationale and downstream limits.
4. Reusable persona templates with grounded role behavior and escalation rules.
5. Persona version/change records for behavior-affecting updates.
6. Grounding contexts that can be attached to future workflow runs and AI
   coworker work packets.
7. Learning promotion queue and promotion decisions.
8. Open product decisions for unresolved source ownership, review roles,
   external source priorities, or implementation/governance choices.

## Non-goals

- MVP2 is not a prompt library.
- MVP2 is not a repository documentation viewer.
- MVP2 is not the existing source-grounding docs or current orchestration
  process exposed as a product.
- MVP2 does not choose storage, retrieval, embedding, connector, provider,
  tenancy, compliance, access-control, retention, deletion, deployment, or
  runtime implementation.
- MVP2 does not automatically approve sources, SME claims, persona changes, or
  learning promotions.
- MVP2 does not allow raw, research, runtime, or ungoverned external material to
  directly become durable product knowledge.

## Acceptance criteria

| ID | Criterion |
| --- | --- |
| MVP2-KPL-AC-001 | A user can distinguish approved knowledge assets from candidates, operational-only evidence, rejected items, superseded items, and review-needed items. |
| MVP2-KPL-AC-002 | Each reusable knowledge asset exposes owner, provenance, evidence class, confidence, freshness, applicability, limitations, and review status. |
| MVP2-KPL-AC-003 | A reviewer can approve, reject, request changes, defer, supersede, or escalate a source or approved extract with rationale. |
| MVP2-KPL-AC-004 | A persona/template owner can define a reusable persona with allowed knowledge, prohibited behavior, evidence expectations, confidence/freshness rules, outputs, and escalation behavior. |
| MVP2-KPL-AC-005 | Persona behavior changes require source or learning provenance, reviewer rationale, and visible version/change record before reuse. |
| MVP2-KPL-AC-006 | Low-confidence, blocked, stale-risk, unknown, assumed, or open claims cannot become committed reusable behavior without review or explicit caveat. |
| MVP2-KPL-AC-007 | Workflow learnings enter a promotion queue with target type, owner, evidence, and decision state rather than silently changing future behavior. |
| MVP2-KPL-AC-008 | The product documentation preserves storage, retrieval, embedding, connector, provider, tenancy, compliance, access, retention, and runtime decisions as future/open. |

## Open product decisions

| ID | Decision | Impact |
| --- | --- | --- |
| MVP2-KPL-OQ-001 | Which first product surface should expose knowledge and persona management: workspace panel, registry view, review queue, or guided setup step? | Determines MVP2 interaction model and handoff with MVP1 workspace. |
| MVP2-KPL-OQ-002 | Who are the named accountable owner and reviewer roles for the first source families and persona templates? | Determines approval routing, freshness review, and promotion authority. |
| MVP2-KPL-OQ-003 | Which non-repository source families should be supported first after canonical product docs and reviewed extracts? | Determines future intake scope without selecting connectors. |
| MVP2-KPL-OQ-004 | What concrete freshness review cadence should apply by asset type or domain? | Determines review workload and stale handling; MVP2 uses labels only until decided. |
| MVP2-KPL-OQ-005 | What user-facing confidence thresholds should apply to workflow dispatch, handoff readiness, and persona template updates? | Determines when Synapse blocks, warns, or escalates. |
| MVP2-KPL-OQ-006 | What external governance, sensitive-data, compliance, access, or retention constraints apply to future sources? | Blocks future ingestion and runtime implementation decisions. |
| MVP2-KPL-OQ-007 | Which knowledge, persona, workflow, validator, and backlog promotion targets should be enabled first in the product experience? | Determines the first learning loop that MVP2 makes reusable. |
