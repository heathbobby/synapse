# Synapse Product MVP1: Operator Journey

- **Status**: product-owner draft
- **MVP**: MVP1
- **Companion spec**: `docs/product/MVP1/AI_COWORKER_WORKSPACE.md`
- **Last updated**: 2026-05-03
- **Primary sources**:
  - `docs/refinement/iteration-inputs/product-mvp1-ai-coworker-workspace.md`
  - `docs/product/MVP_STRATEGY.md`
  - `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
  - `docs/product/PRODUCT_CAPABILITY_MAP.md`
  - `research/Synapse_Initial_Chat_Summary.md`
  - `docs/MVP1/Platform/ReleaseNotes.md`
  - `docs/implementation/IMPLEMENTATION_ROADMAP.md`

## Journey premise

MVP1 serves a human operator running one approved expert workflow in a Synapse
AI coworker workspace:

> Convert a bounded product initiative into an implementation-ready package with
> AI coworker drafts, human review gates, accepted outputs, and captured
> learnings.

The operator experience must feel like directing accountable coworkers, not
like operating internal orchestration tooling. Current CLI-assisted docs,
runtime task cards, memos, workflow YAML, and Cursor-specific conventions are
prototype scaffolding only. They may inform the journey but are not the
customer-facing product journey.

## Journey summary

| Stage | Operator intent | Synapse support | Primary output |
| --- | --- | --- | --- |
| 1. Start workspace | Turn an initiative into a guided workspace. | Creates a workspace and asks for destination, scope, constraints, success criteria, and owner. | Draft workspace brief. |
| 2. Select workflow | Choose the approved expert workflow. | Offers the MVP1 product concept-to-implementation workflow and explains stages/gates. | Confirmed workflow run. |
| 3. Attach knowledge | Ground AI coworkers in approved context. | Lets operator attach sources, record provenance/applicability, and mark known gaps. | Knowledge context set. |
| 4. Staff coworkers | Confirm role-based AI coworkers and reviewers. | Presents coworker roles, responsibilities, expected outputs, and escalation paths. | Staffing and review plan. |
| 5. Dispatch work | Start bounded AI coworker assignments. | Generates work packets with objectives, sources, deliverables, dependencies, and review expectations. | Active coworker tasks. |
| 6. Monitor progress | Understand what is happening and what needs attention. | Shows stage/task status, blockers, review-needed items, and completion signals. | Operator status view. |
| 7. Review outputs | Decide what can be trusted or revised. | Routes outputs through human review gates with evidence, assumptions, risks, and options. | Gate decisions. |
| 8. Assemble handoff | Package accepted work for implementation. | Combines accepted outputs, decisions, risks, blockers, owners, and open questions. | Implementation-ready package. |
| 9. Capture learning | Improve future runs without unsafe automatic promotion. | Records candidate updates to knowledge, personas, workflow, validators, or backlog gates. | Learning queue. |

## Personas in the journey

| Persona | Journey responsibility |
| --- | --- |
| Human operator | Owns destination, scope, dispatch, gate decisions, handoff acceptance, and learning promotion choices. |
| Product owner / initiative owner | Provides product intent, user value, requirements, non-goals, and acceptance posture. Often the same person as the operator in MVP1. |
| Domain reviewer | Reviews evidence, product fit, governance, risk, and readiness when the operator needs a second human judgment. |
| Implementation lead | Receives the final handoff and confirms whether outputs are actionable. |
| AI coworker | Produces bounded role-scoped drafts, critiques, synthesis, and handoff material under human review. |

## Stage details

### 1. Start workspace

**Operator goal**: Start from an initiative, not from tooling configuration.

**Operator sees**

- Workspace name and initiative summary.
- Prompt for destination, expected outcome, constraints, deadlines if known, and
  definition of done.
- Reminder that the operator remains accountable for final decisions.

**Human decisions**

- Is this initiative suitable for the MVP1 approved workflow?
- Who owns the workflow run?
- What outcomes are explicitly out of scope?

**Review gate**

- **G0: Launch readiness** - launch only if the initiative is bounded enough and
  the operator can provide approved context or name the missing context.

**Outputs**

- Workspace brief.
- Owner and stakeholder list.
- Initial assumptions and open questions.

### 2. Select approved expert workflow

**Operator goal**: Apply a reusable expert process without understanding
orchestration internals.

**Operator sees**

- Product concept-to-implementation workflow description.
- Stages, expected outputs, human gates, and estimated effort.
- Clear statement that the workflow is product-facing and tool-agnostic.

**Human decisions**

- Confirm the workflow.
- Accept the default stages or narrow the run.
- Decide whether any stage needs a named reviewer.

**Review gate**

- **G1: Scope and non-goals** - confirm the run matches MVP1 scope and does not
  drift into visual designer, production runtime, broad knowledge registry,
  legacy bridge automation, or other deferred product work.

**Outputs**

- Confirmed workflow run.
- Stage plan and review plan.
- Scope/non-goal record.

### 3. Attach approved knowledge

**Operator goal**: Ensure AI coworkers work from trusted context.

**Operator sees**

- Source attachment area for product strategy, product requirements, capability
  maps, research summaries, release notes, roadmap inputs, or other approved
  materials.
- For each source: provenance, owner if known, applicability, freshness if
  known, and usage constraints.
- Gap list for missing or insufficient source material.

**Human decisions**

- Which sources are approved for this workflow?
- Which claims must remain assumptions because sources are incomplete?
- Which sensitive or irrelevant materials must be excluded?

**Review gate**

- **G2: Evidence sufficiency** - decide whether attached context is enough for
  AI coworker work to proceed, whether additional sources are required, or
  whether outputs must carry explicit uncertainty labels.

**Outputs**

- Knowledge context set.
- Source gap list.
- Evidence and uncertainty expectations.

### 4. Staff AI coworkers and reviewers

**Operator goal**: Assign expert perspectives without turning them into opaque
automation.

**Operator sees**

- Recommended coworker roles for the approved workflow, such as product
  strategist, requirements reviewer, technical/implementation reviewer,
  quality/release reviewer, and integrator.
- Responsibilities, allowed context, expected deliverables, escalation behavior,
  and review gate participation.
- Reviewer roles for product fit, evidence sufficiency, governance/risk, and
  handoff readiness.

**Human decisions**

- Which AI coworker roles should run for this initiative?
- Which human review roles are mandatory?
- What autonomy level applies to each coworker: draft only, revise with review,
  recommend, or prepare handoff for approval?

**Review gate**

- Staffing approval by the operator before dispatch.

**Outputs**

- Coworker roster.
- Reviewer roster.
- Autonomy and escalation settings.

### 5. Dispatch bounded work

**Operator goal**: Start AI coworker work with clear task boundaries.

**Operator sees**

- Work packets for each coworker containing:
  - Objective.
  - Approved sources.
  - Deliverables.
  - Dependencies.
  - Prohibited or deferred topics.
  - Review expectations.
  - Completion signal.
- Warning if required setup fields are missing.

**Human decisions**

- Dispatch, edit, hold, or cancel each work packet.
- Resolve conflicts between tasks before work starts.
- Decide whether a partial run is acceptable.

**Review gate**

- Dispatch confirmation: no AI coworker task starts without an operator-approved
  objective, source context, deliverable, and review expectation.

**Outputs**

- Active AI coworker assignments.
- Task status baseline.
- Dependency and blocker baseline.

### 6. Monitor workflow progress

**Operator goal**: Know what is progressing, blocked, done, or waiting for human
attention.

**Operator sees**

- Stage timeline.
- Coworker task statuses: not started, active, blocked, review needed, revision
  requested, accepted, rejected, or escalated.
- Blockers, missing context, risk flags, and handoff readiness indicators.
- Activity summaries in product language rather than runtime log mechanics.

**Human decisions**

- Provide missing context.
- Reassign or revise a task.
- Pause, cancel, or continue the workflow.
- Escalate blocked or risky work to a reviewer.

**Review gate**

- Blocker/recovery review when any task becomes blocked, partial, failed,
  conflicted, or unsafe to rely on.

**Outputs**

- Current workflow status.
- Blocker and recovery register.
- Review queue.

### 7. Review AI coworker outputs

**Operator goal**: Accept only evidence-backed, useful work into the handoff.

**Operator sees**

- Output summary.
- Source references or evidence notes.
- Assumptions, risks, open questions, and confidence limits.
- Diff or change summary where relevant.
- Decision options: approve, reject, request revision, escalate.

**Human decisions**

- Does the output satisfy the product objective?
- Is the evidence sufficient?
- Are user value, requirements, non-goals, risks, and implementation implications
  clear?
- Does a reviewer need to make or confirm the decision?

**Review gates**

- **G2: Evidence sufficiency** - accept, revise, or mark uncertainty.
- **G3: Product fit** - ensure outputs describe Synapse product value and user
  behavior, not internal scaffolding.
- **G4: Risk and governance** - confirm sensitive decisions, ownership, and
  risk treatment are visible.

**Outputs**

- Gate decision records with rationale.
- Accepted outputs.
- Revision requests or escalations.
- Updated risk/open decision register.

### 8. Assemble implementation handoff

**Operator goal**: Produce a package that downstream implementers can safely use.

**Operator sees**

- Handoff package preview with accepted outputs, decisions, requirements,
  non-goals, risks, blockers, dependencies, owners, and open product decisions.
- Readiness checklist.
- Conditional handoff warnings if reviews or source gaps remain unresolved.

**Human decisions**

- Is the package implementation-ready, conditionally ready, or blocked?
- Who owns each unresolved decision or recovery action?
- Which outputs are accepted for downstream reliance?

**Review gate**

- **G5: Handoff readiness** - package may be handed off only when accepted
  outputs, limitations, and follow-up owners are explicit.

**Outputs**

- Implementation-ready or conditionally ready package.
- Open decision and recovery owner list.
- Downstream acceptance notes.

### 9. Capture workflow learning

**Operator goal**: Make the next run smarter without silently changing reusable
behavior.

**Operator sees**

- Suggested learning items from outputs, reviews, blockers, repeated revisions,
  and handoff feedback.
- Candidate target for each learning item: knowledge, persona guidance, workflow
  template, review gate, validation rule, backlog readiness, or product decision.
- Required owner and recommended action.

**Human decisions**

- Promote, investigate, defer, or reject each learning candidate.
- Decide whether learning needs separate governance review.
- Assign an owner for accepted learning.

**Review gate**

- **G6: Learning promotion** - no reusable product behavior changes without a
  human decision and rationale.

**Outputs**

- Learning queue.
- Promotion decisions.
- Future workflow improvement backlog.

## End-to-end outputs

At the end of a successful MVP1 run, Synapse should provide:

1. Workspace brief and scope/non-goals.
2. Knowledge context set and source gaps.
3. Coworker roster, reviewer roster, and work packets.
4. Status, blocker, and recovery records.
5. Review gate decisions with rationale.
6. Accepted product requirements and supporting product outputs.
7. Implementation handoff package.
8. Learning queue with promotion decisions or owners.

## Review gate map

| Gate | Moment | Human decision | Required record |
| --- | --- | --- | --- |
| G0: Launch readiness | Before workflow run starts | Is the initiative bounded and grounded enough? | Launch, revise setup, or block with owner. |
| G1: Scope and non-goals | After workflow selection | Does the run fit MVP1 scope? | Approved scope/non-goals or escalation. |
| G2: Evidence sufficiency | Before accepting source-backed outputs | Is evidence adequate for reliance? | Accept, revise, or label uncertainty. |
| G3: Product fit | Before product outputs enter handoff | Is this product-facing and user-value oriented? | Accept, revise, or block. |
| G4: Risk and governance | Before risky or sensitive decisions are accepted | Are risks, owners, and approval needs clear? | Accept, mitigate, or escalate. |
| G5: Handoff readiness | Before downstream implementation use | Can the package be safely consumed? | Ready, conditional, or blocked. |
| G6: Learning promotion | After handoff | Should a lesson become reusable behavior? | Promote, investigate, defer, or reject. |

## Operator success criteria

| ID | Success criterion |
| --- | --- |
| MVP1-JOURNEY-001 | The operator can start from an initiative and reach a structured workspace without touching prototype orchestration internals. |
| MVP1-JOURNEY-002 | The operator can see which sources ground the workflow and which claims remain assumptions or open questions. |
| MVP1-JOURNEY-003 | The operator can dispatch role-scoped AI coworker work only after reviewing objective, sources, deliverables, dependencies, and gate expectations. |
| MVP1-JOURNEY-004 | The operator can monitor status and blockers in product terms. |
| MVP1-JOURNEY-005 | The operator can approve, reject, revise, or escalate outputs with rationale. |
| MVP1-JOURNEY-006 | The operator can produce a handoff package that distinguishes accepted outputs from risks, blockers, assumptions, and open decisions. |
| MVP1-JOURNEY-007 | The operator can capture learning candidates without automatically changing reusable product behavior. |

## Non-goals for the MVP1 journey

- The journey does not require a visual workflow designer.
- The journey does not require a production workflow-run database or event bus.
- The journey does not expose Cursor, current runtime memos, generated task
  cards, or YAML workflow files as customer concepts.
- The journey does not support arbitrary expert workflow creation.
- The journey does not automate final approval, risk acceptance, or learning
  promotion.
- The journey does not include multi-tenant administration, billing, compliance
  implementation, or external legacy-system integration.

## Open product decisions

| ID | Decision | Impact on journey |
| --- | --- | --- |
| MVP1-JOQ-001 | Which customer-facing form should the workspace take first: web app, local app, guided document workspace, or hybrid console? | Determines interaction design, persistence, and authentication assumptions. |
| MVP1-JOQ-002 | Which human roles are required versus optional for each gate? | Determines review routing and operator friction. |
| MVP1-JOQ-003 | What is the minimum acceptable evidence display for source-backed AI coworker outputs? | Determines review UX and trust model. |
| MVP1-JOQ-004 | How much task editing can the operator do before dispatch? | Determines flexibility versus workflow consistency. |
| MVP1-JOQ-005 | What handoff format should implementation leads receive first? | Determines export, integration, and downstream acceptance behavior. |
| MVP1-JOQ-006 | Which learning targets can be captured in MVP1 without implementing full MVP2/MVP3 registries? | Determines whether learning is a queue, backlog, or lightweight product object. |
