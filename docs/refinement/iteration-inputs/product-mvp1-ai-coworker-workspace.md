# Input Packet: Synapse Product MVP1 Workspace Definition

- **Workflow**: `synapse-product-development`
- **Phase**: `product-mvp1`
- **Iteration**: `product-mvp1-workspace-definition`

## Iteration goal

Define Synapse product MVP1 as an AI coworker workspace for one approved expert
workflow. This iteration translates the completed internal orchestration
foundation into product-facing requirements, UX/workflow concepts, and acceptance
criteria without treating `cursor_orchestrator` as the product.

## Product/tooling boundary

- Synapse is the product.
- `cursor_orchestrator`, `orchestration-framework/`, Cursor rules, current YAML
  workflows, generated task cards, and runtime memos are scaffolding and evidence.
- Product artifacts may borrow concepts from the scaffolding, but they must
  describe the product surface, persisted state, human decisions, governance,
  and user value in tool-agnostic terms.

## Role source references

### `product_owner`

- `docs/product/MVP_STRATEGY.md`
- `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
- `docs/product/PRODUCT_CAPABILITY_MAP.md`
- `research/Synapse_Initial_Chat_Summary.md`
- `docs/MVP1/Platform/ReleaseNotes.md`
- `docs/implementation/IMPLEMENTATION_ROADMAP.md`

### `ux_designer`

- `docs/product/MVP_STRATEGY.md`
- `docs/product/PRODUCT_CAPABILITY_MAP.md`
- `docs/MVP1/Platform/Features/WorkflowDesigner/Overview.md`
- `docs/MVP1/Platform/Features/WorkflowDesigner/Workflows/CreateWorkflow.md`
- `docs/MVP2/Knowledge/GroundingModel.md`
- `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`

### `qa_lead`

- `docs/product/MVP_STRATEGY.md`
- `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
- `docs/product/ProductMVP1/WORKSPACE_REQUIREMENTS.md`
- `docs/product/ProductMVP1/WORKSPACE_EXPERIENCE.md`
- `docs/MVP1/Platform/AcceptanceCriteria.md`
- `docs/MVP1/Platform/TestingStrategy.md`

## Completion criteria summary

- Product MVP1 requirements describe the AI coworker workspace, not the
  orchestration framework internals.
- Workspace experience describes what the human operator sees, decides, reviews,
  and hands off.
- Acceptance criteria are testable or reviewable and trace to product
  requirements/capability IDs.
- Tooling concepts are clearly marked as prototype/scaffolding when referenced.
