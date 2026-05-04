# Synapse MVP Strategy

- **Status**: corrective product reframing
- **Owning workflow**: `synapse-product-mvp-reframing`
- **Last updated**: 2026-05-03

## Purpose

This document re-anchors the MVP roadmap around **Synapse as the product**.
`cursor_orchestrator` and the vendored `orchestration-framework/` are enabling
tools used to generate, validate, and refine product artifacts in this repository.
They are not the product being specified.

## Product/tooling boundary

| Thing | Role in this repo | Product status |
| --- | --- | --- |
| Synapse | The product/platform being specified. | Product under design. |
| `cursor_orchestrator` | Reusable orchestration framework used to coordinate agents and artifact generation. | Tooling dependency, not the Synapse product. |
| `.orchestration/config/workflows/*` | Project-local orchestration workflows used to produce Synapse artifacts. | Process/configuration assets. |
| MVP1 platform docs already produced | Documentation of the CLI-assisted operating substrate used to bootstrap Synapse requirements. | Foundation/process MVP, not the full product MVP. |

## Corrected MVP framing

### MVP0: Canonical product foundation

**Goal**: Establish canonical requirements, architecture, decisions, artifact
workflow, backlog conventions, and source-grounding rules so future product work
is traceable.

**Primary outputs**

- Product and functional requirements.
- Product capability map.
- Architecture and decision log.
- Work-item and dependency structure.
- Source-grounding and orchestration standards.

**Status**: largely complete as a documentation foundation.

### MVP1: AI coworker workspace for one workflow

**Goal**: Define and later implement the first Synapse product slice: an
operator workspace where a human can define a destination, select a reusable
expert workflow, attach approved knowledge, dispatch agent coworkers, monitor
progress, review outputs, and capture learnings.

**Product capabilities**

- Workflow setup for one approved workflow.
- Role/persona selection.
- Knowledge-context attachment.
- Task dispatch and status visibility.
- Human review gates.
- Output and handoff review.
- Learning capture after completion.

**Important distinction**: The current CLI-assisted orchestration framework can
prototype this flow, but the product MVP is the Synapse operator experience and
runtime contract, not the framework internals.

### MVP2: Knowledge and SME persona layer

**Goal**: Turn canonical sources, approved extracts, and SME guidance into
reusable grounding contexts and persona templates that agent coworkers can
consume safely.

**Product capabilities**

- Source inventory and approval workflow.
- Knowledge asset model.
- Persona template composition.
- Confidence, freshness, and provenance controls.
- Learning promotion into reusable assets.

### MVP3: Workflow runtime, monitoring, and approvals

**Goal**: Define and implement the Synapse runtime concepts that make workflows
observable and governable beyond static CLI-assisted execution.

**Product capabilities**

- Workflow run state model.
- Live monitoring.
- Human approval queues.
- Validation and recovery status.
- Audit trail and operational telemetry.

### MVP4: Legacy bridge package

**Goal**: Apply Synapse to a validated legacy-to-greenfield transition scenario.

**Product capabilities**

- Source intake from a legacy context.
- Current-state knowledge extraction.
- Future-state requirement generation.
- Transition-risk and dependency mapping.
- Handoff to modernization teams.

## Immediate correction

Future iterations should use the completed orchestration-framework artifacts as
**process evidence** and **prototype scaffolding**, then translate them into
Synapse product requirements. New product docs should answer:

1. What does the human operator see and decide?
2. What does Synapse persist, validate, and govern?
3. What is a reusable workflow/persona/knowledge object in the product?
4. Which actions require human review?
5. Which artifacts are product outputs versus orchestration-process outputs?

## Open product decisions

| ID | Decision | Impact |
| --- | --- | --- |
| PMVP-OQ-001 | Is MVP1 a local desktop/CLI workspace, web workspace, or hybrid? | Determines UX, persistence, and deployment architecture. |
| PMVP-OQ-002 | Which first workflow should be productized for an external user? | Determines initial templates, personas, and knowledge requirements. |
| PMVP-OQ-003 | What is the minimum durable runtime state Synapse must own? | Determines data model and runtime boundaries. |
| PMVP-OQ-004 | Which review/approval actions are mandatory in product UX? | Determines governance and audit requirements. |
| PMVP-OQ-005 | What customer data/security constraints apply? | Determines tenancy, compliance, and source-ingestion boundaries. |
