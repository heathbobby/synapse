# Synapse Product MVP2: Knowledge and Persona Contracts

- **Status**: technical-architect draft
- **MVP**: MVP2
- **Last updated**: 2026-05-04
- **Companion capability spec**: `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md`
- **Companion workflow spec**: `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md`
- **Primary sources**:
  - `docs/refinement/iteration-inputs/product-mvp2-knowledge-persona-layer.md`
  - `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md`
  - `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md`
  - `docs/MVP2/Knowledge/GroundingModel.md`
  - `docs/MVP2/Knowledge/SourceInventory.md`
  - `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`

## Purpose

This document defines the product-logical contracts for the MVP2 knowledge and
persona layer. The contracts describe the objects Synapse must reason about when
approved sources, SME guidance, and workflow learnings become governed knowledge
assets, reusable persona behavior, grounding context, and review decisions.

The contracts are intentionally implementation-neutral. They define identifiers,
states, relationships, transition rules, validation/readiness rules, governance
rules, and audit expectations without selecting storage, retrieval, embeddings,
source connectors, providers, tenancy, deployment, runtime mechanics, UI, or
compliance implementation.

## Contract principles

1. **Knowledge changes are governed behavior changes**: A source, extract,
   claim, learning, or persona update becomes reusable only after the required
   owner and reviewer decisions are recorded.
2. **Provenance travels with meaning**: Source references, evidence class,
   confidence, freshness, applicability, limitations, reviewer rationale, and
   promotion state must remain visible as claims become assets or persona
   guidance.
3. **Uncertainty is first-class**: Inferred, assumed, open, stale-risk,
   unknown, low-confidence, blocked, conflicting, or operational-only material
   must remain visible and must not become committed reusable behavior by
   transformation.
4. **Persona templates are product assets**: Reusable AI coworker role behavior
   must be versioned, source-backed or reviewed, bounded by allowed knowledge,
   and governed by escalation rules.
5. **Learning promotion is explicit**: Completed-run lessons may create
   learning signals and promotion requests, but they must not silently alter
   knowledge assets, persona templates, workflow templates, validators,
   standards, or backlog gates.
6. **Implementation decisions remain open**: Product contracts classify
   knowledge and governance needs; they do not choose future technical,
   operational, deployment, or administrative mechanisms.

## Shared vocabularies

### Identifier expectations

All product contracts should carry stable logical identifiers. An identifier is
stable within the product history and review trail, but this document does not
define how identifiers are generated, stored, resolved, or displayed.

| Identifier type | Applies to | Product expectation |
| --- | --- | --- |
| Contract ID | All major records | Unique logical reference for review, relationship mapping, and audit trail. |
| Version ID | Versioned assets and templates | Distinguishes materially different approved or reviewed states. |
| Source reference ID | Source references and claims | Points to the source path, decision ID, extract ID, SME review record, runtime reference, or future source reference without embedding source material. |
| Owner role ID | Governed records | Names the accountable role for correctness, freshness, applicability, and follow-up. |
| Reviewer role ID | Review decisions and governed updates | Names the role that approved, limited, rejected, deferred, superseded, or escalated the item. |
| Promotion request ID | Learning, extract, claim, and behavior changes | Connects a proposed reusable change to its evidence, target, decision, and audit trail. |
| Audit record ID | All material transitions | Connects a transition to actor role, rationale, affected records, and follow-up. |

### Source posture

| Posture | Meaning | Contract consequence |
| --- | --- | --- |
| Approved source | Reviewed canonical source accepted for stated scope. | May ground claims within applicability, confidence, and freshness limits. |
| Approved extract | Reviewed bounded summary promoted from raw, operational, SME, or future candidate evidence. | May ground claims within the approved extract's scope and limitations. |
| Operational-only | Useful for traceability, recovery, or promotion proposal but not durable truth. | Cannot ground reusable assets or persona behavior without promotion. |
| Seed source | Immutable original/raw/research context used only for bounded source review. | Cannot directly ground implementation, reusable knowledge, or persona behavior. |
| Future candidate | External, legacy, customer, SME, or system source without accepted boundaries. | Discovery only until owner, authority, governance posture, and promotion rules are accepted. |

### Evidence class

| Evidence class | Meaning | Contract consequence |
| --- | --- | --- |
| Source-backed | Directly supported by an approved source or approved extract. | May support approved reusable behavior within scope. |
| Inferred | Reasonably derived from approved sources but not directly stated. | May guide draft or caveated work; behavior-affecting reuse requires review. |
| Assumed | Needed to proceed but not validated. | Must remain an assumption with owner, validation need, and risk. |
| Open | Unknown or awaiting product, SME, governance, architecture, owner, or stakeholder decision. | Cannot ground committed behavior; must route to decision, review, or spike. |

### Confidence

| Confidence | Meaning | Contract consequence |
| --- | --- | --- |
| High | Approved source or extract, clear scope, current/recent freshness, no known conflict. | Eligible for reusable grounding within stated limits. |
| Medium | Approved basis with interpretation, dependency, older freshness, partial review, or bounded assumption. | Eligible with caveat; behavior changes may need additional review. |
| Low | Operational, seed, stale-risk, unknown, incomplete, or unpromoted basis. | Discovery, hypothesis, caveat, or promotion proposal only. |
| Blocked | Depends on unresolved owner, source, SME, governance, product, architecture, or implementation decision. | Cannot ground committed behavior; must be escalated or deferred. |

### Freshness

| Freshness | Meaning | Contract consequence |
| --- | --- | --- |
| Current | Reviewed for the current iteration or explicitly confirmed valid. | Eligible for high-confidence use when other gates pass. |
| Recent | Accepted earlier with no known superseding decision. | Confirm no conflict before high-confidence reusable use. |
| Stale-risk | May be outdated due to newer decisions, review gaps, or domain change. | Requires owner/reviewer confirmation before reusable reliance. |
| Superseded | Replaced by a newer approved source, claim, asset, or decision. | Historical reference only; cite the replacement. |
| Unknown | Review date, owner, or applicability is unclear. | Treat as low confidence or open until clarified. |

### Lifecycle state

These states apply to sources, extracts, claims, knowledge assets, persona
templates, promotion requests, learning signals, and governance records where
appropriate.

| State | Meaning | Downstream use |
| --- | --- | --- |
| Candidate | Item is identified but not fully classified or reviewed. | Discovery only. |
| Proposed | Claim, source, owner, target, and intended use are recorded. | Review input only. |
| Review-needed | Human, SME, standards, product, governance, or owner decision is required. | Blocks reusable behavior changes. |
| Approved | Reviewer accepted scope, evidence, confidence, freshness, and limits. | May ground future work within stated limits. |
| Approved-with-limits | Reviewer accepted restricted use, caveats, or lower-confidence treatment. | May be consumed only with visible caveats and scope limits. |
| Operational-only | Useful for traceability or recovery but not durable truth. | Cannot ground reusable behavior. |
| Deferred | Decision postponed pending missing input, owner, SME, governance, or product decision. | Blocks reliance until resolved. |
| Superseded | Replaced by newer approved source, extract, claim, asset, template, or decision. | Historical reference only. |
| Rejected | Reviewer rejected source, claim, promotion, or behavior change. | Do not consume except as limitation or risk context. |
| Blocked | Missing owner, unresolved conflict, governance issue, or insufficient evidence prevents progress. | Escalate or create follow-up; no committed reuse. |

`Request-changes`, `escalate`, and `not-applicable` are review outcomes rather
than durable lifecycle states unless a later product decision promotes them into
the shared state vocabulary.

## Contract object model

### KnowledgeAsset

**Definition**: A reusable governed knowledge unit that packages approved claims,
provenance, owner accountability, applicability, confidence, freshness,
limitations, review state, and consumption boundaries for workflows or personas.

**Required identifiers**

- `knowledge_asset_id`
- `version_id`
- `owner_role_id`
- `reviewer_role_id` when approved, limited, superseded, rejected, or deferred
- related `source_reference_ids`
- related `grounded_claim_ids`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Title and summary | Human-readable description of the reusable knowledge unit. |
| Asset kind | Requirement, architecture, workflow, persona, operational, SME/domain, learning, standard, validator, backlog gate, or approved extract package. |
| Claims | One or more `GroundedClaim` records or approved claim summaries. |
| Source references | Approved source or approved extract references required for reusable reliance. |
| Owner | Role accountable for correctness, applicability, freshness, and limitations. |
| Reviewer | Role that accepted the asset or latest material state transition. |
| Applicability | Workflows, domains, personas, decisions, or targets where the asset may be used. |
| Limitations | Caveats, assumptions, excluded uses, open questions, stale markers, and future-scope exclusions. |
| Confidence | Highest allowed confidence for asset consumption, never higher than its weakest material claim without reviewer rationale. |
| Freshness | Current, recent, stale-risk, superseded, or unknown. |
| Lifecycle state | Candidate through blocked, using the shared lifecycle states. |
| Promotion state | Whether the asset is candidate, proposed, review-needed, approved, approved-with-limits, operational-only, deferred, superseded, rejected, or blocked. |
| Downstream consumers | Personas, workflows, grounding contexts, validators, standards, or backlog gates allowed to consume the asset. |

**Relationship rules**

- A `KnowledgeAsset` must reference at least one approved source, approved
  extract, or approved review decision before it can be `Approved`.
- A `KnowledgeAsset` may contain multiple `GroundedClaim` records, but each
  material claim must retain source references, evidence class, confidence,
  freshness, applicability, and limitations.
- A `KnowledgeAsset` may be consumed by a `PersonaTemplate` only when the
  persona's allowed knowledge scope includes the asset and all persona behavior
  gates pass.
- A `KnowledgeAsset` may be included in a `GroundingContext` only when its state,
  confidence, freshness, applicability, and governance limits satisfy that
  context's readiness rules.
- A superseded asset must point to the replacing asset, claim, extract, or
  decision when known.

**Transition rules**

| From | To | Required condition |
| --- | --- | --- |
| Candidate | Proposed | Source posture, owner, intended use, and preliminary claim scope are recorded. |
| Proposed | Review-needed | Reviewer, review need, open questions, or missing evidence is identified. |
| Proposed or Review-needed | Approved | Reviewer accepts evidence, claims, scope, confidence, freshness, applicability, and limitations. |
| Proposed or Review-needed | Approved-with-limits | Reviewer accepts restricted use, caveats, or lower-confidence consumption rules. |
| Any non-final state | Deferred | Required owner, SME, source, governance, or product input is not yet available. |
| Any non-final state | Blocked | A missing owner, unresolved conflict, prohibited source reliance, or open decision prevents safe reliance. |
| Any non-final state | Rejected | Reviewer rejects the asset for reusable grounding and records rationale. |
| Approved or Approved-with-limits | Superseded | Newer approved asset, extract, claim, or decision replaces the asset. |

**Readiness rules**

A `KnowledgeAsset` is consumption-ready only when:

- it is `Approved` or `Approved-with-limits`;
- material claims are source-backed or reviewed inferred claims;
- low-confidence, blocked, assumed, open, stale-risk, unknown, operational-only,
  or seed-source material is preserved as caveat, limitation, review need, or
  escalation trigger;
- source references, owner, reviewer, applicability, confidence, freshness, and
  limitations are present;
- any persona, workflow, or governance-specific consumption limits are visible;
- any supersession or conflict is resolved or marked as a blocker.

### SourceReference

**Definition**: A product reference to the source behind a claim, extract,
review, asset, persona instruction, or learning signal.

**Required identifiers**

- `source_reference_id`
- `source_id_or_path`
- `owner_role_id`
- optional `reviewer_role_id`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Source class | Canonical product/requirements, architecture/decisions, MVP1 platform, work item/roadmap, standard, reviewed configuration, reviewed input packet, operational evidence, seed source, future candidate, or SME/review evidence. |
| Source posture | Approved source, approved extract, operational-only, seed source, or future candidate. |
| Source status | Current lifecycle state for this source's use in MVP2. |
| Authority scope | What the source may and may not ground. |
| Owner role | Role accountable for source correctness or promotion path. |
| Last-reviewed marker | Review date, iteration, decision, or explicit unknown marker. |
| Freshness | Current, recent, stale-risk, superseded, or unknown. |
| Limitations | Source gaps, authority limits, open decisions, stale markers, and prohibited uses. |

**Relationship rules**

- `SourceReference` may support many `GroundedClaim`, `ApprovedExtract`,
  `KnowledgeAsset`, `PersonaTemplate`, `GroundingContext`, and `ReviewDecision`
  records.
- Operational-only, seed, and future candidate references may support discovery,
  recovery, or promotion proposals but must not directly approve reusable
  knowledge or persona behavior.
- A superseded source reference must identify the superseding reference or record
  an open follow-up when the replacement is unknown.

**Transition rules**

| From | To | Required condition |
| --- | --- | --- |
| Candidate | Proposed | Source class, source posture, owner, authority scope, and intended use are recorded. |
| Proposed | Review-needed | Source authority, freshness, owner, reviewer, governance posture, or limitations require decision. |
| Proposed or Review-needed | Approved | Reviewer accepts the source reference for a stated scope, freshness, confidence posture, and limits. |
| Proposed or Review-needed | Approved-with-limits | Reviewer accepts restricted use, caveats, or lower-confidence treatment. |
| Any active state | Operational-only | Source is useful for traceability, recovery, or promotion proposals but not durable grounding. |
| Any active state | Deferred or Blocked | Required owner, authority, governance, freshness, or conflict resolution is missing. |
| Approved or Approved-with-limits | Superseded | Newer approved source, extract, claim, or decision replaces this reference for reusable reliance. |
| Any active state | Rejected | Reviewer rejects the source reference for the proposed grounding use. |

**Readiness rules**

A `SourceReference` is reusable-grounding-ready only when source class, source
posture, owner, authority scope, freshness, and limitations are known and the
posture is approved source or approved extract.

### ApprovedExtract

**Definition**: A reviewed bounded summary of raw, research, runtime, SME,
operational, or future candidate evidence that has been promoted for reuse
within a stated scope.

**Required identifiers**

- `approved_extract_id`
- `version_id`
- source `source_reference_ids`
- `owner_role_id`
- `reviewer_role_id`
- related `review_decision_id`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Extract summary | Bounded statement of what was approved. |
| Original source references | References to source material or source families without requiring wholesale promotion. |
| Evidence class | Source-backed, inferred, assumed, or open per approved statement. |
| Confidence | High, medium, low, or blocked with rationale. |
| Freshness | Current, recent, stale-risk, superseded, or unknown. |
| Applicability | Where the extract may ground work. |
| Limitations | What the extract excludes, caveats, source gaps, and open questions. |
| Reviewer rationale | Why the extract is acceptable, limited, deferred, rejected, superseded, or blocked. |
| Lifecycle state | Shared lifecycle state. |

**Relationship rules**

- An `ApprovedExtract` may become evidence for one or more `GroundedClaim` or
  `KnowledgeAsset` records.
- An `ApprovedExtract` may support persona guidance only when role applicability
  and behavior impact are reviewed.
- An `ApprovedExtract` must preserve original source posture and limitations.
  Promotion of an extract does not promote the entire original source family.

**Transition rules**

- Candidate extract proposals become `Proposed` after source references, claim
  summary, owner, and target are recorded.
- Extracts become `Approved` or `Approved-with-limits` only through
  `ReviewDecision`.
- Extracts become `Superseded` when a newer extract, approved source, asset, or
  decision replaces their reusable meaning.

**Readiness rules**

An `ApprovedExtract` is ready to ground reusable behavior only when reviewer,
source references, extract scope, evidence class, confidence, freshness,
applicability, limitations, and decision rationale are present.

### GroundedClaim

**Definition**: A specific reusable fact, rule, constraint, recommendation,
assumption, caveat, or open question with attached provenance and governance
signals.

**Required identifiers**

- `grounded_claim_id`
- source `source_reference_ids`
- optional `approved_extract_id`
- optional parent `knowledge_asset_id`
- `owner_role_id`
- `reviewer_role_id` when reviewed
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Claim text | Clear claim, rule, constraint, assumption, or open question. |
| Claim type | Fact, rule, constraint, assumption, limitation, open question, decision, instruction, or learning. |
| Evidence class | Source-backed, inferred, assumed, or open. |
| Confidence | High, medium, low, or blocked with rationale. |
| Freshness | Current, recent, stale-risk, superseded, or unknown. |
| Applicability | Where the claim may be used. |
| Limitations | Known uncertainty, excluded scope, caveats, and future-scope boundaries. |
| Conflicts | Related claims, sources, assets, or decisions that conflict or supersede. |
| Lifecycle state | Shared lifecycle state. |

**Relationship rules**

- A `GroundedClaim` must have at least one source reference, even when the claim
  is assumed or open.
- A claim may belong to multiple `KnowledgeAsset` or `PersonaTemplate` records
  only when each consumer preserves evidence, confidence, freshness, and
  limitations.
- Claims with `Assumed` or `Open` evidence class cannot be converted into
  persona instructions except as caveats, prohibitions, validation needs, or
  escalation triggers.
- Conflicting claims block high-confidence reuse until a reviewer resolves,
  limits, supersedes, or defers the conflict.

**Transition rules**

- `Candidate` to `Proposed` requires claim text, source references, owner, and
  intended target.
- `Proposed` to `Approved` requires reviewer acceptance of evidence,
  confidence, freshness, applicability, and limitations.
- `Approved` to `Superseded` requires a newer approved claim, extract, asset, or
  decision.
- Any state may become `Blocked` when a required decision, source owner, reviewer,
  or governance issue prevents safe reliance.

**Readiness rules**

A `GroundedClaim` may support committed reusable behavior only when it is
source-backed or reviewed inferred, high or medium confidence, current or recent
or reviewer-confirmed stale-risk, and approved or approved-with-limits.

### PersonaTemplate

**Definition**: A reusable governed AI coworker role definition that packages
role purpose, expertise boundary, responsibilities, allowed knowledge,
prohibited behavior, evidence rules, confidence/freshness expectations, output
standards, escalation behavior, review expectations, and version history.

**Required identifiers**

- `persona_template_id`
- `version_id`
- `owner_role_id`
- `reviewer_role_id` for approved versions and behavior-affecting changes
- related `knowledge_asset_ids`
- related `grounded_claim_ids`
- related `governance_policy_ids`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Role purpose | What the AI coworker is meant to accomplish. |
| Expertise boundary | What the persona is qualified to reason about and what is out of scope. |
| Responsibilities | Expected duties, handoffs, and completion signals. |
| Allowed knowledge | Approved assets, extracts, source classes, or grounding contexts the persona may consume. |
| Prohibited behavior | Actions, claims, source classes, or decisions the persona must not perform or assert. |
| Evidence rules | How source-backed, inferred, assumed, and open claims must be handled. |
| Confidence rules | Thresholds for committed output, caveats, draft-only treatment, and escalation. |
| Freshness rules | Required freshness posture and stale/unknown handling. |
| Output standards | Required preservation of provenance, assumptions, open questions, limitations, validation status, and handoff needs. |
| Escalation behavior | Conditions that require human, SME, owner, product, governance, or reviewer escalation. |
| Lifecycle state | Shared lifecycle state for the template version. |

**Relationship rules**

- A `PersonaTemplate` may reference only approved or approved-with-limits
  `KnowledgeAsset`, `ApprovedExtract`, and `GroundedClaim` records as reusable
  role behavior.
- A `PersonaTemplate` may mention low-confidence, stale-risk, assumed, open, or
  blocked material only as caveats, validation needs, prohibitions, or
  escalation triggers.
- A persona behavior change must connect to a `ReviewDecision` and `AuditRecord`
  when it changes role responsibilities, allowed knowledge, prohibited behavior,
  evidence rules, output standards, or escalation behavior.
- A persona template must not override the grounding context supplied for a
  specific workflow run or AI coworker task.

**Transition rules**

| From | To | Required condition |
| --- | --- | --- |
| Candidate | Proposed | Role purpose, owner, intended use, and initial knowledge scope are recorded. |
| Proposed | Review-needed | Evidence, behavior impact, owner, SME, standards, or governance review is needed. |
| Review-needed | Approved | Reviewer accepts role behavior, allowed knowledge, evidence rules, limits, and escalation behavior. |
| Review-needed | Approved-with-limits | Reviewer accepts bounded use, required caveats, or limited workflow/persona scope. |
| Approved | Superseded | New version is approved and replaces prior behavior. |
| Any non-final state | Blocked | Required provenance, owner, reviewer, or governance decision is missing. |
| Any non-final state | Rejected | Reviewer rejects the reusable role behavior or change. |

**Readiness rules**

A `PersonaTemplate` is instantiation-ready only when:

- its current version is `Approved` or `Approved-with-limits`;
- role purpose, responsibilities, allowed knowledge, prohibited behavior,
  evidence rules, confidence/freshness rules, output expectations, and escalation
  behavior are present;
- behavior-affecting guidance is supported by approved or approved-with-limits
  knowledge, extracts, or review decisions;
- unresolved implementation, governance, source, owner, or SME questions are
  preserved as prohibitions, blockers, or escalation triggers;
- required governance policies are satisfied or explicitly not applicable with
  rationale.

### PersonaInstance

**Definition**: A bounded use of an approved persona template for a specific
workflow, task, run, review, or operator-assigned role context.

**Required identifiers**

- `persona_instance_id`
- parent `persona_template_id`
- template `version_id`
- related `grounding_context_id`
- `owner_role_id` or operator-assigned accountable role
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Instantiation purpose | Workflow, task, review, or role assignment being served. |
| Template version | Approved template version in effect. |
| Grounding context | Bounded approved context supplied to the instance. |
| Active caveats | Limits, stale-risk items, approved-with-limits items, assumptions, or open questions that must be preserved. |
| Escalation triggers | Persona and context-specific conditions requiring review or pause. |
| Output obligations | Required citations, assumptions, open questions, validation notes, handoff details, and learning proposals. |
| Readiness state | Ready, ready-with-caveats, review-needed, deferred, blocked, completed, or cancelled. |

**Relationship rules**

- A `PersonaInstance` must reference exactly one approved or
  approved-with-limits `PersonaTemplate` version.
- A `PersonaInstance` must reference one `GroundingContext` for its bounded
  consumption scope.
- A `PersonaInstance` must not expand allowed knowledge beyond the grounding
  context or template boundaries.
- A `PersonaInstance` may produce `LearningSignal` records when repeated gaps,
  ambiguity, source drift, validation failures, or useful recovery patterns
  appear.

**Transition rules**

- `Proposed` to `Ready` requires approved template version and ready grounding
  context.
- `Proposed` to `Ready-with-caveats` requires all caveats and escalation triggers
  to be visible and accepted for the task purpose.
- Any state to `Blocked` requires a recorded blocker, owner, and follow-up.
- `Ready` or `Ready-with-caveats` to `Completed` requires output obligations and
  handoff expectations to be satisfied or explicitly marked incomplete with
  rationale.

**Readiness rules**

A `PersonaInstance` is dispatch-ready only when selected template, grounding
context, allowed knowledge, prohibited sources, confidence/freshness rules,
caveats, escalation triggers, and output obligations are aligned.

### GroundingContext

**Definition**: A bounded approved context package supplied to a workflow run,
persona instance, AI coworker task, review gate, or handoff.

**Required identifiers**

- `grounding_context_id`
- related workflow/task/run reference when applicable
- related `persona_template_id` or `persona_instance_id` when applicable
- related `knowledge_asset_ids`
- related `source_reference_ids`
- `owner_role_id`
- `reviewer_role_id` when readiness is reviewed
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Purpose | Workflow, task, role, review, or handoff that the context supports. |
| Required approved assets | Knowledge assets or extracts required for consumption. |
| Allowed operational references | Operational-only evidence allowed for traceability, recovery, or promotion proposal only. |
| Prohibited sources | Source classes, paths, candidates, or evidence types that must not ground output. |
| Evidence expectations | Required treatment of source-backed, inferred, assumed, and open claims. |
| Confidence threshold | Minimum confidence for committed claims and handling of low/blocked items. |
| Freshness expectation | Required freshness posture and stale/unknown handling. |
| Applicability boundaries | Workflows, domains, personas, decisions, or outputs in scope. |
| Caveats and limitations | Required caveats, approved-with-limits terms, assumptions, and open questions. |
| Handoff requirements | What the consumer must preserve or report. |
| Readiness state | Ready, ready-with-caveats, review-needed, deferred, blocked, superseded, or rejected. |

**Relationship rules**

- A `GroundingContext` may include approved and approved-with-limits assets,
  approved extracts, and source references within scope.
- Operational-only references may be included only when clearly marked for
  traceability, recovery, or promotion proposals.
- A `GroundingContext` must not authorize use that the selected
  `PersonaTemplate`, governance policy, or asset applicability prohibits.
- A grounding context may create or reference `ReviewDecision` records when
  consumption readiness is caveated, deferred, blocked, or escalated.

**Transition rules**

- `Candidate` to `Proposed` requires purpose, owner, candidate assets, source
  posture, and intended consumers.
- `Proposed` to `Ready` requires all required assets/templates to be approved,
  applicable, sufficiently fresh, and above the confidence threshold.
- `Proposed` to `Ready-with-caveats` requires reviewer or owner acceptance of
  visible caveats and limits.
- `Proposed` or `Review-needed` to `Blocked` requires unresolved missing source,
  owner, reviewer, conflict, prohibited source reliance, or governance issue.
- `Ready` or `Ready-with-caveats` to `Superseded` requires a newer grounding
  context or decision replacing it.

**Readiness rules**

A `GroundingContext` is ready only when approved assets, allowed operational
references, prohibited sources, evidence expectations, confidence threshold,
freshness expectation, applicability boundaries, caveats, escalation triggers,
and handoff requirements are explicit and internally consistent.

### PromotionRequest

**Definition**: A proposal to turn a source, extract, claim, SME input,
operational finding, learning signal, or review insight into reusable product
behavior.

**Required identifiers**

- `promotion_request_id`
- candidate `source_reference_ids`
- optional `learning_signal_id`
- proposed target record ID or target type
- `owner_role_id`
- `reviewer_role_id` when assigned
- related `review_decision_id`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Candidate summary | Proposed reusable change or approved extract. |
| Candidate source posture | Approved source, approved extract, operational-only, seed, or future candidate. |
| Proposed target | Knowledge asset, approved extract, persona template, workflow template, validator, standard, backlog gate, or product decision. |
| Evidence class | Source-backed, inferred, assumed, or open. |
| Confidence and rationale | Expected confidence and why. |
| Freshness | Freshness posture of supporting evidence. |
| Applicability | Where the change would apply. |
| Downstream impact | Assets, personas, workflows, standards, validators, or backlog gates affected. |
| Required reviewers | Owner, SME, product, standards, governance, or other role needed for decision. |
| Decision outcome | Approved, approved-with-limits, request-changes, defer, reject, supersede, escalate, or blocked. |

**Relationship rules**

- A `PromotionRequest` may target only one primary reusable change, though it may
  list secondary impacted records.
- A promotion request that changes persona behavior must reference the affected
  persona template and required behavior review roles.
- A promotion request based on operational-only, seed, or future candidate
  evidence must not update reusable behavior until an approving
  `ReviewDecision` exists.
- A rejected or deferred request remains useful as risk, limitation, or future
  decision context but cannot be consumed as approved knowledge.

**Transition rules**

| From | To | Required condition |
| --- | --- | --- |
| Candidate | Proposed | Candidate summary, source references, target, owner, evidence class, confidence, freshness, and limitations are recorded. |
| Proposed | Review-needed | Reviewer or SME/governance/product decision is required. |
| Review-needed | Approved | Reviewer accepts target, scope, evidence, confidence, freshness, and downstream impact. |
| Review-needed | Approved-with-limits | Reviewer accepts restricted use or required caveats. |
| Review-needed | Request-changes | Reviewer requires revision before decision. |
| Review-needed | Deferred | Required input or decision is not yet available. |
| Review-needed | Rejected | Reviewer rejects promotion with rationale. |
| Any active state | Blocked | Missing owner, prohibited source reliance, unresolved conflict, or governance issue prevents progress. |

**Readiness rules**

A `PromotionRequest` is decision-ready only when it identifies candidate source,
proposed change, target, owner, required reviewers, source posture, evidence
class, confidence, freshness, applicability, limitations, downstream impact, and
open decisions.

### ReviewDecision

**Definition**: A human, SME, product, standards, owner, or governance decision
that changes the review state, promotion state, consumption readiness, or
behavioral authority of another contract object.

**Required identifiers**

- `review_decision_id`
- reviewed record ID and record type
- `reviewer_role_id`
- optional `owner_role_id`
- related `source_reference_ids`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Decision type | Approve, approve-with-limits, request-changes, defer, reject, supersede, escalate, block, or mark not-applicable. |
| Reviewer role | Accountable role making the decision. |
| Evidence reviewed | Sources, extracts, claims, SME notes, learning signals, validation results, assumptions, or open questions. |
| Rationale | Why the decision was made. |
| Limits of approval | Scope, caveats, confidence/freshness constraints, and prohibited uses. |
| Affected downstream work | Assets, personas, workflows, standards, validators, backlog gates, or grounding contexts affected. |
| Follow-up owner | Role accountable for unresolved issues or requested changes. |
| Effective state | State assigned to the reviewed record after the decision. |

**Relationship rules**

- A `ReviewDecision` must reference the record it governs.
- A `ReviewDecision` may approve, limit, reject, supersede, defer, escalate, or
  block multiple related downstream records only when each affected record is
  explicitly named.
- Review decisions may raise or lower confidence only with rationale and
  preserved evidence.
- Review decisions cannot erase prior audit records, limitations, source posture,
  or superseded history.

**Transition rules**

- A decision is `Proposed` while evidence is being assembled.
- A decision becomes `Approved`, `Approved-with-limits`, `Deferred`,
  `Rejected`, `Superseded`, or `Blocked` when the reviewer records outcome,
  rationale, limits, affected records, and follow-up.
- A decision may be superseded by a later decision but remains part of the audit
  trail.

**Readiness rules**

A `ReviewDecision` is valid only when reviewer role, evidence reviewed,
decision outcome, rationale, limits, affected downstream records, and follow-up
owner or not-applicable rationale are present.

### LearningSignal

**Definition**: A candidate reusable improvement discovered from workflow
execution, review decisions, repeated revisions, blockers, handoff feedback,
stale-source issues, persona ambiguity, validation gaps, or recovery patterns.

**Required identifiers**

- `learning_signal_id`
- source or runtime `source_reference_ids`
- optional `persona_instance_id`
- optional `grounding_context_id`
- `owner_role_id`
- optional `promotion_request_id`
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Signal summary | What was observed and why it may matter. |
| Signal type | Source drift, missing provenance, validation gap, blocked approval, persona ambiguity, role-boundary issue, workflow gap, repeated revision, recovery pattern, backlog blocker, or other governed learning. |
| Evidence | Sources, run references, review notes, handoff feedback, or repeated issue examples. |
| Recurrence or impact | Whether this is repeated, high-impact, or a one-time observation. |
| Proposed target | Knowledge asset, persona template, workflow template, validator, standard, backlog gate, product decision, or no reusable target. |
| Owner | Role accountable for triage and promotion path. |
| Confidence | Confidence that this is a reusable learning rather than one-time noise. |
| Lifecycle state | Shared lifecycle state. |

**Relationship rules**

- A `LearningSignal` may create a `PromotionRequest` only after owner, target,
  evidence, impact, and review need are recorded.
- A learning signal must remain operational-only until promoted through a review
  decision.
- Repeated grounding failures should route toward standards, persona, workflow,
  validator, or backlog updates rather than remaining isolated notes.

**Transition rules**

- `Candidate` to `Proposed` requires summary, evidence, owner, impact, and
  proposed target or explicit no-target rationale.
- `Proposed` to `Review-needed` requires reusable behavior impact or missing
  reviewer input.
- `Review-needed` to `Approved` or `Approved-with-limits` creates or updates the
  related promotion request outcome.
- `Proposed` or `Review-needed` to `Rejected` requires rationale that the signal
  is not reusable or not product-relevant.
- Any active state may become `Deferred` or `Blocked` when owner, evidence,
  governance, or target decisions are missing.

**Readiness rules**

A `LearningSignal` is promotion-ready only when evidence, recurrence or impact,
owner, proposed target, confidence, limitations, and required reviewer roles are
recorded.

### GovernancePolicy

**Definition**: A product-level rule or gate that constrains how knowledge,
sources, claims, persona behavior, promotion, learning, review, and audit records
may be used.

**Required identifiers**

- `governance_policy_id`
- `version_id`
- `owner_role_id`
- `reviewer_role_id` for approved policy versions
- related `audit_record_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Policy purpose | What risk, quality bar, or review boundary the policy governs. |
| Scope | Object types, source classes, workflows, personas, or promotion targets affected. |
| Rule statement | Product-level requirement, prohibition, gate, or escalation condition. |
| Required evidence | Fields, review records, source posture, confidence, freshness, or decision records needed to satisfy the policy. |
| Enforcement expectation | Block, caveat, review-needed, escalation, or not-applicable rationale. |
| Exceptions | Allowed exception path, reviewer role, rationale, and audit expectation. |
| Lifecycle state | Shared lifecycle state for policy version. |

**Relationship rules**

- Governance policies may apply to any contract object.
- A policy may block readiness without selecting how the block is technically
  enforced.
- A policy exception must create a `ReviewDecision` or `AuditRecord` with
  reviewer role, rationale, limits, and follow-up.
- Governance policies must preserve future implementation decisions as open
  blockers rather than assuming controls.

**Transition rules**

- `Candidate` to `Proposed` requires purpose, scope, owner, and rule statement.
- `Proposed` to `Review-needed` requires affected owner, standards, product, SME,
  or governance review.
- `Review-needed` to `Approved` requires reviewer acceptance of scope, rule,
  evidence, exception path, and readiness effect.
- `Approved` to `Superseded` requires a newer approved policy version or
  decision.

**Readiness rules**

A `GovernancePolicy` is applicable only when scope, rule statement, evidence
expectation, readiness effect, owner, reviewer, and exception handling are
defined.

### AuditRecord

**Definition**: A durable product history record for material lifecycle changes,
review decisions, promotions, persona behavior changes, governance exceptions,
supersession, rejection, deferral, blockers, and consumption readiness decisions.

**Required identifiers**

- `audit_record_id`
- affected record ID and record type
- `actor_role_id`
- optional `review_decision_id`
- optional `promotion_request_id`
- related `source_reference_ids`

**Required properties**

| Property | Product expectation |
| --- | --- |
| Event summary | What changed or was decided. |
| Actor role | Role that performed or recorded the change. |
| Prior state | State before the change, when applicable. |
| New state | State after the change, when applicable. |
| Rationale | Reason for change, including limits and caveats. |
| Evidence references | Sources, claims, extracts, decisions, learning signals, or validation results considered. |
| Affected records | Downstream assets, personas, workflows, grounding contexts, standards, validators, or backlog gates affected. |
| Follow-up | Owner, due decision, review need, blocker, or not-applicable rationale. |

**Relationship rules**

- Every material state transition must create or reference an `AuditRecord`.
- Audit records must preserve superseded, rejected, deferred, blocked, and
  approved-with-limits history.
- Audit records must not convert operational-only evidence into approved
  knowledge; they record what happened and may support promotion requests.
- Audit records should be sufficient for a reviewer to reconstruct why a claim,
  asset, persona behavior, grounding context, or promotion state was allowed,
  limited, blocked, or rejected.

**Transition rules**

- An `AuditRecord` is created when a material transition, review decision,
  promotion decision, governance exception, readiness decision, supersession,
  rejection, deferral, or blocker is recorded.
- If an audit record is later found incomplete or incorrect, a follow-up
  `AuditRecord` should correct or supersede the prior record with rationale
  rather than erasing product history.
- Audit history for approved, approved-with-limits, superseded, rejected,
  deferred, and blocked records remains traceable even when the governed object's
  current state changes.

**Audit expectations by event**

| Event | Required audit content |
| --- | --- |
| Source or extract approval | Reviewer, evidence reviewed, decision, scope, limits, confidence, freshness, and follow-up. |
| Knowledge asset promotion | Asset, claims, provenance, owner, reviewer, affected consumers, and limitations. |
| Persona behavior change | Template version, changed guidance, sources, reviewer rationale, affected workflows, caveats, and escalation changes. |
| Grounding context readiness | Selected assets, persona version, prohibited sources, caveats, confidence/freshness posture, and dispatch decision. |
| Learning promotion | Signal, evidence, recurrence/impact, target, owner, reviewer, decision, and downstream update. |
| Governance exception | Policy, exception rationale, approving reviewer, limits, affected records, and follow-up. |
| Supersession or rejection | Replaced/rejected record, reason, replacement if known, prohibited future use, and affected consumers. |

## Relationship map

| Source object | Relationship | Target object | Rule |
| --- | --- | --- | --- |
| SourceReference | supports | GroundedClaim | Every claim must cite at least one source reference. |
| SourceReference | bounds | ApprovedExtract | Extracts preserve original source posture and limitations. |
| ApprovedExtract | supports | GroundedClaim | Extract scope limits claim applicability. |
| GroundedClaim | composes | KnowledgeAsset | Asset confidence and readiness cannot exceed material claim limits without reviewer rationale. |
| KnowledgeAsset | grounds | PersonaTemplate | Template may use only approved or approved-with-limits assets within role scope. |
| PersonaTemplate | instantiates | PersonaInstance | Instance uses one approved template version. |
| KnowledgeAsset and PersonaTemplate | package | GroundingContext | Context supplies bounded assets and role behavior to a task or workflow. |
| LearningSignal | proposes | PromotionRequest | Learning remains operational-only until promotion is approved. |
| PromotionRequest | results in | ReviewDecision | Reusable behavior changes require decision outcome and rationale. |
| ReviewDecision | changes | Any governed object | Decision must name affected records and effective state. |
| GovernancePolicy | constrains | Any governed object | Policy can block, caveat, require review, or require escalation. |
| AuditRecord | records | Any material transition | Audit trail preserves state, rationale, evidence, and downstream impact. |

## Cross-object transition guardrails

1. **Candidate material cannot become reusable directly**: Candidate sources,
   claims, learnings, extracts, assets, or persona changes must pass through
   proposal and review states before approval.
2. **Operational-only evidence requires promotion**: Runtime, task, handoff, log,
   raw, research, or future-source evidence can create learning signals and
   promotion requests, but it cannot directly approve assets or persona behavior.
3. **Approval is scoped**: Approval always applies to stated claims,
   applicability, limitations, confidence, freshness, and downstream consumers;
   it does not approve unrelated source material.
4. **Approved-with-limits requires visible caveats**: Consumers must preserve the
   caveats or the item is not ready for consumption.
5. **Supersession preserves history**: Superseded records remain traceable and
   must not be deleted from the product audit trail by contract.
6. **Rejected records remain prohibited**: Rejected material may be referenced as
   risk or limitation context but cannot ground future behavior unless a later
   review decision supersedes the rejection.
7. **Blocked records require owner and follow-up**: Blocked state must identify
   what decision or evidence is missing and who owns resolution.
8. **Governance blockers outrank readiness**: Any applicable governance policy
   with unresolved block prevents consumption readiness even if evidence fields
   are otherwise present.

## Validation and readiness gates

| Gate | Applies to | Ready condition | Blocks readiness when |
| --- | --- | --- | --- |
| Identifier gate | All records | Required logical IDs and related record IDs are present. | Record cannot be traced, versioned, reviewed, or audited. |
| Source posture gate | Sources, extracts, claims, assets, contexts | Each material source is approved, approved extract, operational-only, seed, or future candidate. | Operational, seed, raw/research, or future evidence is treated as approved. |
| Provenance gate | Claims, extracts, assets, personas, contexts | Source references, evidence class, confidence, freshness, owner, applicability, and limitations are attached. | Claims cannot be traced or caveats are dropped. |
| Evidence gate | Claims, assets, persona guidance | Claims distinguish source-backed, inferred, assumed, and open. | Assumptions or open questions become committed behavior. |
| Confidence gate | Claims, assets, templates, contexts | High/medium claims are used within scope; low/blocked claims are caveats, proposals, or blockers. | Low or blocked confidence grounds committed behavior. |
| Freshness gate | Sources, claims, assets, contexts | Current/recent freshness is present, or stale-risk/unknown has owner review. | Stale, unknown, or superseded evidence drives reusable behavior without review. |
| Applicability gate | Assets, templates, contexts, instances | Intended workflow, domain, persona, and decision use is within approved scope. | Asset or persona is used outside its approved scope. |
| Persona behavior gate | Persona templates and instances | Behavior-affecting guidance has approved evidence, reviewer rationale, version, limits, and escalation rules. | Template behavior changes without attribution or review. |
| Promotion gate | Extracts, assets, learnings, persona changes | Promotion target, owner, reviewer, outcome, and limits are recorded. | Runtime, raw, research, SME, or future findings bypass promotion. |
| Governance gate | All governed records | Applicable policies are satisfied or not-applicable with rationale. | Policy requires review, escalation, exception, or blocker resolution. |
| Audit gate | All material transitions | Audit record captures actor role, prior/new state, rationale, evidence, affected records, and follow-up. | Material transition cannot be reconstructed. |
| Future-scope gate | All contracts and records | Open implementation topics remain open decisions or blockers. | Contract chooses storage, retrieval, embedding, connector, provider, tenancy, deployment, runtime, UI, or compliance implementation. |

## Governance rules

1. Source approval, extract approval, knowledge asset promotion, SME validation,
   persona behavior changes, consumption readiness exceptions, and learning
   promotion require human or SME review appropriate to the affected scope.
2. Lack of accountable owner or reviewer blocks approval.
3. Low-confidence, blocked, assumed, open, stale-risk, unknown, conflicting, or
   prohibited material must be surfaced as caveat, blocker, validation need,
   open question, or escalation trigger before consumption.
4. Persona templates and instances must preserve the stricter rule when template,
   grounding context, knowledge asset, or governance policy disagree.
5. Approved source or extract status does not imply approval for every workflow,
   persona, domain, or downstream decision; applicability must be explicit.
6. Governance policies may define review requirements, readiness blockers,
   caveat requirements, and escalation paths, but this document does not define
   technical enforcement mechanisms.
7. Source material in raw or research areas remains read-only seed evidence and
   must not be edited or directly promoted without reviewed extract or canonical
   product artifact promotion.
8. Future external or SME/domain source use remains blocked until ownership,
   authority, provenance, freshness, governance posture, and promotion rules are
   accepted at the product-contract level.

## Audit expectations

Synapse should be able to answer these product questions from contract records
and audit history:

- Which sources and approved extracts support this claim, asset, persona
  behavior, grounding context, or promotion?
- Who owns the record and who reviewed the material decision?
- What state was the record in before and after a material transition?
- What evidence was reviewed, what rationale was recorded, and what limitations
  were accepted?
- Which workflows, personas, standards, validators, backlog gates, or grounding
  contexts were affected?
- Which caveats, confidence limits, freshness limits, open questions, or
  governance blockers were preserved?
- What follow-up owner or decision is required before blocked, deferred, stale,
  unknown, low-confidence, assumed, or open material can be reused?

## Open implementation decisions

These decisions remain explicitly outside this product-logical contract. They
must be resolved by later accepted product, architecture, governance, or domain
decisions before implementation commits to them.

| ID | Open decision | Current contract handling |
| --- | --- | --- |
| MVP2-KPC-OQ-001 | What concrete storage, indexing, search, retrieval, embedding, or prompt-context mechanism should implement these contracts? | Future/open; contracts define logical records, relationships, and gates only. |
| MVP2-KPC-OQ-002 | Which connectors, crawlers, sync jobs, external systems, customer corpora, or legacy sources should be supported first? | Future/open; external sources remain future candidates until governed. |
| MVP2-KPC-OQ-003 | What provider, runtime, deployment, scaling, or operational architecture should execute persona and grounding consumption? | Future/open; contracts define product readiness and consumption boundaries only. |
| MVP2-KPC-OQ-004 | What tenancy, access-control, sensitive-data, privacy, retention, deletion, compliance, and audit implementation policies apply? | Future/open governance blockers; this document defines audit expectations but not implementation controls. |
| MVP2-KPC-OQ-005 | What user-facing surface should expose registries, review queues, grounding contexts, persona templates, and audit history? | Future/open; contracts remain independent of UI choices. |
| MVP2-KPC-OQ-006 | Who are the named accountable owners and reviewers for first source families, knowledge assets, persona templates, freshness review, and learning promotion? | Use role-based owners and reviewers until named people or teams are accepted. |
| MVP2-KPC-OQ-007 | What concrete freshness cadence, expiration threshold, or review SLA applies by source class, domain, or asset type? | Use freshness labels and owner review expectations only. |
| MVP2-KPC-OQ-008 | Which persona composition, inheritance, or packaging format should represent templates and instances? | Future/open; this contract defines required product semantics and relationships only. |
| MVP2-KPC-OQ-009 | Which provenance fields should become machine-readable for future validators or event contracts? | Future/open; required logical fields are defined here without schema or event implementation. |
| MVP2-KPC-OQ-010 | Which learning promotion targets should be enabled first in the MVP2 product experience? | Future/open; all target types are defined as logical possibilities with review requirements. |

