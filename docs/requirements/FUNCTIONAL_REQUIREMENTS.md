# Synapse Functional Requirements

- **Status**: draft canonical foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `concept-extraction`
- **Last updated**: 2026-05-03
- **Primary PRD reference**: `docs/requirements/PRODUCT_REQUIREMENTS.md`

## Source Register

| Source ID | Source | How this document uses it |
| --- | --- | --- |
| S1 | `research/Synapse_Initial_Chat_Summary.md` | Candidate product capabilities: grounded knowledge, SME agents, visual workflow designer, hybrid event bus, OOP prompting, live monitoring, feedback loop, legacy bridge. |
| S2 | `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md` | Functional process requirements for canonical docs, orchestration, role agents, deterministic validation, backlog traceability, feedback collection, and quality gates. |
| S3 | `work_items/synapse-product-brief.md` | Project-stage constraints and explicit uncertainty policy. |
| S4 | `docs/refinement/iteration-inputs/concept-extraction.md` | Completion criteria for canonical requirements and backlog initialization. |

## Requirement Status Legend

- **Source-backed**: Supported directly by source text.
- **Assumption**: Needed to make the requirement testable but requires sponsor validation.
- **Open question**: Missing decision prevents complete acceptance criteria.
- **Validation need**: Research, prototype, stakeholder decision, or architecture spike needed before implementation commitment.

## Traceability Map

| Product requirement | Functional requirement IDs |
| --- | --- |
| PRD-001 Canonical documentation truth | FR-001, FR-002, FR-003 |
| PRD-002 Provenance and uncertainty | FR-002, FR-004 |
| PRD-003 Role-based orchestration | FR-005, FR-006, FR-007, FR-008 |
| PRD-004 Persona/template structures | FR-009, FR-010 |
| PRD-005 Concept-to-implementation workflows | FR-005, FR-006, FR-007, FR-008 |
| PRD-006 Human review and monitoring | FR-013, FR-014, FR-015 |
| PRD-007 Feedback loop | FR-016, FR-017 |
| PRD-008 Backlog generation | FR-018, FR-019, FR-020 |
| PRD-009 Domain-agnostic configurability | FR-021, FR-022 |
| PRD-010 Legacy bridge workflow | FR-023 |

## Functional Requirements

### Canonical Documentation and Traceability

#### FR-001: Canonical document registry

**Status**: Source-backed
**As a** human operator, **I need** Synapse to maintain a known set of canonical documentation locations, **so that** downstream agents and humans can cite one source of truth.

**Acceptance criteria**

- Given a Synapse initiative, when canonical docs are initialized, then requirements, architecture, planning, standards, work items, and refinement docs have explicit target paths.
- Given an agent starts work, when it needs product context, then it can identify canonical docs rather than raw seed files as implementation truth.
- Given a canonical document changes, when downstream work references it, then the reference uses the canonical path.

**Source / evidence**

- Canonical truth model and target docs. [S2]
- Concept-extraction completion criteria for canonical docs. [S4]

**Validation needs**

- Confirm whether the long-term canonical root remains `docs/` or must support external repositories / workspaces.

#### FR-002: Source attribution and uncertainty labeling

**Status**: Source-backed
**As a** product stakeholder, **I need** requirements to distinguish facts, assumptions, open questions, and validation needs, **so that** unsupported hypotheses are not mistaken for committed scope.

**Acceptance criteria**

- Given a requirement is created, when it is saved, then it includes source/evidence and a status label.
- Given a requirement depends on interpretation, when it is documented, then the assumption is explicit and tied to a validation need or open question.
- Given an unsupported product detail is requested, when no source exists, then it is recorded as an open question rather than invented.

**Source / evidence**

- Product brief uncertainty policy. [S3]
- Concept-extraction goal to preserve uncertainty. [S4]

#### FR-003: Immutable source handling

**Status**: Source-backed
**As a** repository maintainer, **I need** raw or research seed inputs to remain unmodified during canonical drafting, **so that** source provenance remains intact.

**Acceptance criteria**

- Given an agent performs concept extraction, when it writes outputs, then it writes only to approved canonical deliverables.
- Given seed material is referenced, when a requirement cites it, then it cites the file path without altering the seed.

**Source / evidence**

- Playbook immutable seeds principle. [S2]
- User instruction for this iteration: do not edit `raw/` or `research/` files.

#### FR-004: Open question and validation-need tracking

**Status**: Source-backed
**As a** product stakeholder, **I need** open questions and validation needs to be captured alongside requirements, **so that** downstream agents know which details are committed and which require sponsor or market evidence.

**Acceptance criteria**

- Given a requirement contains unsupported detail, when it is documented, then the unsupported detail is marked as an assumption, open question, or validation need.
- Given an open question blocks delivery planning, when the backlog is reviewed, then the blocking relationship is visible.
- Given validation evidence is collected later, when a requirement is updated, then its status can be promoted or revised with source attribution.

**Source / evidence**

- Product brief asks agents to prefer explicit open questions over invented certainty. [S3]
- Concept-extraction packet requires preservation of source uncertainty and explicit gaps. [S4]

### Workflow Orchestration

#### FR-005: Workflow definition support

**Status**: Source-backed
**As a** human operator, **I need** Synapse workflows to define phases, iterations, source references, roles, deliverables, dependencies, and completion criteria, **so that** concept-to-implementation work is repeatable.

**Acceptance criteria**

- Given a workflow definition, when it is inspected, then it identifies phase/iteration names, participating roles, source references, and target deliverables.
- Given an iteration has upstream dependencies, when a launch is considered, then the dependency status is visible before work starts.
- Given a workflow is adapted to a new initiative, when domain-specific details change, then the standard cadence remains traceable.

**Source / evidence**

- Playbook workflow YAML and six-iteration cadence. [S2]
- Concept-extraction packet workflow metadata. [S4]

**Open questions**

- What workflow authoring surface is required for non-technical users?

#### FR-006: Role-agent task packets

**Status**: Source-backed
**As a** specialized role agent, **I need** a bounded task packet with context, files, quality criteria, and source references, **so that** I can produce consistent artifacts without ad hoc coordination.

**Acceptance criteria**

- Given a role-agent task starts, when it reads its task packet, then it can identify its role, scope, source files, target files, and success criteria.
- Given multiple agents run in parallel, when their task packets are generated, then each agent has disjoint write targets unless explicit coordination is required.

**Source / evidence**

- Specialized agent role library and iteration anatomy. [S2]

#### FR-007: Deterministic validation hooks

**Status**: Source-backed
**As a** human operator, **I need** workflow completion to be validated by deterministic checks where possible, **so that** progress does not rely only on agent self-reporting.

**Acceptance criteria**

- Given an iteration completes, when validation runs, then expected files, minimum content thresholds, required sections, or equivalent checks are evaluated.
- Given validation fails, when results are reported, then missing or insufficient artifacts are listed with actionable next steps.

**Source / evidence**

- `validate_iteration.sh` model and quality gates. [S2]

**Validation needs**

- Define Synapse-specific validators beyond file existence and size.

#### FR-008: Completion signaling

**Status**: Source-backed
**As a** workflow monitor, **I need** agents to emit standardized completion or partial-completion signals, **so that** orchestration can distinguish done, blocked, and token-limited work.

**Acceptance criteria**

- Given an agent finishes all assigned deliverables, when it reports completion, then it uses the agreed completion signal format.
- Given an agent cannot complete all deliverables, when it reports partial completion, then it lists completed items, remaining items, and recommended recovery work.

**Source / evidence**

- Playbook completion signal protocol. [S2]

### Knowledge Grounding and Persona Templates

#### FR-009: SME/persona template library

**Status**: Source-backed at concept level
**As a** principal or subject-matter expert, **I need** reusable SME/persona templates, **so that** expertise can be encoded and reused by agents.

**Acceptance criteria**

- Given a persona template exists, when an agent is instantiated from it, then the agent receives role perspective, core values, responsibilities, source references, and output standards.
- Given a template is updated, when future agents are generated, then the updated guidance is available to them.

**Source / evidence**

- SME agent and OOP prompting concepts. [S1]
- Role definition anatomy. [S2]

**Open questions**

- Should template inheritance be implemented as explicit object inheritance, configuration composition, or prompt includes?

#### FR-010: Knowledge source grounding

**Status**: Source-backed
**As a** specialized role agent, **I need** access to current canonical knowledge and relevant source excerpts, **so that** outputs are grounded and hallucination risk is reduced.

**Acceptance criteria**

- Given an agent receives a task, when sources are provided, then canonical docs and approved source references are listed.
- Given a source gap exists, when the agent needs a missing fact, then it records an open question or validation need.

**Source / evidence**

- Backfilling truth and hallucination reduction pillar. [S1]
- Canonical docs and source references in the playbook. [S2]

**Validation needs**

- Identify first supported source types and retrieval/update mechanics.

### Human Collaboration, Monitoring, and Approvals

#### FR-013: Workflow monitoring surface

**Status**: Source-backed at concept level
**As a** human coworker/operator, **I need** live visibility into workflow progress, **so that** I can monitor autonomous work and intervene when necessary.

**Acceptance criteria**

- Given a workflow is running, when a user views it, then each active iteration or agent has status, target deliverables, and last known signal.
- Given a workflow stalls or fails validation, when the monitor updates, then the issue is visible.

**Source / evidence**

- Visual workflow designer with live monitors. [S1]
- Monitoring and validation process. [S2]

**Validation needs**

- Determine whether MVP1 requires a UI, CLI/status file, or both.

#### FR-014: Human approval checkpoints

**Status**: Source-backed at concept level
**As a** human operator, **I need** explicit approval checkpoints for high-impact steps, **so that** agent autonomy remains governed.

**Acceptance criteria**

- Given a workflow reaches a configured approval step, when approval is required, then downstream execution is paused until approved or rejected.
- Given approval is granted or denied, when the workflow resumes or stops, then the decision is recorded.

**Source / evidence**

- Hybrid event bus supporting synchronous human-in-loop approvals. [S1]

**Open questions**

- Which actions require approval in the first release?

#### FR-015: Visual workflow design

**Status**: Source-backed concept, implementation details open
**As a** workflow author, **I need** a way to define and inspect workflows visually or structurally, **so that** orchestration can be understood and modified by humans.

**Acceptance criteria**

- Given a workflow definition exists, when a user views it, then phases, dependencies, roles, and deliverables are understandable.
- Given nested workflows are supported, when a user expands a workflow, then sub-workflow boundaries and dependencies are clear.

**Source / evidence**

- Visual workflow designer with drag-and-drop canvas and nested workflows. [S1]

**Validation needs**

- Confirm whether drag-and-drop is required for MVP1 or can be deferred behind YAML/Markdown definitions.

### Feedback and Continuous Improvement

#### FR-016: Feedback capture

**Status**: Source-backed
**As a** workflow owner, **I need** each iteration to capture feedback about completion, quality, and failure modes, **so that** the system can improve over time.

**Acceptance criteria**

- Given an iteration ends, when feedback is collected, then it records target artifacts, completed artifacts, completion rate, issues, and recommended improvements.
- Given a recurring issue is detected, when feedback is reviewed, then it can be linked to a template, role, workflow, or process update.

**Source / evidence**

- Knowledge loop and feedback application model. [S1, S2]

#### FR-017: Template/process improvement promotion

**Status**: Source-backed
**As a** workflow owner, **I need** validated learnings to update templates, role definitions, or process docs, **so that** future iterations get measurably better.

**Acceptance criteria**

- Given a feedback item identifies a repeatable pattern, when it is accepted, then the corresponding template, role definition, or workflow guidance is updated.
- Given a learning is applied, when future task packets are generated, then the learning is included.

**Source / evidence**

- Self-augmenting feedback loop. [S1]
- Continuous improvement loop and pattern/action matrix. [S2]

### Backlog Generation and Readiness

#### FR-018: Epic and story generation

**Status**: Source-backed
**As a** product owner, **I need** Synapse to generate epics and candidate stories from canonical requirements, **so that** product concepts can become implementation-ready backlog.

**Acceptance criteria**

- Given canonical PRD and FR documents exist, when backlog generation runs, then candidate MVPs, domains, epics, and stories are proposed with confidence and gaps.
- Given a story is proposed, when it is reviewed, then it links to product and functional requirements.

**Source / evidence**

- Playbook backlog model and concept-extraction completion criteria. [S2, S4]

#### FR-019: Readiness gates

**Status**: Source-backed
**As a** delivery lead, **I need** stories to expose readiness gates, **so that** implementation starts only when product, architecture, and quality views agree.

**Acceptance criteria**

- Given a story is in the backlog, when its status is assessed, then product, technical, quality, dependency, and risk readiness are visible.
- Given a gate is incomplete, when the story is reviewed, then the blocking gap is explicit.

**Source / evidence**

- Playbook work-item quality gates. [S2]

#### FR-020: Dependency and concurrency mapping

**Status**: Source-backed
**As a** delivery planner, **I need** backlog items to identify dependencies and safe parallelism, **so that** agent and human work can be sequenced efficiently.

**Acceptance criteria**

- Given a backlog item depends on another artifact or decision, when it is documented, then the dependency is listed.
- Given multiple items can run concurrently, when planning work, then safe and unsafe parallelism are distinguishable.

**Source / evidence**

- Playbook concurrency model. [S2]
- Concept-extraction completion criteria for concurrency analysis. [S4]

### Domain-Agnostic Configuration and Legacy Bridge

#### FR-021: Domain configuration

**Status**: Source-backed
**As a** workflow administrator, **I need** domains, roles, artifact types, and quality thresholds to be configurable per initiative, **so that** Synapse can operate across use cases.

**Acceptance criteria**

- Given a new initiative starts, when configuration is authored, then domains, roles, workflows, and artifact targets can be tailored without rewriting the core orchestration model.

**Source / evidence**

- Domain-agnostic platform vision. [S1]
- Adaptation playbook. [S2]

#### FR-022: Implementation-agnostic execution boundary

**Status**: Source-backed at concept level
**As a** platform owner, **I need** Synapse to separate product/workflow intent from implementation-specific tooling, **so that** it can adapt to different environments.

**Acceptance criteria**

- Given a workflow is defined, when runtime tools change, then the canonical requirements and task structure remain stable where possible.
- Given an integration is environment-specific, when documented, then it is isolated behind configuration or adapter boundaries.

**Source / evidence**

- Domain-agnostic and implementation-agnostic platform statement. [S1]

**Validation needs**

- Define which runtime abstractions are required in MVP1.

#### FR-023: Legacy-to-greenfield transition workflow

**Status**: Source-backed use-case hypothesis
**As a** modernization team, **I need** Synapse to help extract requirements from legacy operational reality into future-state architecture/backlog artifacts, **so that** transition-state work becomes manageable.

**Acceptance criteria**

- Given a legacy-transition initiative, when source materials are analyzed, then Synapse can produce requirements, current-state assumptions, future-state gaps, and candidate migration epics.
- Given legacy constraints are unknown, when requirements are drafted, then the gaps are captured as validation needs.

**Source / evidence**

- Legacy bridge pillar and WebPT / Project Horizon example. [S1]

**Validation needs**

- Validate a concrete legacy-transition customer, source corpus, and migration workflow before committing to release scope.

## Cross-Cutting Open Questions

| OQ ID | Question | Affected FRs |
| --- | --- | --- |
| OQ-FR-001 | What is the first user-facing interface: CLI, Markdown/git workflow, web UI, visual canvas, or combination? | FR-005, FR-013, FR-015 |
| OQ-FR-002 | What source systems and file types must be supported first? | FR-001, FR-003, FR-010, FR-023 |
| OQ-FR-003 | Which agent actions require approval versus audit-only logging? | FR-014, FR-022 |
| OQ-FR-004 | What quality gates are objective enough for deterministic validation in MVP1? | FR-007, FR-019 |
| OQ-FR-005 | What customer/domain should drive the first workflow templates? | FR-009, FR-021, FR-023 |
