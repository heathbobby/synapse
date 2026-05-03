# Architecture Decision Log

## Status

`canonical draft`

## Purpose

Track architecture decisions that affect Synapse's canonical implementation path.
This log distinguishes accepted source-backed direction from assumptions and
open decisions that still need stakeholder, product, or engineering input.

## Decision Records

| ID | Status | Decision | Rationale | Source | Date |
| --- | --- | --- | --- | --- | --- |
| ADR-0001 | accepted | Treat Synapse as a domain-agnostic operational substrate for agentic workforces. | The research frames Synapse as moving beyond "AI as a tool" toward "AI as a Coworker" and calls it an implementation-agnostic operational substrate. This constrains the architecture to configurable workflows, personas, events, and knowledge assets rather than a single vertical workflow product. | `research/Synapse_Initial_Chat_Summary.md`; `work_items/synapse-product-brief.md` | 2026-05-03 |
| ADR-0002 | accepted | Keep raw and research inputs immutable; promote implementation truth into canonical docs. | The concept-extraction packet and playbook require raw/research inputs to remain source material, while canonical docs become the contract for later agents and implementation work. | `docs/refinement/iteration-inputs/concept-extraction.md`; `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md` | 2026-05-03 |
| ADR-0003 | accepted | Use a visual workflow designer as the primary human authoring and monitoring surface. | Source research explicitly names a drag-and-drop visual workflow designer with nested workflows and live monitors. This becomes a first-class experience-layer capability. | `research/Synapse_Initial_Chat_Summary.md` | 2026-05-03 |
| ADR-0004 | accepted | Use a hybrid event bus pattern for workflow, telemetry, approval, and integration coordination. | Source research calls for centralized Pub/Sub supporting asynchronous telemetry and synchronous human-in-the-loop approvals. Existing event standards require explicit ownership, schema versioning, idempotency, retries, and dead-letter handling. | `research/Synapse_Initial_Chat_Summary.md`; `docs/standards/EVENT_CONTRACT_STANDARDS.md` | 2026-05-03 |
| ADR-0005 | accepted | Model agent personas with inheritance-like OOP composition. | Source research describes Object-Oriented Prompting as Base Template -> Extended Template -> Instance. The architecture therefore includes a persona registry with lineage, versioning, role boundaries, and quality gates. | `research/Synapse_Initial_Chat_Summary.md`; `docs/standards/AI_AGENT_STANDARDS.md` | 2026-05-03 |
| ADR-0006 | accepted | Make the knowledge loop a core platform capability, not a reporting afterthought. | Both the Synapse research and concept-to-implementation playbook state that feedback must update knowledge bases, SME templates, personas, workflow templates, or future execution. | `research/Synapse_Initial_Chat_Summary.md`; `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md` | 2026-05-03 |
| ADR-0007 | accepted | Treat human-in-the-loop approvals as first-class workflow state transitions. | The hybrid event bus requirement includes synchronous approvals, and the architecture thesis keeps humans accountable for risk, policy, scope, and release decisions. | `research/Synapse_Initial_Chat_Summary.md`; `docs/architecture/ARCHITECTURE.md` | 2026-05-03 |
| ADR-0008 | accepted | Include a legacy bridge as a bounded integration capability. | Source research identifies the legacy transition state as a primary use case: stabilizing legacy systems while extracting requirements for greenfield architecture. Keeping it bounded protects the domain-agnostic core. | `research/Synapse_Initial_Chat_Summary.md` | 2026-05-03 |
| ADR-0009 | accepted | Ground agent work in SME and tribal-knowledge assets with evidence classification. | Source research emphasizes codifying tribal knowledge and creating SME agents from up-to-date documentation. Existing agent standards require claims to be classified as source-backed, inferred, assumed, or open. | `research/Synapse_Initial_Chat_Summary.md`; `docs/standards/AI_AGENT_STANDARDS.md` | 2026-05-03 |
| ADR-0010 | accepted | Avoid concrete stack commitments until requirements, constraints, and MVP scope are known. | The product brief says product specifics are hypotheses unless supported and asks for explicit open questions instead of invented certainty. Existing engineering standards require unknown stack choices to be marked as decisions needed. | `work_items/synapse-product-brief.md`; `docs/standards/ENGINEERING_STANDARDS.md` | 2026-05-03 |

## Open Architecture Decisions

| ID | Decision Needed | Why It Matters | Current Guidance | Source |
| --- | --- | --- | --- | --- |
| OAD-0001 | MVP scope and first target workflows | Component depth, adapter priorities, and approval policies depend on the first operational workflows. | Keep architecture domain-agnostic until product requirements identify target users and workflows. | `work_items/synapse-product-brief.md` |
| OAD-0002 | Tenancy and deployment model | Multi-tenant SaaS, single-tenant, and deploy-per-customer models change isolation, audit, data retention, and integration boundaries. | Do not assume tenancy; document data boundaries in future requirements. | `docs/architecture/ARCHITECTURE.md` |
| OAD-0003 | Workflow runtime and persistence mechanism | Determines state durability, replay, recovery, and integration model. | Specify durable state transitions and reconstructable audit trail before choosing implementation technology. | `docs/architecture/TECHNICAL_SPECIFICATIONS.md` |
| OAD-0004 | Event transport, schema format, and registry strategy | The hybrid event bus requires versioned contracts, idempotency, retry, and dead-letter handling. | Follow event contract standards; select transport only after throughput, latency, and operating constraints are known. | `docs/standards/EVENT_CONTRACT_STANDARDS.md` |
| OAD-0005 | Knowledge asset storage and retrieval model | SME grounding requires freshness, confidence, source traceability, and retrieval by workflow/persona/domain. | Treat raw notes as inputs and canonical docs/approved extracts as runtime truth. | `research/Synapse_Initial_Chat_Summary.md`; `docs/standards/AI_AGENT_STANDARDS.md` |
| OAD-0006 | Human approval policy model | Defines when autonomous execution is acceptable and when human review blocks execution. | Start with explicit workflow gates and record approver, evidence, rationale, timestamp, and resulting state. | `docs/architecture/TECHNICAL_SPECIFICATIONS.md` |
| OAD-0007 | Visual workflow template representation | Versioning, diffing, testing, nested workflow reuse, and promotion depend on the template format. | Require versioned templates and source links; defer concrete graph serialization. | `research/Synapse_Initial_Chat_Summary.md` |
| OAD-0008 | Legacy bridge MVP adapter set | Adapter scope affects security, permissions, rate limits, and operational risk. | Keep legacy adapters isolated from core workflow/persona models until initial systems are selected. | `research/Synapse_Initial_Chat_Summary.md` |
| OAD-0009 | Agent runtime integration strategy | Persona execution, tool permissions, telemetry, and artifact collection depend on runtime interfaces. | Use pluggable adapters and preserve role boundaries/completion signals. | `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md`; `docs/standards/AI_AGENT_STANDARDS.md` |
| OAD-0010 | Compliance and data governance constraints | Sensitive data handling, retention, audit requirements, and access controls shape every layer. | Mark compliance as unknown until stakeholder input is available. | `work_items/synapse-product-brief.md` |

## Assumptions to Validate

- Synapse will initially reuse the orchestration-framework operating concepts
  for workflows, task cards, role agents, memos, validation, and feedback loops.
- The first implementation should prioritize architecture contracts and
  workflow/persona/knowledge abstractions before choosing specific vendors.
- Human reviewers and SMEs are available for approval and knowledge validation
  in workflows where policy, release, or high-risk decisions are involved.
- Legacy bridge scenarios are strategically important, but the first legacy
  system and adapter boundaries remain unspecified.
