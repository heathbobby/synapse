# Input Packet: MVP2 Source Inventory and Grounding Model

- **Workflow**: `synapse-concept-to-implementation`
- **Phase**: `phase-8` - MVP2 Iteration 1 - Source Inventory and Grounding
- **Iteration**: `mvp2-iteration-01-source-grounding`

This packet follows the one-input-per-agent convention used by the current
framework task-card generator. Role agents should read this packet first, then
load the role-specific source references below.

## Iteration goal

Define the first MVP2 knowledge-grounding foundation that can consume MVP1
canonical artifacts, classify source types, preserve provenance and freshness,
and prepare persona/template work without selecting a runtime knowledge store.

## Role source references

### `data_architect`

- `docs/requirements/PRODUCT_REQUIREMENTS.md`
- `docs/requirements/FUNCTIONAL_REQUIREMENTS.md`
- `docs/architecture/ARCHITECTURE.md`
- `docs/architecture/TECHNICAL_SPECIFICATIONS.md`
- `docs/architecture/DECISIONS.md`
- `docs/MVP1/Platform/Overview.md`
- `docs/MVP1/Platform/Infrastructure.md`
- `docs/MVP1/Platform/DataModel.md`
- `docs/MVP1/Platform/Integrations.md`
- `docs/MVP1/Platform/TestingStrategy.md`
- `docs/MVP1/Platform/AcceptanceCriteria.md`
- `docs/MVP1/Platform/OperationalRunbook.md`
- `docs/MVP1/Platform/ReleaseNotes.md`
- `docs/implementation/IMPLEMENTATION_ROADMAP.md`
- `docs/work_items/INDEX.md`
- `docs/work_items/DEPENDENCY_MAP.md`

### `standards_curator`

- `docs/standards/AI_AGENT_STANDARDS.md`
- `docs/standards/ENGINEERING_STANDARDS.md`
- `docs/standards/EVENT_CONTRACT_STANDARDS.md`
- `docs/refinement/APPLYING_LEARNINGS_PLAYBOOK.md`
- `docs/refinement/ORCHESTRATION_PLAYBOOK.md`
- `docs/refinement/SCALABLE_ORCHESTRATION_PHILOSOPHY.md`
- `docs/MVP1/Platform/TestingStrategy.md`
- `docs/MVP1/Platform/AcceptanceCriteria.md`
- `docs/MVP1/Platform/OperationalRunbook.md`

## Scope boundaries

MVP2 source grounding is about contracts and standards, not implementation of a
knowledge store. Keep these future/open unless later decisions accept them:

- embeddings, vector databases, search indexes, or retrieval algorithms;
- source-system connectors, sync jobs, or crawlers;
- tenancy, access-control, retention, deletion, or compliance enforcement;
- provider-specific agent runtimes or prompt-management services;
- automatic promotion of runtime logs or memos without human/integrator review.

## Completion criteria summary

- Source inventory prioritizes MVP1 canonical docs, orchestration config, work
  items, standards, decisions, memos/log references, and future raw/external
  sources.
- Grounding model defines provenance, confidence, freshness, review, promotion,
  and consumption contracts without choosing storage or retrieval technology.
- Knowledge grounding standards describe how sources become approved knowledge
  and how repeated learnings update templates, personas, workflows, or backlog
  gates.
- Future runtime knowledge store, retrieval, embeddings, tenancy, compliance,
  and source-system connectors are marked open or future scope.
