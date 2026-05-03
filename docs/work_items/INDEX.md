# Synapse Work Item Index

- **Status**: refined backlog foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `backlog-refinement`
- **Last updated**: 2026-05-03
- **Primary inputs**:
  - `docs/requirements/PRODUCT_REQUIREMENTS.md`
  - `docs/requirements/FUNCTIONAL_REQUIREMENTS.md`
  - `docs/planning/DELIVERY_BACKLOG.md`
  - `docs/planning/EXECUTION_ORCHESTRATION.md`

This index is the canonical entry point for executable Synapse work items. It
uses the `E##` epic convention and `US-E##-###` story convention. MVP1 is scoped
to the canonical concept-to-implementation pipeline: canonical documentation,
workflow/task-packet definition, deterministic validation, backlog readiness,
and orchestration handoff for one initiative.

## Readiness and confidence policy

| Label | Meaning |
| --- | --- |
| Draft | Backlog item exists but still has unresolved product, architecture, quality, or dependency gaps. |
| Refined | Product scope, traceability, dependencies, acceptance-quality criteria, and open questions are explicit enough for technical refinement. |
| Ready candidate | Item can be implemented after named architecture/quality gates are accepted. |
| Deferred | Supported or plausible future work that is outside MVP1. |

## MVP sequence and epic map

| Epic | Name | MVP | Readiness status | Requirement trace | Dependencies | Summary |
| --- | --- | --- | --- | --- | --- | --- |
| E01 | Canonical Documentation Foundation | MVP1 | Refined | PRD-001, PRD-002; FR-001, FR-002, FR-003, FR-004 | None | Establish canonical doc registry, source attribution, uncertainty labels, immutable-source handling, and open-question tracking. |
| E02 | Workflow Definition and Task-Packet Model | MVP1 | Ready candidate | PRD-003, PRD-005; FR-005, FR-006, FR-010 | E01; ADR-0011; ADR-0012; ADR-0013 | Define CLI-assisted workflow phases, roles, inputs, deliverables, completion criteria, and bounded agent task packets for the orchestration-framework domain. |
| E03 | Deterministic Validation and Completion Signals | MVP1 | Draft | PRD-003, PRD-005; FR-007, FR-008, FR-019 | E01, E02; ADR-0014 | Specify objective validation hooks and standardized completion, partial-completion, blocked, and recovery signals. |
| E04 | Backlog Generation and Readiness Gates | MVP1 | Draft | PRD-008; FR-018, FR-019, FR-020 | E01; partial E02 | Generate traceable epics/stories with readiness gates, dependency notes, risks, and acceptance-quality criteria. |
| E05 | Orchestration Execution Handoff | MVP1 | Draft | PRD-005, PRD-008; FR-005, FR-006, FR-008, FR-020 | E02, E03, E04 | Package accepted MVP1 contracts into an implementation handoff that states launch order, owners, recovery paths, and remaining blockers. |
| E06 | Source Inventory and Grounding Model | MVP2 | Deferred | PRD-001, PRD-002, PRD-009; FR-003, FR-010, FR-021, FR-022 | E01, E02 | Prioritize source types and grounding mechanics for repeatable role-agent work. |
| E07 | SME Persona and Role Template Library | MVP2 | Deferred | PRD-004, PRD-009; FR-009, FR-021 | E02, E06 | Define reusable persona templates and composition rules for role agents. |
| E08 | Domain Configuration Model | MVP2 | Deferred | PRD-009; FR-021, FR-022 | E02, E07 | Separate domain-specific roles, artifacts, and quality thresholds from the core workflow model. |
| E09 | Workflow Status and Monitoring Surface | MVP3 | Deferred | PRD-006; FR-013, FR-015 | E02, E03 | Expose workflow, iteration, agent, deliverable, and validation status to human operators. |
| E10 | Human Approval Checkpoints | MVP3 | Deferred | PRD-006; FR-014, FR-022 | E09 | Define approval classes, pause/resume behavior, and decision recording for high-impact actions. |
| E11 | Feedback Capture and Improvement Promotion | MVP3 | Deferred | PRD-007; FR-016, FR-017 | E03, E07, E09 | Link iteration outcomes and recurring failures to template, role, workflow, or process improvements. |
| E12 | Legacy-to-Greenfield Requirement Extraction | MVP4 | Deferred | PRD-010; FR-023 | E01, E06, E08 | Apply Synapse to a validated modernization corpus to extract current-state assumptions and future-state gaps. |
| E13 | Transition-State Planning Artifacts | MVP4 | Deferred | PRD-010; FR-018, FR-019, FR-023 | E12 | Produce migration planning artifacts only after a concrete legacy-transition use case is validated. |

## MVP1 story map

| Story | Title | Epic | Readiness status | Requirement trace | Dependencies |
| --- | --- | --- | --- | --- | --- |
| US-E01-001 | Define the canonical documentation registry | E01 | Refined | PRD-001; FR-001 | None |
| US-E01-002 | Standardize source attribution and uncertainty labels | E01 | Refined | PRD-002; FR-002, FR-004 | US-E01-001 |
| US-E01-003 | Protect raw and research inputs during canonical drafting | E01 | Refined | PRD-001, PRD-002; FR-003 | US-E01-001 |
| US-E01-004 | Maintain the open-question and validation-need register | E01 | Refined | PRD-002; FR-004 | US-E01-002 |
| US-E01-005 | Define canonical artifact acceptance-quality criteria | E01 | Refined | PRD-001, PRD-008; FR-001, FR-019 | US-E01-001, US-E01-002 |
| US-E02-001 | Define workflow phase and iteration metadata | E02 | Draft | PRD-003, PRD-005; FR-005 | E01 |
| US-E02-002 | Define role-agent task packet structure | E02 | Draft | PRD-003, PRD-005; FR-006, FR-010 | US-E02-001 |
| US-E02-003 | Define dependency and write-target coordination rules | E02 | Draft | PRD-003, PRD-005; FR-006, FR-020 | US-E02-001 |
| US-E03-001 | Specify deterministic validation checks for MVP1 artifacts | E03 | Draft | PRD-005; FR-007, FR-019 | E01, E02 |
| US-E03-002 | Specify completion, partial-completion, and blocked signals | E03 | Draft | PRD-003, PRD-005; FR-008 | E02 |
| US-E03-003 | Define recovery handling for validation and token-budget failures | E03 | Draft | PRD-005; FR-007, FR-008 | US-E03-001, US-E03-002 |
| US-E04-001 | Generate traceable epic and story candidates from canonical requirements | E04 | Draft | PRD-008; FR-018 | E01 |
| US-E04-002 | Apply product, technical, quality, dependency, risk, and implementation readiness gates | E04 | Draft | PRD-008; FR-019 | E01, partial E02 |
| US-E04-003 | Document dependency and concurrency notes for backlog items | E04 | Draft | PRD-008; FR-020 | E01, partial E02 |
| US-E05-001 | Package MVP1 implementation handoff and launch sequence | E05 | Draft | PRD-005, PRD-008; FR-005, FR-020 | E02, E03, E04 |
| US-E05-002 | Record MVP1 assumptions, exclusions, and unresolved blockers | E05 | Draft | PRD-002, PRD-008; FR-004, FR-019 | E02, E03, E04 |

## Story readiness gates

A story is ready for implementation only when all gates below are recorded in
its epic deliverables or story detail:

| Gate | Acceptance-quality criteria |
| --- | --- |
| Product | Persona, user value, scope boundaries, MVP fit, assumptions, open questions, and excluded future scope are explicit. |
| Requirements traceability | PRD and FR IDs are linked; unsupported specifics are marked as assumptions, open questions, or validation needs. |
| Architecture/technical | Technical boundary, data/integration implications, write targets, and sequencing constraints are reviewed or identified as non-blocking. |
| Quality | Acceptance criteria, validation approach, deterministic checks where feasible, and failure/recovery expectations are documented. |
| Dependencies | Upstream docs, decisions, stories, and unsafe parallelism are listed. |
| Risk | Security/privacy, source-provenance, reliability, token-budget, and scope-creep risks are assessed where relevant. |
| Implementation | The story is small enough to execute, has clear done criteria, and names deliverables that can be inspected. |

## MVP1 assumptions and open questions

| ID | Type | Item | Impact |
| --- | --- | --- | --- |
| D-WI-001 | Decision | MVP1 delivery mode is CLI-assisted orchestration using `orchestration-framework/cli.py`, generated task cards, runtime memos, and canonical docs. | Unblocks E02 and sizes E05 around CLI-assisted handoff rather than runtime-backed product behavior. |
| D-WI-002 | Decision | The orchestration framework is the first internal domain/initiative for MVP1 workflow templates. | Gives E02/E04 a concrete, source-backed domain without inventing an external customer. |
| D-WI-003 | Decision | MVP1 metadata is Markdown-first: structured headings and tables with PRD/FR IDs, E##/US-E##-### IDs, confidence, readiness, dependency, owner/reviewer, and validation fields. | Unblocks task-packet and backlog metadata refinement while deferring machine-readable schemas. |
| D-WI-004 | Decision | Initial validators target required files, required sections, trace markers, ID format, prohibited source mutations, and completion-signal format. | Unblocks E03 validator specification. |
| OQ-WI-004 | Open question | What source types must be supported first for grounding after MVP1? | Blocks E06 and later MVP2 planning. |
