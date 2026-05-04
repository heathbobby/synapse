# Synapse Product MVP2: Persona Template System

- **Status**: standards-curator draft
- **MVP**: MVP2
- **Last updated**: 2026-05-04
- **Companion capability spec**: `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md`
- **Companion workflow spec**: `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md`
- **Companion contract spec**: `docs/product/MVP2/KNOWLEDGE_PERSONA_CONTRACTS.md`
- **Primary sources**:
  - `docs/refinement/iteration-inputs/product-mvp2-knowledge-persona-layer.md`
  - `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md`
  - `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md`
  - `docs/product/MVP2/KNOWLEDGE_PERSONA_CONTRACTS.md`
  - `docs/MVP2/Knowledge/GroundingModel.md`
  - `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`
  - `docs/standards/AI_AGENT_STANDARDS.md`

## Purpose

This document defines the Synapse MVP2 product-facing SME/persona template
system. The system turns approved knowledge, SME guidance, review expectations,
and workflow learning into reusable AI coworker role behavior that can be safely
instantiated for bounded work.

Persona templates are governed product assets, not prompt-only tooling. Synapse
must make role purpose, expertise boundaries, allowed knowledge, evidence rules,
confidence and freshness expectations, escalation behavior, review status,
version history, and learning promotion visible before reusable persona behavior
is consumed.

This system is implementation-neutral. It does not choose a storage mechanism,
retrieval approach, embedding model, prompt-management service, provider runtime,
connector, tenancy model, compliance control, access-control mechanism, UI, or
deployment architecture.

## Product principles

1. **Personas are reusable governed assets**: A persona template packages role
   behavior, approved knowledge scope, evidence discipline, output obligations,
   and escalation rules for future AI coworker use.
2. **Role behavior must be source-backed or reviewed**: Behavior-affecting
   instructions require approved knowledge, approved extracts, SME validation,
   or review decisions with preserved provenance.
3. **Instances are bounded by context**: A persona instance may use only the
   approved template version and grounding context supplied for its workflow,
   task, run, review, or handoff.
4. **Uncertainty remains visible**: Low-confidence, blocked, stale-risk,
   unknown, assumed, open, conflicting, or prohibited material may become a
   caveat, validation need, blocker, or escalation trigger, but not committed
   reusable behavior.
5. **Human review governs promotion**: Source approval, SME validation, persona
   behavior changes, consumption readiness exceptions, and learning promotion
   require accountable review.
6. **Learning is explicit**: Completed-run learnings may propose changes to
   persona templates, knowledge assets, standards, validators, workflow
   templates, or backlog gates, but must not silently alter future behavior.

## Persona system objects

| Object | Product meaning | Required product-visible properties |
| --- | --- | --- |
| Base persona | Shared baseline behavior that applies to all Synapse AI coworkers. | Evidence discipline, role-boundary rule, safe action classes, prohibited actions, output obligations, escalation defaults, learning-signal expectations. |
| Extended persona template | Reusable governed role specialization for an SME/domain/coworker role. | Role purpose, expertise boundary, responsibilities, allowed knowledge, prohibited behavior, evidence rules, confidence/freshness rules, outputs, escalation behavior, owner, reviewer, version, lifecycle state. |
| Persona instance | Bounded use of one approved template version for a specific workflow/task/run/review. | Instantiation purpose, template version, grounding context, active caveats, escalation triggers, output obligations, readiness state, completion or handoff state. |
| Persona change record | Product history record for behavior-affecting template changes. | Changed guidance, sources, evidence class, confidence/freshness impact, reviewer rationale, affected workflows, version impact, follow-up owner. |
| Persona learning signal | Candidate reusable improvement discovered during workflow execution or review. | Signal summary, evidence, recurrence/impact, proposed target, owner, confidence, review need, promotion state. |

## Base persona

The base persona is the minimum product behavior contract for every Synapse AI
coworker before any role specialization is applied.

### Baseline responsibilities

Every Synapse AI coworker must:

1. Operate within the assigned role, objective, deliverables, sources, and
   completion criteria.
2. Consume only approved knowledge assets, approved extracts, allowed operational
   references, and grounding context explicitly supplied for the task.
3. Preserve source references, evidence class, confidence, freshness,
   applicability, assumptions, open questions, limitations, and review status in
   material outputs and handoffs.
4. Distinguish source-backed claims from inferred, assumed, and open claims.
5. Treat raw, research, operational-only, seed, rejected, superseded, and future
   candidate material as non-durable unless the assigned task explicitly scopes a
   review or promotion proposal.
6. Escalate when role scope, source authority, confidence, freshness,
   provenance, governance posture, or required review is insufficient.
7. Produce learning signals when repeated ambiguity, source drift, validation
   gaps, role-boundary issues, or useful recovery patterns appear.

### Baseline prohibited behavior

Every Synapse AI coworker must not:

- silently expand role scope, source authority, deliverables, or approval rights;
- convert assumptions, open questions, or low-confidence material into committed
  product, persona, architecture, governance, compliance, runtime, or
  implementation decisions;
- embed raw, research, operational-only, or future external claims directly into
  reusable persona behavior without approved promotion;
- override the grounding context, prohibited sources, prohibited edits, quality
  gates, or completion criteria for the assigned work;
- approve its own source promotion, SME validation, governance exception,
  persona behavior change, or learning promotion unless a human review decision
  grants that authority;
- imply a knowledge store, retrieval mechanism, embedding model, connector,
  provider, tenancy, retention, deletion, access-control, compliance, UI, or
  deployment implementation that has not been accepted by canonical product,
  architecture, or governance decision.

## Extended persona template

An extended persona template specializes the base persona for a recurring SME,
domain reviewer, specialist, integrator, operator-support, or governance role.
The template defines what the AI coworker is allowed to know, do, produce, and
escalate when instantiated.

### Required template fields

| Field | Product requirement |
| --- | --- |
| `persona_template_id` | Stable logical identifier for review, audit, and relationship mapping. |
| `version_id` | Approved version of the template behavior. |
| `role_name` | Human-readable role name. |
| `role_purpose` | What the AI coworker is meant to accomplish. |
| `expertise_boundary` | Domain, workflow, decision, and authority limits. |
| `responsibilities` | Duties, expected work products, handoffs, and completion signals. |
| `allowed_knowledge` | Approved knowledge assets, approved extracts, source classes, or grounding contexts the role may consume. |
| `prohibited_behavior` | Actions, claims, sources, decisions, or outputs the role must not perform or assert. |
| `allowed_action_classes` | Product-level actions the role may perform when authorized by its task and grounding context. |
| `evidence_rules` | Required treatment of source-backed, inferred, assumed, and open claims. |
| `confidence_rules` | High, medium, low, and blocked confidence handling for committed output, caveats, draft-only work, and escalation. |
| `freshness_rules` | Current, recent, stale-risk, superseded, and unknown freshness handling. |
| `grounding_requirements` | Required approved assets, prohibited sources, caveats, review status, and handoff preservation rules. |
| `output_standards` | Required output shape, citations, assumptions, open questions, validation status, limitations, and handoff notes. |
| `escalation_behavior` | Conditions that require human, SME, product, standards, owner, governance, or reviewer escalation. |
| `owner_role_id` | Role accountable for correctness, applicability, freshness, and template maintenance. |
| `reviewer_role_id` | Role that approved the current version or latest behavior-affecting change. |
| `lifecycle_state` | Candidate, proposed, review-needed, approved, approved-with-limits, deferred, superseded, rejected, or blocked. |
| `audit_record_ids` | Product history for material review, versioning, promotion, and supersession events. |

### Template readiness

An extended persona template is instantiation-ready only when:

- the current version is `approved` or `approved-with-limits`;
- role purpose, expertise boundary, responsibilities, allowed knowledge,
  prohibited behavior, evidence rules, confidence/freshness rules, output
  standards, and escalation behavior are complete;
- behavior-affecting guidance references approved or approved-with-limits
  knowledge, approved extracts, SME guidance records, or review decisions;
- low-confidence, blocked, stale-risk, unknown, assumed, open, or conflicting
  material is preserved as caveat, blocker, validation need, prohibition, or
  escalation trigger;
- owner, reviewer, version, state, rationale, and affected workflows are visible;
- applicable governance policies are satisfied or marked not applicable with
  rationale.

## Persona instance

A persona instance is the bounded product use of one approved persona template
version for one workflow, task, run, review, or operator-assigned role context.
It is not a new reusable template unless promoted through review.

### Required instance fields

| Field | Product requirement |
| --- | --- |
| `persona_instance_id` | Stable logical identifier for the bounded assignment. |
| `persona_template_id` and `version_id` | The approved or approved-with-limits template version being instantiated. |
| `instantiation_purpose` | Workflow, task, review, handoff, or role assignment being served. |
| `grounding_context_id` | Bounded context package supplied to the instance. |
| `active_caveats` | Approved-with-limits terms, stale-risk items, assumptions, open questions, and limitations that must be preserved. |
| `escalation_triggers` | Template-level and context-specific conditions requiring review or pause. |
| `output_obligations` | Required citations, evidence labels, validation notes, handoff details, and learning proposals. |
| `readiness_state` | Ready, ready-with-caveats, review-needed, deferred, blocked, completed, or cancelled. |
| `owner_role_id` | Accountable role or operator-assigned owner for follow-up. |

### Instance rules

- An instance must reference exactly one approved or approved-with-limits template
  version.
- An instance must not expand allowed knowledge beyond the grounding context,
  template, governance policy, or asset applicability boundaries.
- A ready-with-caveats instance must preserve every caveat in outputs and
  handoffs.
- A blocked instance must identify the blocker, owner, required decision, and
  follow-up path.
- An instance may create learning signals, but those signals remain
  operational-only until reviewed and promoted.

## Role boundaries

Persona templates must describe role authority separately from role expertise.
Expertise means the role can reason within a bounded domain; authority means the
role may make, recommend, approve, or escalate a decision.

| Boundary | Product rule |
| --- | --- |
| Scope boundary | The persona may work only on assigned workflows, domains, decisions, and deliverables. |
| Knowledge boundary | The persona may consume only approved or explicitly allowed knowledge within applicability limits. |
| Decision boundary | The persona may recommend or draft within scope, but cannot approve source promotion, SME validation, governance exceptions, or reusable behavior changes without the required reviewer decision. |
| Tool/action boundary | The persona may perform only allowed product action classes authorized by the template and grounding context. |
| Governance boundary | Sensitive, compliance, access, retention, tenancy, provider, deployment, or external-source questions remain open, blocked, or escalated unless approved elsewhere. |
| Learning boundary | Runtime observations may create learning signals or promotion requests but do not change reusable behavior automatically. |

## Allowed tool and action classes

Synapse templates should describe allowed actions as product-level classes. They
must not require a particular tool adapter, model provider, prompt format, or
runtime implementation.

| Action class | Allowed use | Required guardrails |
| --- | --- | --- |
| Read approved knowledge | Inspect approved knowledge assets, approved extracts, standards, contracts, and grounding context supplied for the work. | Preserve source references, confidence, freshness, applicability, and limitations. |
| Read allowed operational references | Inspect operational-only evidence for traceability, recovery, or promotion proposal. | Mark operational-only; do not treat as durable truth. |
| Draft or update assigned deliverables | Produce the exact artifacts or outputs assigned to the persona instance. | Stay within scope, cite grounding, preserve caveats, and avoid prohibited edits. |
| Classify claims | Label claims as source-backed, inferred, assumed, or open with confidence and freshness. | Do not upgrade evidence class or confidence without reviewer rationale. |
| Propose promotion | Create candidate promotion requests for sources, SME guidance, learnings, standards, validators, workflow templates, backlog gates, or persona changes. | Include source posture, target, owner, reviewer need, limitations, and downstream impact. |
| Validate readiness | Check required fields, prohibited sources, caveats, completion criteria, or review gates where the task allows. | Separate deterministic checks from review-only sufficiency judgments. |
| Handoff and escalate | Report outputs, blockers, caveats, validation status, open questions, and follow-up owners. | Use the strictest applicable template, grounding-context, asset, and governance rule. |
| Capture learning | Record repeated gaps, source drift, persona ambiguity, validation failures, or recovery patterns. | Keep as learning signal until reviewed for promotion. |

### Prohibited action classes

Unless separately authorized by a reviewed product decision, persona templates
must prohibit:

- direct approval of sources, approved extracts, SME validation, persona
  behavior changes, governance exceptions, or learning promotion;
- direct use of raw, research, seed, operational-only, rejected, superseded, or
  future candidate material as durable grounding;
- expansion of source scope, role authority, allowed knowledge, or affected
  workflows without review;
- implementation commitments about storage, retrieval, embeddings, connectors,
  providers, tenancy, compliance, retention, deletion, access-control, UI, or
  deployment;
- external side effects, customer-facing commitments, or administrative changes
  outside the assigned and governed workflow.

## Evidence rules

Persona behavior and outputs must use the shared MVP2 evidence classes.

| Evidence class | Persona use | Required handling |
| --- | --- | --- |
| Source-backed | Directly supported by approved source or approved extract. | May support reusable role behavior within scope; cite source path/ID or approved reference. |
| Inferred | Reasonably derived from approved sources but not directly stated. | May guide draft or caveated work; behavior-affecting reuse requires review. |
| Assumed | Needed to proceed but not validated. | Record assumption, validation need, owner, and risk; do not convert to instruction except as caveat or escalation. |
| Open | Unknown or awaiting product, SME, governance, architecture, owner, or stakeholder decision. | Do not ground committed behavior; route to decision, reviewer, spike, or blocker. |

Material persona claims must preserve:

- source path or source/reference ID;
- source posture;
- evidence class;
- confidence and rationale;
- freshness;
- owner and reviewer where applicable;
- applicability;
- limitations, assumptions, open questions, and prohibited uses;
- promotion or lifecycle state.

## Grounding requirements

Persona templates and instances must rely on grounding context rather than
unbounded context assembly.

### Template grounding

Template guidance may include knowledge only when:

1. the claim comes from an approved source, approved extract, SME guidance record,
   or review decision;
2. the claim is applicable to the role and affected workflows;
3. confidence is high or medium, or lower confidence is preserved only as caveat,
   validation need, or escalation trigger;
4. freshness is current, recent, or reviewer-confirmed for stale-risk use;
5. behavior impact, reviewer rationale, and version effect are recorded;
6. open decisions remain explicit prohibitions, blockers, or questions.

### Instance grounding

A persona instance must receive a grounding context that identifies:

- required approved assets and approved extracts;
- allowed operational references, if any, marked operational-only;
- prohibited source classes and excluded material;
- evidence expectations and citation requirements;
- confidence threshold and low/blocked handling;
- freshness expectation and stale/unknown handling;
- active caveats, limitations, and open questions;
- handoff and escalation requirements.

When template, grounding context, knowledge asset, and governance policy
requirements conflict, the stricter rule governs.

## Confidence and freshness rules

| Signal | Persona behavior |
| --- | --- |
| High confidence | May support committed output and reusable role behavior within approved scope. |
| Medium confidence | May support committed or draft output with caveat; behavior changes may require additional review. |
| Low confidence | Discovery, hypothesis, caveat, validation need, or promotion proposal only. |
| Blocked confidence | Must not ground committed behavior; escalate or record blocker. |
| Current freshness | Eligible for use within scope when other gates pass. |
| Recent freshness | Eligible when no known superseding decision or conflict exists. |
| Stale-risk freshness | Requires owner/reviewer confirmation before reusable reliance. |
| Superseded freshness | Historical reference only; cite replacement when known. |
| Unknown freshness | Treat as low confidence or open until clarified. |

## Escalation behavior

Persona templates must define escalation conditions and target reviewer roles.
Escalation is required when:

- required approved knowledge is missing;
- provenance, owner, reviewer, confidence, freshness, applicability, or
  limitations are absent for a material claim;
- a claim is low-confidence, blocked, assumed, open, stale-risk, unknown,
  conflicting, rejected, superseded, or prohibited;
- raw, research, operational-only, seed, or future candidate evidence is needed
  for more than discovery or promotion proposal;
- role scope, deliverable scope, source authority, or action authority is unclear;
- a persona behavior change, SME validation, source promotion, governance
  exception, or learning promotion is requested;
- sensitive data, tenancy, access, retention, deletion, compliance, provider,
  deployment, connector, storage, retrieval, or runtime choices are implicated
  without accepted decisions;
- completion criteria, validation expectations, or handoff requirements cannot
  be satisfied.

Escalation records should identify the blocker, affected workflow/persona,
evidence reviewed, required decision, owner, reviewer, and downstream impact.

## Output standards

Persona outputs are reviewable only when they include:

1. changed artifacts or generated deliverables with paths or stable IDs;
2. source and evidence summary for material claims;
3. confidence, freshness, assumptions, open questions, and limitations;
4. role and scope boundaries observed;
5. validation performed and validation not performed;
6. risks, blockers, dependency impacts, and required follow-up owners;
7. handoff notes for the next operator, reviewer, integrator, or persona;
8. learning signals or promotion recommendations when repeated issues appear;
9. confirmation that prohibited files, source classes, and action classes were
   not used as durable grounding.

Persona templates may add role-specific output standards, but they must not
remove the base requirements.

## Governance and review

### Required review gates

| Gate | Required decision | Persona system effect |
| --- | --- | --- |
| Template creation | Should this reusable role exist, and who owns it? | Creates candidate, proposed, approved, approved-with-limits, deferred, rejected, or blocked template state. |
| Allowed knowledge review | Which assets, extracts, source classes, and grounding contexts may the role consume? | Defines consumption boundary and prohibited sources. |
| SME/domain validation | Is expert guidance accurate, applicable, and bounded enough for reuse? | Allows SME guidance to support template behavior or blocks it as caveat/open item. |
| Persona behavior change | Should approved knowledge or learning alter role responsibilities, evidence rules, outputs, or escalation behavior? | Creates new version/change record or rejects/defers change. |
| Consumption readiness | Is this template and grounding context ready for a specific instance? | Allows ready, ready-with-caveats, review-needed, deferred, or blocked dispatch state. |
| Learning promotion | Should workflow learning change reusable behavior or another target? | Updates template only after promotion decision and audit record. |

### Review outcomes

Review decisions may approve, approve with limits, request changes, defer,
reject, supersede, escalate, block, or mark not applicable with rationale.
Reviewer rationale must preserve affected workflows, limitations, confidence and
freshness impact, follow-up owner, and downstream behavior impact.

## Versioning

Persona templates are versioned whenever reusable behavior changes. A new
version is required when any of these change:

- role purpose, expertise boundary, or responsibilities;
- allowed knowledge, prohibited sources, or action classes;
- evidence, confidence, freshness, or grounding rules;
- output standards, handoff requirements, or completion signals;
- escalation triggers or reviewer routing;
- SME guidance incorporated into reusable behavior;
- governance policy applicability;
- learning promotion that changes future role behavior.

Version records must include changed guidance, source references, evidence class,
confidence and freshness impact, reviewer rationale, affected workflows, prior
version, new version, lifecycle state, and follow-up owner.

Superseded versions remain traceable and may be referenced for history, risk, or
rollback analysis, but must not ground new work unless a later review decision
restores or supersedes them.

## Safe consumption

Synapse may instantiate a persona only when all applicable readiness gates pass
or are explicitly accepted with caveats:

| Gate | Ready condition | Blocks readiness when |
| --- | --- | --- |
| Template gate | Approved or approved-with-limits template version exists. | Template is candidate, proposed, review-needed, deferred, rejected, superseded without replacement, or blocked. |
| Grounding context gate | Required assets, allowed operational references, prohibited sources, confidence/freshness rules, caveats, and handoff requirements are explicit. | Context is missing, inconsistent, or authorizes prohibited use. |
| Provenance gate | Material guidance and claims include source references, evidence class, confidence, freshness, owner, applicability, and limitations. | Claims cannot be traced or caveats are dropped. |
| Applicability gate | Template, asset, and context scope match the assigned workflow/task/domain. | Persona or knowledge is used outside approved scope. |
| Governance gate | Applicable policy requirements are satisfied or not applicable with rationale. | Governance review, exception, or blocker is unresolved. |
| Output obligation gate | Required output, validation, handoff, and learning-capture expectations are visible. | The instance cannot produce a reviewable or safely consumable output. |

Ready-with-caveats consumption is allowed only when caveats are visible to the
operator and preserved in the persona instance, output, and handoff.

## Learning promotion

Persona instances should create learning signals when they reveal repeated or
high-impact:

- role-boundary ambiguity;
- source drift, stale knowledge, or missing provenance;
- confidence/freshness classification errors;
- repeated validation failures or review blockers;
- over-reliance on operational-only or future candidate evidence;
- output/handoff gaps;
- escalation routing gaps;
- successful recovery patterns that should become reusable;
- SME/domain guidance gaps;
- workflow or backlog readiness blockers.

Learning signals remain operational-only until reviewed. A learning signal may
be promoted to:

| Target | Promote when | Required review expectation |
| --- | --- | --- |
| Persona template | Learning changes role responsibilities, boundaries, evidence rules, output standards, prohibited behavior, or escalation behavior. | Persona/template owner and relevant reviewer accept behavior impact. |
| Knowledge asset or approved extract | Learning changes a reusable claim, limitation, applicability note, or source summary. | Knowledge owner confirms provenance, confidence, freshness, and scope. |
| Workflow template | Learning changes a repeatable workflow step, dependency, input, output, or handoff expectation. | Workflow owner confirms downstream impact. |
| Validator or quality gate | Learning reveals a repeatable objective check or review-only readiness gate. | QA/reviewer confirms deterministic versus review-only boundary. |
| Standard | Learning changes cross-role evidence, provenance, output, governance, or promotion expectations. | Standards owner and affected owner accept reusable rule. |
| Backlog gate or work item | Learning creates an implementation dependency, spike, blocker, risk, or future product decision. | Backlog owner records priority, owner, and blocking impact. |

Promotion must record target, owner, reviewer, source evidence, recurrence or
impact, confidence, freshness, affected workflows/personas, decision outcome,
and limitations.

## Non-goals

The MVP2 persona template system does not:

- define prompt syntax as the product model;
- choose a persona composition, inheritance, packaging, storage, retrieval,
  embedding, connector, provider, runtime, tenancy, access, compliance, privacy,
  retention, deletion, UI, or deployment implementation;
- approve sources, SME claims, persona changes, governance exceptions, or
  learning promotions automatically;
- treat raw, research, operational-only, seed, runtime, rejected, superseded, or
  ungoverned external material as durable persona knowledge without review;
- productize every possible domain pack, persona pack, expert workflow, or
  source system in MVP2.

## Acceptance criteria

| ID | Criterion |
| --- | --- |
| MVP2-PTS-AC-001 | A user can distinguish base persona rules, extended persona templates, persona instances, change records, and learning signals. |
| MVP2-PTS-AC-002 | A persona/template owner can define role purpose, expertise boundary, responsibilities, allowed knowledge, prohibited behavior, allowed action classes, evidence rules, output standards, and escalation behavior. |
| MVP2-PTS-AC-003 | A persona template exposes owner, reviewer, version, lifecycle state, source/provenance references, confidence, freshness, applicability, limitations, and affected workflows for behavior-affecting guidance. |
| MVP2-PTS-AC-004 | A persona instance cannot expand allowed knowledge beyond its approved template, grounding context, asset applicability, or governance limits. |
| MVP2-PTS-AC-005 | Low-confidence, blocked, stale-risk, unknown, assumed, open, conflicting, rejected, superseded, or prohibited material is surfaced as caveat, validation need, blocker, or escalation trigger before consumption. |
| MVP2-PTS-AC-006 | Persona behavior changes require source or learning provenance, reviewer rationale, version/change record, confidence/freshness impact, and affected workflow scope before reuse. |
| MVP2-PTS-AC-007 | Persona outputs preserve evidence, confidence, freshness, assumptions, open questions, limitations, validation status, handoff needs, and learning/promotion recommendations where applicable. |
| MVP2-PTS-AC-008 | Persona learning signals enter a promotion path with target type, owner, evidence, review state, decision outcome, and limitations rather than silently changing future behavior. |
| MVP2-PTS-AC-009 | The system remains product-facing and does not expose repository-only orchestration mechanics, raw/research material, or prompt-management details as the customer product model. |
| MVP2-PTS-AC-010 | The system preserves future storage, retrieval, embedding, connector, provider, tenancy, access, compliance, retention, deletion, UI, and runtime decisions as open implementation choices. |

## Open product decisions

| ID | Decision | Current handling |
| --- | --- | --- |
| MVP2-PTS-OQ-001 | Which first persona templates should ship as MVP2 product assets? | Use role-based templates until product owners select initial catalog. |
| MVP2-PTS-OQ-002 | Who are the named accountable owners and reviewers for first persona templates, SME validation, and persona behavior changes? | Use role-based owner/reviewer fields until named people or teams are accepted. |
| MVP2-PTS-OQ-003 | What user-facing surface should expose persona template registry, version history, readiness, and caveats? | Future/open; this document defines product semantics only. |
| MVP2-PTS-OQ-004 | What exact confidence thresholds block dispatch, allow ready-with-caveats, or allow draft-only persona work? | Use high/medium/low/blocked labels and escalation expectations until thresholds are accepted. |
| MVP2-PTS-OQ-005 | What freshness cadence or review SLA should apply by persona type or knowledge domain? | Use current/recent/stale-risk/superseded/unknown labels and owner review expectations only. |
| MVP2-PTS-OQ-006 | Which future source systems, external corpora, customer corpora, or domain packs may supply SME/persona knowledge? | Treat as future candidates until ownership, access, provenance, governance, and promotion rules are approved. |
| MVP2-PTS-OQ-007 | Which persona composition, inheritance, serialization, event, or validation format should implement these product contracts? | Future/open; product-facing template semantics remain implementation-neutral. |
