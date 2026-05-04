# Synapse Product MVP2: Knowledge Workflow

- **Status**: product-owner draft
- **MVP**: MVP2
- **Companion capability spec**: `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md`
- **Last updated**: 2026-05-03
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

## Workflow premise

MVP2 gives Synapse a governed workflow for turning source material, SME input,
and completed-run learning into reusable knowledge and persona behavior. The
workflow makes approval, provenance, confidence, freshness, applicability, and
limitations visible before an AI coworker can rely on an asset or template.

The workflow is product-facing. It describes what Synapse users review, decide,
and consume. It does not expose repository-only source-grounding documents,
orchestration configuration, runtime memos, task cards, or Cursor-specific
mechanics as the customer product.

## Source intake workflow summary

| Stage | User intent | Synapse support | Primary output |
| --- | --- | --- | --- |
| 1. Intake candidate | Bring a source, SME note, workflow learning, or approved extract candidate into review. | Captures source type, owner, proposed use, status, and known limitations. | Source candidate. |
| 2. Classify posture | Decide whether the input is approved, operational, seed, SME, future candidate, or already superseded. | Prompts for source posture, evidence class, confidence, freshness, applicability, and owner. | Classified review item. |
| 3. Review source or extract | Decide whether the candidate can ground future Synapse work. | Presents evidence, proposed claims, provenance, confidence/freshness, limitations, and decision options. | Source approval decision or approved extract. |
| 4. Create knowledge asset | Package approved claims into a reusable product object. | Records claims, owners, reviewers, provenance, applicability, consumption limits, and promotion state. | Governed knowledge asset. |
| 5. Update SME/persona template | Decide whether approved knowledge changes role behavior. | Shows affected persona guidance, evidence rules, confidence/freshness impact, escalation behavior, and version change. | Persona template or change record. |
| 6. Attach grounding context | Supply approved assets and persona guidance to a workflow run or AI coworker. | Builds bounded context with allowed sources, prohibited sources, caveats, evidence expectations, and escalation triggers. | Grounding context for workflow consumption. |
| 7. Capture learning signals | Identify lessons from runs, reviews, blockers, revisions, or handoff feedback. | Creates learning items with evidence, recurrence/impact, target type, owner, and promotion state. | Learning queue. |
| 8. Promote or reject learning | Decide whether learning should change reusable assets or become a backlog item. | Routes learning to knowledge, persona, workflow, validator, standard, or backlog review. | Promotion decision and updated asset/backlog target. |

## Workflow actors

| Actor | Workflow responsibility |
| --- | --- |
| Knowledge owner | Owns source family or asset accuracy, scope, freshness, and limitations. |
| SME / domain reviewer | Validates expert guidance and applicability before it becomes reusable. |
| Persona/template owner | Maintains role behavior and approves persona-impacting changes with reviewer support. |
| Human operator | Selects approved knowledge and persona templates for a workflow run and sees caveats before dispatch. |
| Product/governance reviewer | Confirms product fit, risk posture, review sufficiency, and promotion decisions. |
| AI coworker | Consumes only approved or explicitly allowed context under a persona template and escalates when guardrails are not met. |

## Stage details

### 1. Intake candidate

**User goal**: Introduce potential knowledge without treating it as durable truth.

**User sees**

- Candidate title, source type, source owner if known, proposed use, and target
  workflow/persona/domain.
- Whether the candidate came from an approved source, SME input, completed
  workflow output, reviewer decision, operational evidence, seed material, or
  future external source.
- Warning when the source cannot directly ground future work without review.

**Human decisions**

- Is the candidate in scope for Synapse MVP2 review?
- Who owns the candidate and who should review it?
- Should the candidate proceed to classification, be returned for clarification,
  or be rejected as out of scope?

**Outputs**

- Source candidate.
- Initial owner/reviewer assignment.
- Proposed promotion target if known.

### 2. Classify posture

**User goal**: Make source authority and uncertainty explicit before review.

**User sees**

- Source posture options: approved source, approved extract, operational source,
  seed source, future candidate source, SME review evidence, superseded, or
  rejected.
- Evidence class: source-backed, inferred, assumed, or open.
- Confidence: high, medium, low, or blocked.
- Freshness: current, recent, stale-risk, superseded, or unknown.
- Applicability and known limitations.

**Human decisions**

- What authority does this source have today?
- What claims, if any, are source-backed versus inferred, assumed, or open?
- Does freshness or confidence require owner review before reuse?
- Does any open decision block approval?

**Outputs**

- Classified review item.
- Confidence/freshness/provenance record.
- Review blockers or open questions.

### 3. Review source or extract

**User goal**: Decide what can safely ground future Synapse work.

**User sees**

- Proposed claim or approved extract summary.
- Original source references or source IDs.
- Owner, reviewer, applicability, limitations, evidence class, confidence, and
  freshness.
- Downstream impact on knowledge assets, persona templates, workflow templates,
  validators, standards, or backlog gates.

**Human decisions**

- Approve the source or extract within a stated scope.
- Approve with limits or lower confidence.
- Request changes, defer, reject, supersede, or escalate.
- Assign follow-up for missing owner, stale source, conflict, or governance
  blocker.

**Outputs**

- Source approval decision.
- Approved extract when promotion is accepted.
- Review-needed, rejected, deferred, superseded, or blocked state when not
  accepted.

### 4. Create knowledge asset

**User goal**: Package approved knowledge so future workflows and personas can
reuse it safely.

**User sees**

- Knowledge asset kind, owner, reviewer, claims, provenance, applicability,
  limitations, confidence, freshness, review status, and promotion state.
- Where the asset may be used: workflow, domain, persona, decision area, backlog
  gate, or handoff context.
- Consumption constraints and escalation triggers.

**Human decisions**

- Should the approved claim become a reusable knowledge asset?
- Which workflows, personas, domains, or decisions may consume it?
- What limitations must remain visible?
- When is owner review required before future use?

**Outputs**

- Governed knowledge asset.
- Asset consumption limits.
- Owner and review state.

### 5. Update SME/persona template

**User goal**: Convert approved knowledge or SME guidance into reusable role
behavior only when review supports it.

**User sees**

- Persona role purpose, responsibilities, allowed knowledge, prohibited behavior,
  evidence expectations, confidence/freshness thresholds, output standards, and
  escalation behavior.
- Proposed persona change with source references, reviewer rationale, affected
  workflows, and version impact.
- Any low-confidence, stale, assumed, or open claims that must remain caveats or
  escalation instructions.

**Human decisions**

- Should the persona template change at all?
- Is the knowledge source applicable to this role and workflow?
- Does the change require SME, standards, product, or governance review?
- Should the change be approved, limited, deferred, rejected, or escalated?

**Outputs**

- Persona template.
- Persona version/change record.
- Role-specific consumption and escalation rules.

### 6. Attach grounding context to workflow consumption

**User goal**: Give a workflow run or AI coworker a bounded, reviewable context
package.

**User sees**

- Required approved knowledge assets.
- Persona template and role behavior.
- Allowed operational references, if any, marked as operational-only.
- Prohibited source classes and excluded material.
- Evidence expectations, confidence threshold, freshness expectations, and
  handoff requirements.
- Warnings for stale-risk, unknown, low-confidence, blocked, assumed, or open
  material.

**Human decisions**

- Is the selected knowledge/persona context ready for this workflow run?
- Are caveats acceptable for draft work, or must the run block pending review?
- Which low-confidence or stale items require escalation before dispatch?
- What must the AI coworker report back in its handoff?

**Outputs**

- Grounding context.
- Consumption readiness decision.
- Escalation and caveat instructions for the AI coworker.

### 7. Capture learning signals

**User goal**: Turn workflow experience into improvement candidates without
silently changing reusable behavior.

**User sees**

- Suggested learning from completed workflow outputs, review decisions, repeated
  revisions, blockers, handoff feedback, stale-source issues, persona ambiguity,
  or validation gaps.
- Evidence, recurrence or impact, proposed target, owner, and review need.
- Difference between one-time observation and reusable improvement candidate.

**Human decisions**

- Is this a real learning signal or a one-off note?
- What target should it affect: knowledge asset, persona template, workflow
  template, validator, standard, backlog gate, or product decision?
- Who owns review and promotion?

**Outputs**

- Learning item.
- Promotion request candidate.
- Improvement backlog entry when promotion is not immediate.

### 8. Promote or reject learning

**User goal**: Decide which learning changes future Synapse behavior.

**User sees**

- Learning item, source evidence, recurrence/impact, target asset, affected
  workflows/personas, confidence/freshness impact, and proposed change.
- Review options and downstream consequences.

**Human decisions**

- Promote the learning into a reusable target.
- Request changes or additional SME/source review.
- Defer pending product, architecture, governance, source-owner, or freshness
  decision.
- Reject with rationale.

**Outputs**

- Promotion decision.
- Updated knowledge asset, persona template, workflow template, validator,
  standard, or backlog gate when approved.
- Deferred/rejected record with rationale and limitations.

## Review gate map

| Gate | Moment | Human decision | Required record |
| --- | --- | --- | --- |
| G0: Intake classification | Before review work proceeds | Is the candidate in scope, and who owns it? | Candidate state, owner, reviewer, proposed target. |
| G1: Source approval | Before source or extract can ground future work | Is this source/extract approved within a stated scope? | Decision, reviewer, evidence reviewed, rationale, limitations. |
| G2: Knowledge asset promotion | Before approved claim becomes reusable asset | Should this claim become reusable product knowledge? | Asset, claims, provenance, confidence, freshness, applicability, owner. |
| G3: SME validation | Before SME guidance becomes reusable | Is the SME claim accurate, applicable, and bounded? | SME/reviewer role, evidence reviewed, confidence, limitations. |
| G4: Persona behavior change | Before role behavior changes | Should this knowledge alter a persona template? | Version/change record, reviewer rationale, affected workflows. |
| G5: Consumption readiness | Before workflow or AI coworker dispatch | Is selected knowledge/persona context ready or caveated? | Grounding context, caveats, blockers, escalation instructions. |
| G6: Learning promotion | After workflow output or review creates learning | Should the learning update reusable behavior or backlog gates? | Promotion decision, target, owner, rationale, follow-up. |

## Consumption rules for AI coworkers

AI coworkers consuming MVP2 knowledge and persona templates must:

1. Use approved knowledge assets and approved extracts within stated
   applicability and limitations.
2. Treat operational, seed, raw, research, and future candidate sources as
   non-durable unless the task explicitly allows them for review or promotion
   proposal.
3. Preserve evidence class, confidence, freshness, provenance, assumptions,
   open questions, and limitations in outputs and handoffs.
4. Escalate rather than rely on low-confidence, blocked, stale-risk, unknown,
   conflicting, or prohibited material.
5. Follow persona template boundaries, allowed knowledge, prohibited behavior,
   quality gates, output expectations, and escalation instructions.
6. Propose learning or promotion requests when repeated gaps, ambiguity, source
   drift, validation failures, or useful recovery patterns appear.

## Learning promotion targets

| Target | Promote when | Required reviewer expectation |
| --- | --- | --- |
| Knowledge asset | Learning changes a reusable claim, applicability note, limitation, or approved extract. | Knowledge owner confirms provenance, confidence, freshness, and scope. |
| Persona template | Learning changes role responsibility, evidence rule, prohibited action, output standard, or escalation behavior. | Persona/template owner and relevant reviewer accept behavior impact. |
| Workflow template | Learning changes a repeatable workflow step, dependency, gate, input, output, or handoff expectation. | Workflow owner confirms product fit and downstream impact. |
| Validator or quality gate | Learning reveals a repeatable objective check or review-only readiness criterion. | QA/reviewer role confirms what can be checked automatically versus reviewed. |
| Standard | Learning changes evidence, provenance, confidence, freshness, review, or promotion expectations across roles. | Standards owner and affected owner accept reusable rule. |
| Backlog gate or work item | Learning creates implementation dependency, spike, blocker, risk, or future product decision. | Backlog owner records priority, owner, and blocking impact. |

## Status model

MVP2 knowledge workflow states should remain product-level and implementation
neutral:

| State | Meaning | Allowed downstream use |
| --- | --- | --- |
| Candidate | Item is identified but not classified or reviewed. | Discovery only. |
| Proposed | Claim, source, target, and owner are recorded for review. | Review input only. |
| Review-needed | Human, SME, product, standards, or governance decision is required. | Blocks reusable behavior changes. |
| Approved | Reviewer accepted scope, evidence, confidence, freshness, and limits. | May ground future work within stated limits. |
| Approved with limits | Reviewer accepted restricted use or required caveats. | May be consumed only with visible caveats and scope limits. |
| Operational-only | Useful for traceability or recovery but not durable truth. | May not ground reusable behavior. |
| Deferred | Decision postponed pending source, SME, product, governance, or owner input. | Blocks reliance until resolved. |
| Superseded | Replaced by newer approved source or decision. | Historical reference only. |
| Rejected | Reviewer rejected source, claim, or promotion. | Do not consume except as limitation or risk context. |
| Blocked | Missing owner, unresolved decision, governance issue, or insufficient evidence prevents progress. | Escalate or create follow-up; no committed reuse. |

## End-to-end outputs

At the end of a successful MVP2 knowledge workflow, Synapse should provide:

1. Classified source candidates and source approval decisions.
2. Approved extracts with reviewer rationale and limitations.
3. Governed knowledge assets ready for approved workflow/persona consumption.
4. SME guidance records and validation decisions.
5. Persona templates and persona change records with grounded behavior.
6. Grounding contexts attached to workflow runs or AI coworker work packets.
7. Learning items, promotion requests, and promotion decisions.
8. Backlog gates or open product decisions where reusable behavior remains
   blocked.

## Non-goals for the workflow

- The workflow does not choose a storage, retrieval, embedding, search, indexing,
  connector, crawler, synchronization, prompt-management, provider, runtime,
  tenancy, access-control, retention, deletion, privacy, compliance, billing, or
  deployment implementation.
- The workflow does not make raw, research, runtime, or ungoverned external
  material directly reusable without review.
- The workflow does not automatically approve sources, SME guidance, persona
  changes, or learning promotions.
- The workflow does not require users to understand repository-only source
  grounding docs, orchestration memos, task cards, workflow YAML, or Cursor rules
  as product concepts.
- The workflow does not productize every possible source system, domain pack,
  persona pack, or expert workflow in MVP2.

## Acceptance criteria

| ID | Criterion |
| --- | --- |
| MVP2-KWF-AC-001 | A source, SME input, or learning candidate can be classified before it is allowed to ground future work. |
| MVP2-KWF-AC-002 | A reviewer can approve, approve with limits, request changes, defer, reject, supersede, or block a source or extract with rationale. |
| MVP2-KWF-AC-003 | Approved knowledge assets preserve source references, evidence class, confidence, freshness, applicability, limitations, owner, reviewer, and promotion state. |
| MVP2-KWF-AC-004 | Persona template changes require approved knowledge or SME guidance, reviewer rationale, affected workflow scope, and version/change record. |
| MVP2-KWF-AC-005 | Grounding context for an AI coworker includes required approved assets, allowed operational references, prohibited sources, evidence expectations, confidence/freshness requirements, and escalation instructions. |
| MVP2-KWF-AC-006 | Low-confidence, blocked, stale-risk, unknown, assumed, open, conflicting, or prohibited material is surfaced as caveat, blocker, or escalation need before consumption. |
| MVP2-KWF-AC-007 | Workflow learnings enter a promotion path with target type, owner, evidence, review state, and decision outcome. |
| MVP2-KWF-AC-008 | The workflow remains product-facing and does not describe repository-only source-grounding docs as the product experience. |
| MVP2-KWF-AC-009 | The workflow preserves implementation choices for storage, retrieval, embeddings, connectors, providers, tenancy, compliance, access, retention, and runtime as open/future decisions. |

## Open product decisions

| ID | Decision | Impact |
| --- | --- | --- |
| MVP2-KWF-OQ-001 | Which user-facing product surface should host the knowledge workflow first: registry, review queue, workspace side panel, or guided setup flow? | Determines interaction design and MVP1 handoff. |
| MVP2-KWF-OQ-002 | Which source families and SME/persona templates should be onboarded first for an external or internal user? | Determines initial review workload and asset catalog. |
| MVP2-KWF-OQ-003 | Who are the named reviewers for source approval, SME validation, persona behavior changes, freshness review, and learning promotion? | Determines approval routing and accountability. |
| MVP2-KWF-OQ-004 | What confidence thresholds should block dispatch, require caveat, or allow draft-only work? | Determines workflow friction and trust posture. |
| MVP2-KWF-OQ-005 | What freshness cadence or review SLA should apply by source or asset type? | Determines owner workload and stale-source escalation. |
| MVP2-KWF-OQ-006 | Which learning promotion targets should be enabled first in the product experience? | Determines how quickly the self-augmenting loop becomes reusable. |
| MVP2-KWF-OQ-007 | What future governance constraints apply before external source systems or customer/domain corpora can enter the workflow? | Blocks ingestion, connector, access, retention, and compliance implementation decisions. |
