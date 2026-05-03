# Synapse Product MVP1: AI Coworker Workspace

- **Status**: product-owner draft
- **MVP**: MVP1
- **Last updated**: 2026-05-03
- **Primary sources**:
  - `docs/refinement/iteration-inputs/product-mvp1-ai-coworker-workspace.md`
  - `docs/product/MVP_STRATEGY.md`
  - `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
  - `docs/product/PRODUCT_CAPABILITY_MAP.md`
  - `research/Synapse_Initial_Chat_Summary.md`
  - `docs/MVP1/Platform/ReleaseNotes.md`
  - `docs/implementation/IMPLEMENTATION_ROADMAP.md`

## Product definition

Synapse Product MVP1 is an **AI coworker workspace** where a human operator can
take one approved expert workflow from destination-setting through AI-assisted
execution, human review, implementation handoff, and learning capture.

For MVP1, the approved expert workflow is:

> **Product concept-to-implementation workflow**: convert a bounded product
> initiative into an implementation-ready package containing source-grounded
> requirements, workflow scope, review decisions, delivery outputs, risks,
> blockers, and follow-up learning.

This workflow is selected because the current repository already proves the
underlying operating pattern through product/refinement, release, and roadmap
artifacts. Synapse must translate that pattern into a product experience for
human operators and AI coworkers, not expose the current CLI, runtime memos,
Cursor rules, workflow YAML, or repository-specific orchestration internals as
the customer product.

In short: Synapse MVP1 is not `cursor_orchestrator`; `cursor_orchestrator` is
prototype scaffolding used to help define and validate this product experience.

## Product/tooling boundary

| Concern | MVP1 product treatment |
| --- | --- |
| Synapse workspace | Product surface for setup, dispatch, monitoring, review, handoff, and learning capture. |
| AI coworkers | Product-managed role participants assigned bounded work with context, outputs, and review gates. |
| Expert workflow | Reusable product workflow template with stages, inputs, decisions, gates, and outputs. |
| Knowledge context | Approved sources attached to the workflow with ownership, provenance, and applicability visible to the operator. |
| Current CLI/orchestration docs | Prototype scaffolding and evidence only. They may inform concepts, but are not customer-facing product mechanics. |
| Runtime memos/task cards | Prototype evidence only. Product MVP1 should define user-visible task, review, output, and learning objects independently. |

## MVP1 product scope

### In scope

MVP1 shall enable one operator to run one approved expert workflow with AI
coworker assistance:

1. Define the workflow destination, scope, constraints, and success criteria.
2. Select the approved product concept-to-implementation workflow.
3. Attach approved knowledge sources and mark any known gaps.
4. Select or confirm role-based AI coworkers for the workflow.
5. Generate bounded work packets for each coworker role.
6. Dispatch work and monitor stage/task status.
7. Review AI coworker outputs at explicit human gates.
8. Approve, reject, request revision, or escalate outputs.
9. Assemble the accepted handoff package.
10. Capture learnings for future knowledge, persona, workflow, validator, or
    backlog improvements.

### Deferred from MVP1

- Multi-workflow marketplace or full workflow template library.
- Visual drag-and-drop workflow designer.
- Fully automated workflow execution without human ownership.
- Broad knowledge registry, source ingestion pipeline, or SME persona registry.
- Live event bus, telemetry backend, workflow-run database, product API, or
  production approval automation.
- Multi-tenant administration, billing, compliance implementation, or external
  customer deployment model.
- Legacy bridge adapters or domain-specific migration automation.

## Primary personas

| Persona | Role in MVP1 | Needs |
| --- | --- | --- |
| Human operator | Owns destination, scope, decisions, approvals, and final handoff. | Clear setup path, visible progress, evidence-backed outputs, confidence in what needs review. |
| Product owner / initiative owner | Defines product value, scope, non-goals, requirements, and acceptance posture. | Translate ambiguous initiative ideas into implementation-ready product decisions. |
| Domain reviewer | Reviews evidence, risk, governance, and product fit at gates. | Understand what changed, why it is supported, and what remains uncertain. |
| Implementation lead | Consumes the final handoff package. | Clear requirements, dependencies, risks, acceptance criteria, and open decisions. |
| AI coworker | Performs bounded expert work under a role/persona with sources and deliverables. | Precise task context, allowed sources, expected outputs, quality gates, and escalation rules. |

## Jobs to be done

| ID | Job |
| --- | --- |
| JTBD-MVP1-001 | When I have a product initiative, I want Synapse to help structure the work so I can move from ambiguity to an implementation-ready package. |
| JTBD-MVP1-002 | When AI coworkers produce work, I want to see their sources, assumptions, confidence limits, and review needs so I can decide whether to trust or revise the output. |
| JTBD-MVP1-003 | When multiple expert perspectives are needed, I want Synapse to coordinate role-scoped tasks so work does not become an unreviewable pile of disconnected AI drafts. |
| JTBD-MVP1-004 | When a workflow completes, I want accepted decisions and lessons to be captured so the next workflow starts smarter. |
| JTBD-MVP1-005 | When work is not ready, I want blockers, recovery actions, and accountable owners to be visible before downstream teams rely on it. |

## User value

MVP1 creates value by:

- Reducing the product owner's time spent translating vague initiatives into
  structured execution artifacts.
- Making AI coworker work reviewable through explicit source context, task
  boundaries, outputs, gates, and decisions.
- Scaling principal-level workflow discipline without requiring every user to
  know the underlying orchestration mechanics.
- Keeping humans accountable for destination, scope, risk acceptance, and final
  promotion of reusable behavior.
- Turning each completed workflow into learning that improves future workflows.

## Product requirements

| ID | Requirement | Source alignment |
| --- | --- | --- |
| MVP1-WORKSPACE-001 | Synapse shall provide a workspace for one approved expert workflow: product concept-to-implementation. | CAP-001, CAP-002; SYN-PRD-009 |
| MVP1-WORKSPACE-002 | Synapse shall let the operator define destination, scope, constraints, success criteria, and non-goals before dispatch. | SYN-PRD-009 |
| MVP1-WORKSPACE-003 | Synapse shall let the operator attach approved knowledge context and identify known source gaps. | SYN-PRD-001; CAP-003 precursor |
| MVP1-WORKSPACE-004 | Synapse shall present role-based AI coworkers with responsibilities, allowed context, expected outputs, and escalation behavior. | SYN-PRD-002 precursor; CAP-004 precursor |
| MVP1-WORKSPACE-005 | Synapse shall produce bounded work packets for AI coworkers, including objective, sources, deliverables, dependencies, review expectations, and completion signal. | CAP-002 |
| MVP1-WORKSPACE-006 | Synapse shall show workflow stage and coworker task status in operator-friendly terms. | CAP-006 precursor |
| MVP1-WORKSPACE-007 | Synapse shall require human review gates before outputs are accepted into the implementation handoff package. | SYN-PRD-005; CAP-005 precursor |
| MVP1-WORKSPACE-008 | Synapse shall support approve, reject, request revision, and escalate decisions with rationale. | SYN-PRD-005, SYN-PRD-009 |
| MVP1-WORKSPACE-009 | Synapse shall assemble accepted outputs into a product-facing implementation handoff package. | CAP-002, CAP-001 |
| MVP1-WORKSPACE-010 | Synapse shall capture workflow learnings as candidate updates to knowledge, personas, workflow templates, validators, or backlog gates. | SYN-PRD-006; CAP-007 precursor |
| MVP1-WORKSPACE-011 | Synapse shall distinguish accepted facts, assumptions, open questions, risks, blockers, and review-only judgments. | SYN-PRD-001, SYN-PRD-009 |
| MVP1-WORKSPACE-012 | Synapse shall keep prototype scaffolding references out of the customer-facing workflow unless shown as implementation evidence for internal operators. | MVP strategy product/tooling boundary |

## Product objects for MVP1

| Object | Description | MVP1 persistence expectation |
| --- | --- | --- |
| Workspace | Container for one workflow run, its operator, context, tasks, decisions, outputs, and learning. | Durable enough to resume and audit one workflow. |
| Workflow template | Approved concept-to-implementation sequence with stages, inputs, gates, and outputs. | Versioned template reference. |
| Workflow run | A specific execution of the template for one product initiative. | State, owner, current stage, status, timestamps, and output links. |
| Knowledge attachment | Approved source or context attached to the run. | Source name, owner if known, provenance, applicability, known gaps. |
| AI coworker role | Role-bound agent participant such as product strategist, reviewer, architect, QA/release reviewer, or integrator. | Role, responsibility, allowed context, output expectations. |
| Work packet | Bounded assignment for an AI coworker or human reviewer. | Objective, source context, deliverables, dependencies, status, review needs. |
| Review gate | Human decision point before promotion or handoff. | Decision, reviewer, rationale, affected outputs, follow-up action. |
| Handoff package | Accepted product and implementation-readiness outputs for downstream execution. | Accepted artifacts, open decisions, risks, blockers, owners, validation/review state. |
| Learning item | Candidate improvement discovered during or after the run. | Target type, evidence, proposed change, owner, status. |

## Human decisions and review gates

| Gate | Required human decision | Possible outcomes |
| --- | --- | --- |
| G0: Launch readiness | Is the initiative bounded enough, and are approved sources available? | Launch, revise setup, block pending source/scope decision. |
| G1: Scope and non-goals | Does the workflow scope match the product objective and MVP boundary? | Approve scope, narrow scope, escalate product decision. |
| G2: Evidence sufficiency | Are outputs grounded enough for downstream reliance? | Accept, request source-backed revision, mark assumption/open question. |
| G3: Product fit | Do requirements and outputs express user value rather than internal tooling mechanics? | Accept, revise, block product-facing handoff. |
| G4: Risk and governance | Are risks, sensitive data, approvals, and ownership clear enough? | Accept, require mitigation, escalate. |
| G5: Handoff readiness | Can the implementation lead safely consume the package? | Handoff, conditional handoff, block with recovery owner. |
| G6: Learning promotion | Which lessons should become reusable product assets? | Promote candidate, defer, reject with rationale. |

## MVP1 outputs

The product concept-to-implementation workflow should produce:

1. Product initiative summary.
2. Personas and jobs-to-be-done.
3. Product scope, non-goals, and assumptions.
4. Product requirements with trace to capability or product requirement IDs.
5. Review gate decisions and unresolved open product decisions.
6. Risk, blocker, dependency, and recovery register.
7. Accepted implementation handoff package.
8. Learning capture queue for future knowledge, persona, workflow, validation, or
   backlog improvements.

## Learning capture

Synapse MVP1 should capture learning without automatically promoting it into
canonical reusable behavior. Every learning item should include:

- What was learned.
- Evidence or workflow output that supports it.
- Whether it affects knowledge, persona behavior, workflow template, review
  gate, validation rule, or backlog readiness.
- Human owner for review.
- Recommended action: promote, investigate, defer, or reject.

Promotion into reusable assets remains a human-reviewed decision in MVP1.

## Non-goals

- Synapse MVP1 is not a prompt library.
- Synapse MVP1 is not a documentation generator for this repository.
- Synapse MVP1 is not `cursor_orchestrator` or the current orchestration
  framework.
- Synapse MVP1 does not expose Cursor-specific concepts as required customer
  concepts.
- Synapse MVP1 does not attempt full autonomy, multi-tenant SaaS operations, or
  production-grade workflow runtime infrastructure.
- Synapse MVP1 does not productize every expert workflow at once.

## Open product decisions

| ID | Decision | Impact |
| --- | --- | --- |
| MVP1-OQ-001 | What is the first customer-facing surface: local workspace, web app, hybrid app, or internal product console? | Determines UX, persistence, authentication, and deployment architecture. |
| MVP1-OQ-002 | Who is the named first target user or team for the product concept-to-implementation workflow? | Determines persona prioritization, workflow vocabulary, and acceptance criteria. |
| MVP1-OQ-003 | What level of durable state must Synapse own in MVP1 versus store in existing work systems? | Determines data model, audit, and recovery behavior. |
| MVP1-OQ-004 | Which review gates are mandatory for every run versus configurable by workflow owner? | Determines governance and operator friction. |
| MVP1-OQ-005 | What qualifies a knowledge attachment as approved for MVP1? | Determines source governance and evidence sufficiency. |
| MVP1-OQ-006 | What AI coworker autonomy levels are allowed for draft, revise, approve, and handoff actions? | Determines permissions, accountability, and risk controls. |
| MVP1-OQ-007 | Which learning items may be promoted immediately, and which require separate governance review? | Determines safety of the self-augmenting feedback loop. |
| MVP1-OQ-008 | What implementation artifact format should the handoff package use first? | Determines integration with downstream product, engineering, or delivery tools. |
