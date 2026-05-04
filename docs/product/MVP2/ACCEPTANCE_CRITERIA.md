# Synapse Product MVP2 Acceptance Criteria

- **Status**: QA lead draft
- **Product slice**: MVP2 knowledge and SME persona layer
- **Last updated**: 2026-05-04

## Purpose

This document defines product acceptance criteria for the Synapse MVP2 knowledge
and persona layer. MVP2 acceptance is measured by whether Synapse can turn
approved sources, approved extracts, SME guidance, persona behavior, grounding
contexts, and reviewed workflow learnings into governed reusable assets that AI
coworkers can consume safely.

These criteria are product-facing and tool-agnostic. Current repository
grounding docs, orchestration artifacts, runtime memos, task cards, workflow
YAML, Cursor rules, and CLI-assisted workflows may provide prototype evidence,
but they are not the customer-facing product model or accepted MVP2 runtime.

## Source basis

| Source | Acceptance use |
| --- | --- |
| `docs/refinement/iteration-inputs/product-mvp2-knowledge-persona-layer.md` | Defines the MVP2 knowledge/persona goal, product/tooling boundary, role source references, and completion criteria. |
| `docs/product/MVP_STRATEGY.md` | Defines MVP2 as the knowledge and SME persona layer and keeps implementation choices deferred. |
| `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md` | Provides SYN-PRD trace IDs for governed knowledge, SME/persona templates, workflow composition, review, learning, human accountability, and domain-agnostic packaging. |
| `docs/product/PRODUCT_CAPABILITY_MAP.md` | Provides CAP trace IDs for the canonical knowledge registry, persona template system, human governance, learning promotion, and deferred capability boundaries. |
| `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md` | Defines MVP2 product capabilities, objects, controls, review gates, outputs, non-goals, and draft criteria. |
| `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md` | Defines the end-to-end source, knowledge, persona, grounding-context, and learning-promotion workflow. |
| `docs/product/MVP2/KNOWLEDGE_PERSONA_CONTRACTS.md` | Provides logical product contracts for knowledge, persona, grounding, promotion, review, learning, governance, and audit objects. |
| `docs/product/MVP2/PERSONA_TEMPLATE_SYSTEM.md` | Provides product-facing persona template hierarchy, role boundaries, grounding rules, governance, versioning, and learning-promotion expectations. |
| `docs/MVP2/Knowledge/GroundingModel.md` | Provides logical grounding records, evidence/confidence/freshness rules, approved-vs-operational consumption, promotion lifecycle, persona grounding rules, quality gates, and open decisions. |
| `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md` | Provides source promotion, provenance, confidence, freshness, review, SME/persona grounding, learning promotion, validation gates, source immutability, and future-scope standards. |

## Acceptance status values

Use these values when recording MVP2 product acceptance, review gates,
validation summaries, promotion decisions, or audit/governance reviews.

| Status | Meaning | Blocks product acceptance? |
| --- | --- | --- |
| `not-run` | Required validation or review has not been performed. | Yes, unless explicitly `not-applicable` with rationale. |
| `passed` | Deterministic criterion passed with evidence. | No. |
| `failed` | Deterministic criterion failed. | Yes, until recovered or accepted as a limitation by the right reviewer. |
| `review-needed` | Human, SME, product, standards, or governance judgment is required. | Yes, until approved, rejected, deferred, escalated, or marked not applicable with rationale. |
| `approved` | Named reviewer or accountable role accepted the criterion within recorded limits. | No, within those limits. |
| `request-changes` | Revision is required. | Yes, until changes are completed and accepted. |
| `blocked` | Missing source, owner, reviewer, decision, evidence, governance posture, or safe path prevents reliance. | Yes. |
| `needs-spike` | Bounded discovery is required before acceptance. | Yes, except for the spike itself. |
| `not-applicable` | Criterion does not apply and rationale is recorded. | No. |

## Classification model

| Classification | Meaning | Required evidence |
| --- | --- | --- |
| Deterministic | The criterion can be checked by repeatable inspection of required fields, states, sections, object relationships, status transitions, or changed paths. | Target object or surface, rule, status, evidence, and owner for failures. |
| Review-only | Human judgment is required for source authority, evidence sufficiency, SME correctness, persona behavior impact, governance, readiness, or promotion. | Reviewer role, evidence reviewed, decision, rationale, downstream effect, limits, and recovery or follow-up action. |
| Both | Objective completeness can pass while human judgment is still required. | Deterministic evidence plus named review decision. |

## MVP2 product acceptance matrix

All applicable criteria must be `passed`, `approved`, or `not-applicable` with
rationale before the MVP2 knowledge and persona layer is accepted as
product-ready for the scoped workflow/persona/source set. Any row with
`failed`, `blocked`, `needs-spike`, `request-changes`, unresolved
`review-needed`, or required `not-run` status blocks acceptance for the affected
scope.

| AC ID | Area | Trace | Acceptance criterion | Classification | Validation evidence | Blocks acceptance when |
| --- | --- | --- | --- | --- | --- | --- |
| MVP2-AC-001 | Product/tooling boundary | SYN-PRD-009, SYN-PRD-010; CAP-003, CAP-004 | Given any MVP2 surface, contract, workflow, or artifact, when it describes product behavior, then Synapse is presented as the governed knowledge/persona product layer and repository-only grounding docs, Cursor rules, orchestration memos, task cards, workflow YAML, CLI scaffolding, and framework internals are treated only as prototype evidence or internal tooling. | Both | Product boundary review plus future-scope guard. | Prototype tooling is required as a customer concept or treated as the product contract. |
| MVP2-AC-002 | Source intake | SYN-PRD-001, SYN-PRD-009; CAP-003 | Given a source, SME note, workflow learning, approved-extract candidate, operational reference, seed source, or future external source enters MVP2, when intake is inspected, then title/reference, source type, source posture, owner role, proposed use, target workflow/persona/domain, known limitations, and requested reviewer are present or explicitly blocked with owner. | Deterministic | Source candidate or intake checklist field-completeness check. | A candidate proceeds to review without source identity, posture, owner/reviewer, proposed use, or limitations. |
| MVP2-AC-003 | Intake classification gate | SYN-PRD-001, SYN-PRD-005, SYN-PRD-009; CAP-003, CAP-005 | Given a candidate is ready for classification, when G0 intake classification is decided, then the reviewer records candidate accepted for review, returned for clarification, rejected as out of scope, or blocked with evidence, rationale, proposed target, owner, and recovery action. | Review-only | G0 classification decision record. | A candidate advances toward reusable knowledge without an explicit intake decision and accountable owner. |
| MVP2-AC-004 | Source posture and state model | SYN-PRD-001; CAP-003 | Given a review item or source reference is displayed or consumed, when state is inspected, then it uses product-level states that distinguish candidate, proposed, review-needed, approved, approved with limits, operational-only, deferred, superseded, rejected, and blocked or plain-language equivalents. | Deterministic | Source/review item state checklist. | Users cannot distinguish approved sources from operational-only, rejected, superseded, deferred, blocked, or review-needed sources. |
| MVP2-AC-005 | Evidence, confidence, and freshness classification | SYN-PRD-001, SYN-PRD-009; CAP-003 | Given a reusable claim, extract, source summary, SME guidance, persona instruction, or grounding-context item is inspected, when classification is evaluated, then evidence class, confidence label and rationale, freshness label, applicability, assumptions/open questions, and limitations are present or explicitly marked not applicable with rationale. | Deterministic | Field-completeness check against evidence, confidence, freshness, applicability, and limitation fields. | Source-backed, inferred, assumed, and open claims are conflated, or confidence/freshness is missing for material reusable claims. |
| MVP2-AC-006 | Source review and approval decision | SYN-PRD-001, SYN-PRD-005, SYN-PRD-009; CAP-003, CAP-005 | Given a source or extract is submitted for approval, when G1 source approval is reviewed, then the reviewer can approve, approve with limits, request changes, defer, reject, supersede, escalate, or block with evidence reviewed, rationale, scope, limitations, downstream effect, and follow-up owner. | Review-only | G1 source approval record. | A source or extract grounds future work without reviewer decision, rationale, scope, limitations, or recovery owner for unresolved issues. |
| MVP2-AC-007 | Approved extract creation | SYN-PRD-001, SYN-PRD-009; CAP-003 | Given raw, research, runtime, operational, SME, seed, or future external evidence is proposed for reuse, when an approved extract is created, then the extract contains bounded approved claim text, original source reference when available, reviewer role, evidence reviewed, applicability, confidence, freshness, limitations, approval decision, and promotion state. | Both | Approved extract field-completeness check plus reviewer approval. | Unpromoted raw, research, runtime, operational, SME, or future external material becomes reusable product knowledge directly. |
| MVP2-AC-008 | Knowledge asset promotion | SYN-PRD-001, SYN-PRD-005, SYN-PRD-009; CAP-003, CAP-005 | Given an approved source or approved extract proposes a reusable claim, when G2 knowledge asset promotion is decided, then the reviewer records promote, revise, defer, reject, assign owner, or block with target asset, claims, provenance, confidence, freshness, applicability, consumption limits, and rationale. | Both | Knowledge asset promotion record and field checklist. | A reusable knowledge asset is created without approved evidence, owner, reviewer, provenance, limits, or promotion decision. |
| MVP2-AC-009 | Knowledge asset completeness | SYN-PRD-001; CAP-003 | Given a knowledge asset is available for workflow or persona consumption, when it is inspected, then asset kind, stable ID/reference, owner, reviewer, claims, source references, source posture, evidence class, confidence, freshness, applicability, limitations, review status, promotion state, downstream consumers, and consumption constraints are visible. | Deterministic | Knowledge asset object or registry field check. | Any reusable asset lacks traceable source, owner/reviewer, evidence, confidence/freshness, applicability, limitations, or review status. |
| MVP2-AC-010 | Knowledge registry findability and status visibility | SYN-PRD-001, SYN-PRD-009; CAP-003 | Given a knowledge owner, reviewer, operator, or persona owner uses the MVP2 registry, when they review available assets, then they can filter or distinguish approved, approved-with-limits, review-needed, operational-only, superseded, rejected, deferred, blocked, stale-risk, unknown-freshness, and low-confidence items. | Deterministic | Registry/list view or equivalent product-visible status checklist. | Users cannot tell which assets are reusable, caveated, historical, blocked, or review-needed. |
| MVP2-AC-011 | SME guidance capture and validation | SYN-PRD-002, SYN-PRD-005, SYN-PRD-009; CAP-004, CAP-005 | Given SME or domain guidance is proposed for reuse, when G3 SME validation is reviewed, then SME/reviewer role, domain applicability, evidence reviewed, guidance text, confidence, freshness, assumptions/open questions, limitations, downstream impact, and decision outcome are recorded. | Both | SME guidance record plus G3 validation decision. | SME claims enter approved extracts, knowledge assets, or persona behavior without reviewer attribution, applicability, caveats, or governance classification. |
| MVP2-AC-012 | Persona template definition | SYN-PRD-002, SYN-PRD-009; CAP-004 | Given a persona/template owner defines a reusable persona template, when the template is inspected, then role purpose, expertise boundary, responsibilities, intended workflow use, allowed knowledge assets/extracts, prohibited source classes, prohibited behavior, evidence rules, quality gates, output expectations, handoff requirements, confidence/freshness expectations, escalation behavior, owner, reviewer, and version are present. | Deterministic | Persona template field-completeness checklist. | A persona template can be selected without bounded role, allowed knowledge, prohibited behavior, evidence rules, output standards, escalation rules, or ownership. |
| MVP2-AC-013 | Persona template source grounding | SYN-PRD-001, SYN-PRD-002, SYN-PRD-009; CAP-003, CAP-004 | Given persona guidance includes a claim or instruction, when grounding is inspected, then each material behavior-affecting instruction traces to an approved source, approved extract, or validated SME guidance and preserves source path/ID or promotion reference, evidence class, confidence, freshness, assumptions/open questions, limitations, reviewer rationale, and applicability. | Both | Persona guidance provenance check plus reviewer decision for behavior-affecting instructions. | Persona guidance embeds raw/research, runtime, operational-only, low-confidence, stale-risk, unknown, assumed, open, or external claims as committed behavior without review and caveat. |
| MVP2-AC-014 | Persona behavior change gate | SYN-PRD-002, SYN-PRD-005, SYN-PRD-009; CAP-004, CAP-005 | Given approved knowledge, SME guidance, or learning could change reusable persona behavior, when G4 persona behavior change is decided, then the persona/template owner or reviewer records approve version, request changes, defer, reject, or escalate with changed guidance, source/provenance, rationale, confidence/freshness impact, affected workflows, limits, and version/change record. | Review-only | G4 persona version/change record. | Persona behavior changes silently, without source provenance, reviewer rationale, affected scope, or visible version history. |
| MVP2-AC-015 | Persona instance creation | SYN-PRD-002, SYN-PRD-009; CAP-002, CAP-004 | Given an operator instantiates a persona for a workflow run or AI coworker task, when the instance is inspected, then it references an approved persona template version, selected knowledge assets/extracts, role-specific objective, task/workflow scope, allowed operational references, prohibited sources/actions, evidence expectations, confidence/freshness thresholds, escalation triggers, handoff requirements, and consumption readiness state. | Deterministic | Persona instance or coworker assignment field-completeness check. | An AI coworker can act from an unversioned persona, unapproved template, unclear role scope, missing allowed/prohibited context, or missing readiness state. |
| MVP2-AC-016 | Persona instance override control | SYN-PRD-002, SYN-PRD-005, SYN-PRD-009; CAP-004, CAP-005 | Given a workflow run needs persona-instance customization, when overrides are reviewed, then any deviation from the approved template or grounding context is recorded as temporary, scoped, source-backed or caveated, reviewer-approved when behavior-affecting, and prevented from becoming reusable template behavior without promotion. | Both | Instance override record plus review decision for behavior-affecting changes. | Temporary run-specific instructions silently override template boundaries or become reusable behavior without review. |
| MVP2-AC-017 | Grounding context completeness | SYN-PRD-001, SYN-PRD-002, SYN-PRD-009; CAP-002, CAP-003, CAP-004 | Given knowledge and persona guidance are attached to a workflow run or AI coworker task, when grounding context is inspected, then it includes task/workflow IDs, required approved assets, approved extracts, allowed operational references, prohibited sources, exclusions, evidence expectations, confidence threshold, freshness expectation, assumptions/open questions, caveats, escalation instructions, and handoff requirements. | Deterministic | Grounding context field-completeness check. | AI coworker work is dispatched without bounded approved context, exclusions, caveats, confidence/freshness rules, or handoff expectations. |
| MVP2-AC-018 | Consumption readiness gate | SYN-PRD-001, SYN-PRD-002, SYN-PRD-005, SYN-PRD-009; CAP-002, CAP-003, CAP-004, CAP-005 | Given a grounding context and persona instance are ready for use, when G5 consumption readiness is decided, then the operator or reviewer records ready, ready with caveats, review-needed, blocked, or not applicable with evidence, rationale, caveats, blockers, escalation instructions, and downstream limits. | Both | G5 consumption readiness decision and context checklist. | Workflow dispatch or persona consumption proceeds while selected knowledge/persona context is unresolved, prohibited, stale-risk/unknown without review, low/blocked without caveat, or missing owner. |
| MVP2-AC-019 | Uncertainty and escalation handling | SYN-PRD-001, SYN-PRD-002, SYN-PRD-009; CAP-003, CAP-004, CAP-005 | Given low-confidence, blocked, stale-risk, unknown, superseded, assumed, open, conflicting, prohibited, governance-sensitive, or out-of-scope material appears, when consumption is evaluated, then Synapse surfaces it as caveat, blocker, assumption/open question, escalation need, or review-needed item rather than committed reusable behavior. | Both | Grounding/readiness review, caveat list, blocker list, or escalation record. | Uncertain or prohibited material grounds committed knowledge, persona, product, governance, or implementation behavior without review. |
| MVP2-AC-020 | AI coworker consumption discipline | SYN-PRD-001, SYN-PRD-002, SYN-PRD-009; CAP-002, CAP-003, CAP-004 | Given an AI coworker consumes MVP2 context, when its output or handoff is inspected, then it uses approved assets/extracts within applicability limits, labels operational references as operational-only, preserves evidence class, confidence, freshness, provenance, assumptions/open questions, and limitations, follows persona boundaries, and proposes promotion requests for reusable gaps. | Both | Output/handoff evidence review and source-use checklist. | AI coworker output expands source authority, drops caveats, violates persona boundaries, or relies on prohibited/unpromoted material. |
| MVP2-AC-021 | Learning signal capture | SYN-PRD-006, SYN-PRD-009; CAP-007 | Given completed runs, reviews, blockers, revisions, handoff feedback, stale-source issues, validation gaps, repeated defects, recovery patterns, or persona ambiguity create learning, when captured, then each learning item records signal summary, source/runtime reference, evidence, recurrence or impact, target asset type, owner, reviewer role, confidence/freshness impact, promotion state, rationale, and limitations. | Deterministic | Learning item field-completeness check. | Learning is unowned, untraceable, lacks target/reviewer, or cannot be reviewed for promotion. |
| MVP2-AC-022 | Learning promotion decision | SYN-PRD-005, SYN-PRD-006, SYN-PRD-009; CAP-005, CAP-007 | Given a learning item could change knowledge, approved extracts, persona templates, workflow templates, validators, standards, or backlog gates, when G6 learning promotion is reviewed, then the reviewer can promote, investigate, request changes, defer, reject, mark operational-only, or create backlog/spike with evidence, rationale, target, owner, limitations, and downstream effect. | Review-only | G6 promotion decision record. | Workflow learning silently changes future product behavior or reusable guidance without review and promotion record. |
| MVP2-AC-023 | Promotion target routing | SYN-PRD-001, SYN-PRD-002, SYN-PRD-003, SYN-PRD-006, SYN-PRD-009; CAP-001, CAP-003, CAP-004, CAP-007 | Given a source, SME claim, or learning is approved for promotion, when routing is inspected, then the target is one of knowledge asset, approved extract, persona template, workflow template, validator/quality gate, standard, backlog gate/work item, or documented open decision with appropriate owner and reviewer expectations. | Deterministic | Promotion request target and owner/reviewer checklist. | A promotion target is ambiguous, ownerless, outside MVP2 scope, or modifies reusable behavior without the right review path. |
| MVP2-AC-024 | Required review gate coverage | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given MVP2 source, knowledge, persona, grounding, or learning work is accepted, when gate coverage is inspected, then G0 intake classification, G1 source approval, G2 knowledge asset promotion, G3 SME validation, G4 persona behavior change, G5 consumption readiness, and G6 learning promotion are present where applicable or marked not applicable with rationale. | Deterministic | Gate coverage matrix or review summary. | Applicable gates are missing, unresolved, or bypassed for reusable knowledge/persona behavior. |
| MVP2-AC-025 | Human accountability | SYN-PRD-005, SYN-PRD-009; CAP-005 | Given source promotion, SME validation, persona behavior change, grounding readiness, governance-sensitive acceptance, or learning promotion requires judgment, when accountability is inspected, then a human owner/reviewer/approver role is named and unavailable reviewers are delegated, escalated, or blocked. | Both | Owner/reviewer roster plus gate records. | Review-only acceptance is implied without named accountable role, evidence reviewed, decision, rationale, limits, and recovery action. |
| MVP2-AC-026 | Audit trail and governance reconstruction | SYN-PRD-001, SYN-PRD-002, SYN-PRD-005, SYN-PRD-006, SYN-PRD-009; CAP-003, CAP-004, CAP-005, CAP-007 | Given material MVP2 actions occur, when auditability is inspected, then source intake, classification, source approval, extract creation, knowledge asset promotion, SME validation, persona template changes, persona instance overrides, grounding-context readiness, AI coworker consumption, learning capture, promotion decisions, rejection/supersession, and recovery are reconstructable through audit trail entries or equivalent review records with actor/role, target, state, evidence, rationale, timestamp/version marker, and correlation to affected objects. | Deterministic | Audit trail or activity summary checklist. | Material source, knowledge, persona, grounding, learning, or governance decisions cannot be traced to actor, target, state, evidence, rationale, and affected objects. |
| MVP2-AC-027 | Governance and source immutability | SYN-PRD-001, SYN-PRD-009; CAP-003, CAP-005 | Given MVP2 product criteria or related artifacts are changed, when repository changes or equivalent source operations are inspected, then `raw/` and `research/` remain unmodified and raw/research/runtime/external material is used only through reviewed promotion into approved extracts, canonical docs, or other approved product records. | Deterministic | Changed-path summary or source immutability check. | `raw/` or `research/` files are edited, or unpromoted source material is treated as durable product truth. |
| MVP2-AC-028 | Domain-agnostic packaging | SYN-PRD-010, SYN-PRD-009; CAP-003, CAP-004 | Given MVP2 knowledge assets or persona templates are defined, when product scope is reviewed, then assets and templates support domain-specific packs through explicit applicability and limitations without hard-coding a single customer/domain corpus or requiring legacy bridge content for MVP2 acceptance. | Review-only | Product scope review and applicability/limitations inspection. | MVP2 acceptance depends on a specific unvalidated domain pack, customer corpus, or legacy bridge implementation. |
| MVP2-AC-029 | Non-goals and deferred implementation boundary | SYN-PRD-009, SYN-PRD-010; CAP-003, CAP-004, CAP-005, CAP-007, CAP-008, CAP-010 | Given MVP2 scope is reviewed, when product claims are inspected, then storage, retrieval, embedding, search indexing, source connectors, crawlers, sync jobs, prompt-management service, model/provider/runtime selection, product API, event bus, tenancy, access control, retention/deletion, privacy/compliance, billing, deployment, admin tooling, arbitrary ingestion, broad connector marketplace, and automatic final approvals are marked deferred, future, or open. | Both | Future-scope guard plus product/architecture/governance review. | MVP2 acceptance depends on unsupported implementation choices, external connectors, compliance/admin capabilities, or automated approval. |
| MVP2-AC-030 | Acceptance traceability | SYN-PRD-001, SYN-PRD-002, SYN-PRD-005, SYN-PRD-006, SYN-PRD-009, SYN-PRD-010; CAP-003, CAP-004, CAP-005, CAP-007 | Given MVP2 acceptance evidence is prepared, when the acceptance package is inspected, then every accepted criterion maps to at least one SYN-PRD ID and at least one CAP ID and any untraced product claim is removed, traced, or marked as an open decision. | Deterministic | Acceptance trace matrix or row-by-row trace inspection. | Criteria, product claims, or acceptance evidence lack SYN-PRD/CAP trace or introduce unreviewed scope. |

## End-to-end journey acceptance

An MVP2 knowledge and persona layer is accepted only when the following
journey-level criteria are met:

1. A knowledge owner or reviewer can intake a source, SME note, approved-extract
   candidate, operational reference, or learning signal without treating it as
   durable truth.
2. The source or candidate can be classified by posture, evidence class,
   confidence, freshness, applicability, limitations, owner, reviewer, and
   promotion target.
3. A human reviewer can approve, limit, request changes, defer, reject,
   supersede, escalate, or block sources and extracts with rationale and
   downstream effect.
4. Approved extracts and governed knowledge assets preserve provenance,
   confidence, freshness, applicability, limitations, owner, reviewer, and
   promotion state.
5. SME guidance can be captured and validated before it changes approved
   extracts, knowledge assets, persona guidance, workflow templates, validators,
   standards, or backlog gates.
6. Persona templates encode role purpose, boundaries, allowed knowledge,
   prohibited behavior, evidence rules, output expectations, quality gates,
   confidence/freshness expectations, and escalation behavior.
7. Persona instances for workflow runs reference approved template versions and
   bounded grounding context, and instance overrides remain scoped and reviewed
   before becoming reusable behavior.
8. Grounding contexts can be attached to AI coworker work with approved assets,
   approved extracts, allowed operational references, prohibited sources,
   caveats, confidence/freshness rules, escalation instructions, and handoff
   requirements.
9. AI coworker outputs and handoffs preserve evidence, confidence, freshness,
   provenance, assumptions/open questions, limitations, and persona boundaries.
10. Workflow learnings enter a promotion path and cannot silently change future
    product behavior.
11. Human review gates, audit records, and governance decisions make reusable
    source, knowledge, persona, grounding, and learning changes reconstructable.
12. MVP2 remains product-facing and does not require customer-facing exposure of
    repository tooling, raw/research material, runtime memos, task cards, Cursor
    rules, workflow YAML, or orchestration framework internals.

## Required review gates

| Gate | Acceptance decision | Required record | Related criteria |
| --- | --- | --- | --- |
| G0: Intake classification | Accept for review, return for clarification, reject as out of scope, or block. | Candidate state, source type/posture, owner, reviewer, proposed use/target, rationale, recovery action. | MVP2-AC-002, MVP2-AC-003 |
| G1: Source approval | Approve, approve with limits, request changes, defer, reject, supersede, escalate, or block. | Source/extract, evidence reviewed, reviewer, rationale, scope, limitations, downstream effect, follow-up owner. | MVP2-AC-004, MVP2-AC-005, MVP2-AC-006, MVP2-AC-007 |
| G2: Knowledge asset promotion | Promote, revise, defer, reject, assign owner, or block. | Target asset, claims, provenance, evidence class, confidence, freshness, applicability, owner, review status, consumption limits. | MVP2-AC-008, MVP2-AC-009, MVP2-AC-010 |
| G3: SME validation | Approve extract/guidance, request SME revision, limit applicability, defer, reject, or escalate. | SME/reviewer role, domain scope, evidence reviewed, guidance, caveats, confidence/freshness, downstream impact. | MVP2-AC-011 |
| G4: Persona behavior change | Approve version, request changes, defer, reject, or escalate. | Persona template/version, changed guidance, source/provenance, reviewer rationale, affected workflows, confidence/freshness impact, limits. | MVP2-AC-012, MVP2-AC-013, MVP2-AC-014, MVP2-AC-016 |
| G5: Consumption readiness | Ready, ready with caveats, review-needed, blocked, or not applicable. | Grounding context, persona instance, caveats, blockers, evidence expectations, escalation instructions, downstream limits. | MVP2-AC-015, MVP2-AC-017, MVP2-AC-018, MVP2-AC-019, MVP2-AC-020 |
| G6: Learning promotion | Promote, investigate, request changes, defer, reject, operational-only, backlog/spike, or not applicable. | Learning item, evidence, recurrence/impact, target, owner, reviewer, rationale, promotion limits, downstream effect. | MVP2-AC-021, MVP2-AC-022, MVP2-AC-023 |
| G7: Audit/governance readiness | Approve audit/governance posture, accept with limits, request changes, needs-spike, defer, or block. | Audit trail summary, source immutability evidence, reviewer/owner coverage, future-scope guard, open governance decisions. | MVP2-AC-024, MVP2-AC-025, MVP2-AC-026, MVP2-AC-027, MVP2-AC-029, MVP2-AC-030 |

## Readiness blocker summary

Any of the following blocks MVP2 product acceptance for the affected scope:

- Acceptance criteria are not testable or reviewable.
- Required SYN-PRD or CAP trace is missing for a product acceptance claim.
- Sources, extracts, knowledge assets, SME guidance, persona templates, persona
  instances, grounding contexts, learning items, or promotion requests lack
  owner, reviewer, evidence, rationale, or status where required.
- Source posture is missing, ambiguous, or conflates approved sources with
  approved extracts, operational-only sources, seed/raw/research sources, future
  candidate sources, rejected sources, superseded sources, or blocked sources.
- Source-backed, inferred, assumed, and open claims are conflated.
- Confidence or freshness labels are missing for material reusable claims.
- Low-confidence, blocked, stale-risk, unknown, superseded, assumed, open,
  conflicting, prohibited, raw, research, runtime, operational-only, SME, or
  future external material grounds committed behavior without review.
- Approved extracts omit source reference, reviewer, evidence reviewed,
  applicability, confidence, freshness, limitations, or approval decision.
- Knowledge assets are reusable without provenance, owner/reviewer, evidence
  class, confidence, freshness, applicability, limitations, review status, or
  promotion state.
- Persona templates lack role boundaries, allowed knowledge, prohibited
  behavior, evidence rules, quality gates, output expectations, escalation
  behavior, owner, reviewer, or version.
- Persona instances do not reference an approved template version or bounded
  grounding context.
- Persona behavior changes or run-specific overrides silently alter reusable
  behavior without source provenance, reviewer rationale, and version/change
  record.
- Grounding context lacks approved assets/extracts, allowed operational
  references, prohibited sources, confidence/freshness expectations, caveats,
  escalation instructions, or handoff requirements.
- AI coworker output drops provenance, uncertainty, source limitations,
  confidence/freshness caveats, or persona boundaries.
- Learning changes knowledge, persona behavior, workflow templates, validators,
  standards, or backlog gates without a promotion decision.
- Required review gates are missing, unresolved, or bypassed.
- Review-only gates lack reviewer role, evidence reviewed, decision, rationale,
  downstream effect, limits, or recovery/follow-up action.
- Material actions cannot be reconstructed through audit trail or equivalent
  correlated records.
- `raw/` or `research/` files are modified, or raw/research content is promoted
  without review into product truth.
- MVP2 acceptance depends on deferred storage, retrieval, embedding, search,
  connector, crawler, sync, prompt-management, provider/runtime, event bus,
  product API, tenancy, access, retention/deletion, privacy/compliance, billing,
  deployment, administration, connector marketplace, legacy bridge, or automated
  approval capabilities.

## Non-goals and tooling boundary

MVP2 acceptance does not require and must not imply acceptance of:

- a runtime knowledge store, vector database, retrieval algorithm, embedding
  model, search index, crawler, synchronization job, source connector, or
  arbitrary ingestion system;
- a prompt-management service, model/provider/runtime choice, product API,
  event bus, telemetry backend, scheduler, workflow-run database, or production
  execution architecture;
- tenancy, access-control, retention/deletion, privacy, compliance, sensitive
  data, billing, deployment, customer administration, or audit implementation;
- a broad external connector marketplace, customer/domain corpus, legacy bridge
  adapter, or every possible expert workflow/persona/domain pack;
- automatic final approval of sources, SME claims, approved extracts, persona
  behavior changes, grounding readiness, risk acceptance, or learning
  promotions;
- direct use of raw, research, runtime, operational-only, or ungoverned external
  material as durable product knowledge;
- customer-facing exposure of repository-only source-grounding docs,
  `.orchestration/` runtime artifacts, generated task cards, runtime memos,
  workflow YAML, Cursor rules, or `cursor_orchestrator` internals as product
  concepts.

## Trace summary

| Requirement or capability | Covered by criteria |
| --- | --- |
| SYN-PRD-001 Governed knowledge assets | MVP2-AC-002 through MVP2-AC-010, MVP2-AC-013, MVP2-AC-017 through MVP2-AC-020, MVP2-AC-026, MVP2-AC-027, MVP2-AC-030 |
| SYN-PRD-002 SME/persona templates | MVP2-AC-011 through MVP2-AC-020, MVP2-AC-026, MVP2-AC-030 |
| SYN-PRD-003 Workflow design surface | MVP2-AC-023, MVP2-AC-029 |
| SYN-PRD-005 Human review and approval | MVP2-AC-003, MVP2-AC-006 through MVP2-AC-008, MVP2-AC-011, MVP2-AC-014, MVP2-AC-016, MVP2-AC-018, MVP2-AC-022, MVP2-AC-024 through MVP2-AC-027, MVP2-AC-029, MVP2-AC-030 |
| SYN-PRD-006 Feedback and learning | MVP2-AC-021 through MVP2-AC-023, MVP2-AC-026, MVP2-AC-030 |
| SYN-PRD-009 Human accountability | MVP2-AC-001 through MVP2-AC-030 |
| SYN-PRD-010 Domain-agnostic packaging and product boundary | MVP2-AC-001, MVP2-AC-028 through MVP2-AC-030 |
| CAP-001 Workflow authoring experience | MVP2-AC-023 |
| CAP-002 Task packet generation | MVP2-AC-015, MVP2-AC-017 through MVP2-AC-020 |
| CAP-003 Canonical knowledge registry | MVP2-AC-001 through MVP2-AC-010, MVP2-AC-013, MVP2-AC-017 through MVP2-AC-020, MVP2-AC-023, MVP2-AC-026 through MVP2-AC-030 |
| CAP-004 SME/persona template system | MVP2-AC-001, MVP2-AC-011 through MVP2-AC-020, MVP2-AC-023, MVP2-AC-026, MVP2-AC-028 through MVP2-AC-030 |
| CAP-005 Human approval and governance | MVP2-AC-003, MVP2-AC-006 through MVP2-AC-008, MVP2-AC-011, MVP2-AC-014, MVP2-AC-016, MVP2-AC-018, MVP2-AC-022, MVP2-AC-024 through MVP2-AC-027, MVP2-AC-029, MVP2-AC-030 |
| CAP-007 Feedback and learning promotion | MVP2-AC-021 through MVP2-AC-023, MVP2-AC-026, MVP2-AC-029, MVP2-AC-030 |
| CAP-008 Integration and event contracts boundary | MVP2-AC-029 |
| CAP-010 Product packaging and administration boundary | MVP2-AC-029 |

