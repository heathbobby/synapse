# Input Packet: Synapse Product MVP2 Knowledge and Persona Layer

- **Workflow**: `synapse-product-development`
- **Phase**: `phase-2` - MVP2 Knowledge and SME Persona Layer
- **Iteration**: `mvp2-knowledge-persona-layer`

## Iteration goal

Define Synapse product MVP2 as the layer that turns approved sources, SME
guidance, and workflow learnings into governed knowledge assets and reusable
persona templates that AI coworkers can safely consume.

## Product/tooling boundary

- Synapse is the product.
- MVP2 product artifacts should describe user-visible product behavior,
  product-owned runtime contracts, governance, review, and reusable product
  assets.
- Existing source-grounding docs under `docs/MVP2/Knowledge/` and
  `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md` are product input evidence,
  not the final product UX or runtime by themselves.
- Do not expose `cursor_orchestrator`, Cursor rules, YAML workflow files, or
  runtime memos as the customer-facing product model.

## Role source references

### `product_owner`

- `docs/product/MVP_STRATEGY.md`
- `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
- `docs/product/PRODUCT_CAPABILITY_MAP.md`
- `docs/product/MVP1/AI_COWORKER_WORKSPACE.md`
- `docs/product/MVP1/OPERATOR_JOURNEY.md`
- `docs/MVP2/Knowledge/SourceInventory.md`
- `docs/MVP2/Knowledge/GroundingModel.md`
- `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`

### `technical_architect`

- `docs/product/MVP_STRATEGY.md`
- `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
- `docs/product/MVP1/RUNTIME_CONTRACTS.md`
- `docs/MVP2/Knowledge/SourceInventory.md`
- `docs/MVP2/Knowledge/GroundingModel.md`
- `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`
- `docs/architecture/ARCHITECTURE.md`
- `docs/architecture/TECHNICAL_SPECIFICATIONS.md`
- `docs/architecture/DECISIONS.md`

### `standards_curator`

- `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
- `docs/product/PRODUCT_CAPABILITY_MAP.md`
- `docs/MVP2/Knowledge/GroundingModel.md`
- `docs/standards/AI_AGENT_STANDARDS.md`
- `docs/standards/KNOWLEDGE_GROUNDING_STANDARDS.md`
- `.orchestration/config/agent-personas.yaml`

### `qa_lead`

- `docs/product/MVP_STRATEGY.md`
- `docs/product/SYNAPSE_PRODUCT_REQUIREMENTS.md`
- `docs/product/PRODUCT_CAPABILITY_MAP.md`
- `docs/product/MVP1/ACCEPTANCE_CRITERIA.md`
- `docs/product/MVP2/KNOWLEDGE_AND_PERSONA_LAYER.md`
- `docs/product/MVP2/KNOWLEDGE_WORKFLOW.md`
- `docs/product/MVP2/KNOWLEDGE_PERSONA_CONTRACTS.md`
- `docs/product/MVP2/PERSONA_TEMPLATE_SYSTEM.md`

## Completion criteria summary

- Product MVP2 requirements describe governed knowledge assets and reusable
  SME/persona templates as product capabilities.
- Knowledge workflow covers source intake, review, approval, grounding context
  creation, persona consumption, and learning promotion.
- Persona template system defines reusable SME/persona behavior with governance,
  evidence, confidence, and escalation controls.
- Runtime contracts avoid committing to storage, retrieval, embeddings,
  provider, tenancy, deployment, or compliance implementation.
- Acceptance criteria are testable or reviewable and trace to Synapse product
  requirements/capability IDs.
