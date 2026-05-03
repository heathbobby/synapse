# Delivery Backlog

- **Status**: draft canonical foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `concept-extraction`
- **Last updated**: 2026-05-03
- **Primary inputs**:
  - `docs/requirements/PRODUCT_REQUIREMENTS.md`
  - `docs/requirements/FUNCTIONAL_REQUIREMENTS.md`
  - `research/Synapse_Initial_Chat_Summary.md`
  - `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md`
  - `work_items/synapse-product-brief.md`

This document is the canonical backlog summary for implementation planning.
Detailed epics and stories should live under `docs/work_items/` once backlog
generation expands beyond this concept-extraction foundation.

## 1. Backlog Status and Confidence Policy

The current sources support backlog structure and candidate work areas, but they
do not yet support committed market, stack, pricing, compliance, or UX details.
Treat every MVP, domain, epic, and story below as a refinement candidate until
the open questions in the PRD are resolved.

| Label | Meaning |
| --- | --- |
| Source-backed | Directly supported by the source inputs or canonical requirements. |
| Assumption | Reasonable sequencing or decomposition needed for planning; requires validation. |
| Open question | Missing decision prevents implementation-ready scope. |
| Validation need | Research, sponsor decision, technical spike, or prototype needed before commitment. |

## 2. Backlog Principles

- Every implementation story traces to canonical PRD and FR IDs.
- Every story records acceptance criteria, dependencies, risks, readiness gates,
  and source confidence before implementation.
- Raw and research files remain immutable inputs; implementation work references
  canonical docs.
- Backlog refinement is complete only when Product, Architecture, and Quality
  views agree.
- Unsupported specifics remain open questions rather than implicit scope.

## 3. Candidate MVP Sequence

| MVP | Candidate goal | Confidence | Primary requirements | Notes |
| --- | --- | --- | --- | --- |
| MVP1 | Canonical concept-to-implementation pipeline for one initiative. | Medium | PRD-001, PRD-002, PRD-003, PRD-005, PRD-008; FR-001 to FR-008, FR-018 to FR-020 | Best-supported initial slice because current repo and playbook center on canonical docs, role-agent orchestration, validation, and backlog readiness. |
| MVP2 | Configurable knowledge-grounding and SME/persona template layer. | Medium | PRD-004, PRD-009; FR-009, FR-010, FR-021, FR-022 | Supported conceptually; source types, retrieval mechanics, and inheritance model are open. |
| MVP3 | Workflow monitoring, approvals, and feedback-loop hardening. | Medium-low | PRD-006, PRD-007; FR-013 to FR-017 | Supported by concept summary and playbook, but UI/runtime choices remain unknown. |
| MVP4 | Legacy-bridge / transition-state workflow package. | Low | PRD-010; FR-023 | Source-backed use-case hypothesis; requires a validated customer/domain and source corpus. |

## 4. Candidate Product Domains

| Domain | Description | Confidence | Source / rationale |
| --- | --- | --- | --- |
| Canonical Knowledge | Requirements, architecture, planning, standards, work items, provenance, uncertainty, and source traceability. | High | Canonical truth model and concept-extraction goal. |
| Orchestration Runtime | Workflow definitions, phases, roles, task packets, completion signals, validation, and recovery. | High | Playbook process model and existing workflow references. |
| Agent Persona and Template System | Role definitions, SME templates, inheritance/composition, prompt generation, and reusable expertise packaging. | Medium | OOP prompting, SME agent concept, role library model. |
| Human Collaboration and Governance | Monitoring, approvals, review checkpoints, visible workflow state, and intervention points. | Medium-low | Visual workflow designer, hybrid event bus, live monitors; details open. |
| Feedback and Continuous Improvement | Feedback capture, pattern detection, template/process promotion, and learning loop. | Medium | Knowledge loop and playbook feedback loop. |
| Legacy Transition Workflows | Requirement extraction and migration planning from current-state systems into future-state architecture. | Low | Legacy bridge pillar; concrete domain absent. |

## 5. Candidate Epics

### MVP1: Canonical Concept-to-Implementation Pipeline

| Epic ID | Epic | Status | Requirement trace | Dependencies | Key gaps |
| --- | --- | --- | --- | --- | --- |
| E01 | Canonical Documentation Foundation | Source-backed | PRD-001, PRD-002; FR-001 to FR-004 | None | Confirm long-term doc roots and metadata format. |
| E02 | Workflow Definition and Iteration Model | Source-backed | PRD-003, PRD-005; FR-005, FR-006 | E01 | Confirm workflow authoring surface and configuration schema. |
| E03 | Deterministic Validation and Completion Signals | Source-backed | PRD-003, PRD-005; FR-007, FR-008 | E01, E02 | Define Synapse-specific validators beyond file existence/size. |
| E04 | Backlog Generation and Readiness Gates | Source-backed | PRD-008; FR-018, FR-019, FR-020 | E01 | Confirm initial MVP/domain/epic taxonomy. |
| E05 | Orchestration Execution Handoff | Assumption | PRD-005; FR-005, FR-006, FR-020 | E02, E03, E04 | Decide whether MVP1 is docs-only, CLI-assisted, or includes runtime automation. |

### MVP2: Knowledge Grounding and SME Templates

| Epic ID | Epic | Status | Requirement trace | Dependencies | Key gaps |
| --- | --- | --- | --- | --- | --- |
| E06 | Source Inventory and Grounding Model | Source-backed | PRD-001, PRD-002; FR-003, FR-010 | E01 | Select initial source types and retrieval/update approach. |
| E07 | SME Persona / Role Template Library | Source-backed at concept level | PRD-004; FR-009 | E02 | Decide template inheritance/composition mechanism. |
| E08 | Domain Configuration Model | Source-backed | PRD-009; FR-021, FR-022 | E02, E07 | Define configurable boundaries and stable runtime abstractions. |

### MVP3: Human Governance and Continuous Improvement

| Epic ID | Epic | Status | Requirement trace | Dependencies | Key gaps |
| --- | --- | --- | --- | --- | --- |
| E09 | Workflow Status and Monitoring Surface | Source-backed at concept level | PRD-006; FR-013, FR-015 | E02, E03 | Decide CLI/status-file vs web UI vs visual canvas for MVP3. |
| E10 | Human Approval Checkpoints | Source-backed at concept level | PRD-006; FR-014 | E09 | Define approval classes and audit requirements. |
| E11 | Feedback Capture and Improvement Promotion | Source-backed | PRD-007; FR-016, FR-017 | E03, E07 | Define feedback schema, ownership, and promotion workflow. |

### MVP4: Legacy Bridge Workflow Package

| Epic ID | Epic | Status | Requirement trace | Dependencies | Key gaps |
| --- | --- | --- | --- | --- | --- |
| E12 | Legacy-to-Greenfield Requirement Extraction | Source-backed use-case hypothesis | PRD-010; FR-023 | E01, E06, E08 | Validate customer/domain, source corpus, and current-state/future-state templates. |
| E13 | Transition-State Planning Artifacts | Assumption | PRD-010; FR-018, FR-019, FR-023 | E12 | Define migration planning outputs and acceptance criteria. |

## 6. Candidate Story Seeds

These are not final user stories. They are traceable seeds for future expansion
under `docs/work_items/`.

| Story seed ID | Candidate story | Epic | Trace | Confidence | Readiness |
| --- | --- | --- | --- | --- | --- |
| US-E01-001 | As a human operator, I need initialized canonical requirement, architecture, planning, standards, and work-item docs so agents share one implementation truth. | E01 | FR-001 | High | Needs metadata/schema decision. |
| US-E01-002 | As a product stakeholder, I need each requirement to show source/evidence, assumptions, open questions, and validation needs. | E01 | FR-002 | High | Ready for refinement. |
| US-E01-003 | As a repository maintainer, I need raw/research sources protected from edits during canonical drafting. | E01 | FR-003 | High | Ready for refinement. |
| US-E02-001 | As a workflow owner, I need workflow definitions to list phases, dependencies, roles, inputs, deliverables, and completion criteria. | E02 | FR-005 | High | Needs schema decision. |
| US-E02-002 | As a specialized agent, I need a bounded task packet with context, source refs, files, and quality criteria. | E02 | FR-006 | High | Needs task-packet template. |
| US-E03-001 | As an operator, I need deterministic validation to identify missing or incomplete deliverables. | E03 | FR-007 | High | Needs validator scope. |
| US-E03-002 | As an operator, I need standardized completion and partial-completion signals. | E03 | FR-008 | High | Needs signal format finalization. |
| US-E04-001 | As a product owner, I need candidate epics and stories generated from canonical requirements with traceability. | E04 | FR-018 | High | Needs `docs/work_items/` expansion. |
| US-E04-002 | As a delivery lead, I need readiness gates for product, technical, quality, dependencies, and risks. | E04 | FR-019 | High | Needs gate definitions. |
| US-E04-003 | As a delivery planner, I need dependency and concurrency notes on backlog items. | E04 | FR-020 | High | Needs dependency format. |
| US-E06-001 | As an agent, I need approved source material and canonical knowledge surfaced for grounding. | E06 | FR-010 | Medium | Needs source-type prioritization. |
| US-E07-001 | As an SME, I need reusable persona templates that encode role perspective, values, responsibilities, and output standards. | E07 | FR-009 | Medium | Needs inheritance/composition decision. |
| US-E09-001 | As an operator, I need a monitoring view that shows workflow, iteration, agent, deliverable, and signal status. | E09 | FR-013 | Medium-low | Needs interface decision. |
| US-E10-001 | As an operator, I need high-impact workflow steps to pause for human approval. | E10 | FR-014 | Medium-low | Needs autonomy policy. |
| US-E11-001 | As a workflow owner, I need iteration feedback captured and linked to template/process improvements. | E11 | FR-016, FR-017 | Medium | Needs feedback schema. |
| US-E12-001 | As a modernization team, I need requirements extracted from legacy source material into current-state assumptions and future-state gaps. | E12 | FR-023 | Low | Needs validated customer/domain. |

## 7. Readiness Gates

Use these gates before promoting any story seed to implementation-ready status:

| Gate | Required evidence |
| --- | --- |
| Product | Persona, user value, scope boundaries, source confidence, and acceptance criteria are explicit. |
| Requirements traceability | PRD and FR IDs are linked; assumptions and open questions are documented. |
| Architecture | Architecture owner confirms technical boundaries, data/integration needs, and constraints. |
| Quality | Test approach, validation method, and success/failure criteria are documented. |
| Dependencies | Upstream artifacts, decisions, and sequential constraints are listed. |
| Risk | Security/privacy, reliability, token-budget, and scope-creep risks are assessed where relevant. |
| Implementation | Work is small enough for a role/team to execute and has clear done criteria. |

## 8. Dependency and Sequencing Notes

### Sequential dependencies

1. E01 must precede every other epic because canonical paths, traceability, and
   uncertainty labels are foundational.
2. E02 should precede E03 because validation and completion signals need a known
   workflow/task-packet model.
3. E04 should use E01 outputs and early E02 structure, but can be refined in
   parallel with E03 once canonical requirement IDs are stable.
4. E06 to E08 should follow MVP1 foundation because knowledge grounding and
   persona templates need canonical source and workflow conventions.
5. E09 to E11 depend on workflow execution and validation concepts.
6. E12 and E13 should not start until a concrete legacy-transition domain and
   source corpus are validated.

### Safe parallelism candidates

- E02 task-packet template drafting and E04 readiness-gate drafting can proceed
  in parallel after E01 metadata conventions are accepted.
- E06 source inventory and E07 persona template modeling can proceed in parallel
  after MVP1 workflow conventions are stable.
- E09 monitoring requirements and E10 approval policy discovery can proceed in
  parallel after workflow statuses and agent actions are defined.

## 9. Open Questions Blocking Backlog Commitment

| OQ ID | Question | Blocks |
| --- | --- | --- |
| OQ-BL-001 | What is the first deployment/product mode: internal platform, SaaS, open-core framework, or services-enabled tool? | MVP boundaries, NFRs, architecture, GTM. |
| OQ-BL-002 | Which user/domain should drive MVP1 workflow templates? | E02, E04, E07, E08. |
| OQ-BL-003 | Is MVP1 expected to ship executable software, canonical documentation, or a CLI-assisted workflow foundation? | E05 and implementation sizing. |
| OQ-BL-004 | What source systems/file types must be supported first? | E06 and FR-010. |
| OQ-BL-005 | What approval model and autonomy limits are acceptable? | E09, E10, security architecture. |
| OQ-BL-006 | Which compliance/security constraints apply before customer data is handled? | Architecture, NFRs, release planning. |

## 10. Validation Backlog

| Validation item | Suggested method | Output |
| --- | --- | --- |
| Confirm MVP1 scope | Stakeholder walkthrough of PRD, FRs, and this backlog. | Approved MVP1 epic list and exclusions. |
| Select first domain | Compare candidate domains against available source material and sponsor priorities. | Domain list and artifact templates. |
| Define task-packet and metadata standards | Architect + requirements strategist working session. | Template accepted for role-agent iterations. |
| Prototype validation gates | Run one concept-to-implementation iteration and inspect validation misses. | Validator requirements and quality threshold changes. |
| Validate legacy-bridge use case | Customer or stakeholder interview around a real modernization initiative. | Decision to promote, defer, or drop MVP4. |
