# Synapse Product Requirements

- **Status**: product-reframed canonical draft
- **Purpose**: Define Synapse as the product/platform being built, separate from
  the orchestration tooling used to produce these artifacts.
- **Last updated**: 2026-05-03

## Product definition

Synapse is a domain-agnostic operational substrate for agentic workforces. It
helps organizations codify expert workflows, ground AI coworkers in approved
knowledge, coordinate human/agent execution, and feed operational learning back
into reusable templates, personas, and knowledge assets.

`cursor_orchestrator` and the vendored `orchestration-framework/` are build-time
and repo-operations tooling. They are not the Synapse product surface.

## Source-backed product pillars

| Pillar | Product meaning |
| --- | --- |
| Backfill the truth | Turn tribal knowledge, raw documents, incidents, tickets, conversations, and system observations into governed knowledge assets. |
| Scale expertise | Encode principal-level workflows into reusable personas, templates, gates, and guided execution paths. |
| Coordinate AI coworkers | Assign work to agents and humans with clear context, boundaries, approvals, state, and handoff contracts. |
| Bridge legacy and future systems | Extract requirements and stabilize transition states while supporting greenfield architecture decisions. |
| Self-augment | Promote every completed workflow, review, incident, or discovery into improved knowledge, personas, workflows, or validation gates. |
| Build trust culturally | Make human ownership, review, evidence, and learning visible so adoption feels augmentative rather than opaque or threatening. |

## Product requirements

| ID | Requirement | MVP focus |
| --- | --- | --- |
| SYN-PRD-001 | Synapse shall maintain governed knowledge assets with provenance, owner, confidence, freshness, applicability, and review status. | MVP1 |
| SYN-PRD-002 | Synapse shall support SME/persona templates that encode role perspective, allowed tools, evidence rules, quality gates, and escalation behavior. | MVP2 |
| SYN-PRD-003 | Synapse shall provide a workflow design surface for composing expert processes, agent/human steps, approvals, dependencies, and validation gates. | MVP2 |
| SYN-PRD-004 | Synapse shall execute or coordinate workflows through explicit state, task assignment, completion signals, recovery paths, and audit records. | MVP3 |
| SYN-PRD-005 | Synapse shall expose human-in-the-loop review and approval checkpoints for policy-sensitive, high-risk, or confidence-limited work. | MVP3 |
| SYN-PRD-006 | Synapse shall publish feedback and operational learning back into knowledge assets, personas, workflow templates, validators, and backlog gates. | MVP3 |
| SYN-PRD-007 | Synapse shall support integrations with external source systems and work systems through explicit source ownership, access, retention, and contract boundaries. | MVP4 |
| SYN-PRD-008 | Synapse shall support legacy-transition workflows that extract current-state truth, identify future-state gaps, and produce implementation-ready migration artifacts. | MVP4 |
| SYN-PRD-009 | Synapse shall keep humans accountable for destination, constraints, risk acceptance, and final promotion of reusable behavior. | Cross-cutting |
| SYN-PRD-010 | Synapse shall remain domain-agnostic while allowing domain-specific workflow packs, persona packs, source packs, and validation packs. | Cross-cutting |

## Non-goals for the product

- Synapse is not merely a prompt library.
- Synapse is not merely this repository's documentation generator.
- Synapse is not the same thing as `cursor_orchestrator`.
- Synapse does not require the final product to expose Cursor-specific concepts.
- Synapse does not begin with a fully automated no-human approval model.

## Tooling boundary

| Concern | Product or tooling? | Notes |
| --- | --- | --- |
| `.orchestration/config/workflows/*.yaml` in this repo | Tooling artifact | Used to generate/refine Synapse specs. May inspire product workflow schema but is not itself the product contract. |
| Runtime task cards and memos | Tooling artifact | Useful evidence for learning, but product runtime should define its own durable task/audit model later. |
| CLI-assisted orchestration | Tooling / prototyping mode | Useful for building specs and proving workflows. Product UX/runtime may later differ. |
| Governed knowledge assets | Product capability | Core Synapse functionality. |
| SME/persona template registry | Product capability | Core Synapse functionality. |
| Visual workflow designer | Product capability | Future product UX, not MVP1 repo tooling. |
| Hybrid event bus | Product architecture capability | Future implementation after contracts and constraints mature. |
| Legacy bridge adapters | Product/domain pack capability | Future after validated customer/source corpus. |

## Open product questions

| ID | Question | Impact |
| --- | --- | --- |
| SYN-OQ-001 | Who is the first paying or internal target user? | Determines ICP, workflow packs, UX, integrations, and compliance posture. |
| SYN-OQ-002 | Is Synapse initially SaaS, internal platform, open-core, or services-enabled product? | Determines deployment, packaging, support, and GTM. |
| SYN-OQ-003 | Which source systems should be supported first beyond repository docs? | Determines MVP1/MVP4 connector and governance scope. |
| SYN-OQ-004 | What autonomy levels are acceptable for different action classes? | Determines approval model, permissions, audit, and safety. |
| SYN-OQ-005 | Which compliance and data-governance regimes matter first? | Determines tenancy, retention, access, and deployment architecture. |
