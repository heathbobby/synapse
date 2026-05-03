# Input Packet: Epic and User Story Refinement

- **Workflow**: `synapse-concept-to-implementation`
- **Phase**: `phase-1` - Backlog Refinement
- **Iteration**: `backlog-refinement`

This packet prevents duplicate task-card generation in the current framework,
where each `inputs` entry creates a separate task. Role agents should read
the packet first, then load the role-specific source references below.

## Iteration goal

Create a backlog that engineers and agent teams can execute. Each
story should trace to canonical requirements, name dependencies, and
meet a ready-for-implementation quality gate.

## Role source references

### `product_owner`

- `docs/requirements/PRODUCT_REQUIREMENTS.md`
- `docs/requirements/FUNCTIONAL_REQUIREMENTS.md`
- `docs/planning/DELIVERY_BACKLOG.md`

### `tech_lead`

- `docs/architecture/TECHNICAL_SPECIFICATIONS.md`
- `docs/planning/EXECUTION_ORCHESTRATION.md`
- `docs/work_items/INDEX.md`

### `dependency_analyst`

- `docs/work_items/INDEX.md`
- `docs/planning/CONCURRENCY_ANALYSIS.md`

## Completion criteria summary

- Work item structure uses E## and US-E##-### naming conventions.
- Each backlog artifact traces to canonical requirements and architecture documents.
- Readiness gates define product, technical, architecture, and quality approval criteria.
- Dependencies and concurrency constraints are explicit before MVP technical documentation begins.
