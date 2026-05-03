# Input Packet: Concept Extraction and Canonical Truth Drafting

- **Workflow**: `synapse-concept-to-implementation`
- **Phase**: `phase-0` - Seed Extraction and Canonical Foundation
- **Iteration**: `concept-extraction`

This packet prevents duplicate task-card generation in the current framework,
where each `inputs` entry creates a separate task. Role agents should read
the packet first, then load the role-specific source references below.

## Iteration goal

Transform immutable raw inputs and project research into canonical
Markdown documents that future agents cite as the source of truth.
Preserve source uncertainty and initialize backlog/domain structure
without treating raw notes as final requirements.

## Role source references

### `requirements_strategist`

- `research/Synapse_Initial_Chat_Summary.md`
- `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md`
- `work_items/synapse-product-brief.md`

### `architect`

- `research/Synapse_Initial_Chat_Summary.md`
- `research/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md`
- `work_items/synapse-product-brief.md`
- `docs/requirements/PRODUCT_REQUIREMENTS.md` after the requirements strategist updates it

### `dependency_analyst`

- `docs/requirements/PRODUCT_REQUIREMENTS.md`
- `docs/architecture/ARCHITECTURE.md`
- `docs/planning/DELIVERY_BACKLOG.md`

## Completion criteria summary

- Canonical requirements, architecture, planning, and decision docs exist and cite source inputs.
- Raw seed or research files remain immutable; agents write only canonical docs outputs.
- Backlog identifies candidate MVPs, domains, and epics with explicit confidence and gaps.
- Concurrency analysis separates safe parallel work from sequential dependencies.
