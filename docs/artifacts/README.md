# Synapse Artifact Factory

This directory is the committed home for durable Synapse strategy artifacts.
Generated coordination state stays under `.orchestration/runtime/` and must not
be committed.

## Canonical artifact families

| Family | Purpose |
| --- | --- |
| Root | `ARTIFACT_INDEX.md`, `DECISION_LOG.md`, `OPEN_QUESTIONS.md`, `EXECUTIVE_SUMMARY.md`, `ARTIFACT_GAP_LOG.md` |
| `requirements/` | Product requirements, personas, JTBD, assumptions, and risks |
| `customer/` | Customer discovery plan, validation experiments, voice-of-customer synthesis |
| `market/` | Market analysis, TAM/SAM/SOM, trends, competitive analysis, positioning, differentiation |
| `gtm/` | GTM strategy, ICP/segmentation, pricing/packaging, launch plan |
| `business/` | Business case, revenue model, unit economics, milestones, risk register |
| `architecture/` | Technical architecture, system context, data/integration, roadmap, security/privacy, threat model, compliance |
| `pitch/` | Pitch outline, investor narrative, investor Q&A |
| `reviews/` | Source brief, discovery, market, commercial, architecture, and final refinement critiques |
| `refinement/` | Revision backlog, refinement plan, executive revision notes |

## Workflow cadence

The artifact factory intentionally separates generation from critique:

1. `phase-0` normalizes the source brief and creates the artifact index,
   decision log, and open-question log.
2. `phase-1` through `phase-4` generate specialist artifacts and a
   `product_critic` review for each major artifact family.
3. `phase-5` creates pitch and executive synthesis artifacts.
4. `phase-6` turns critique and gap logs into a concrete revision backlog,
   refinement plan, updated ledgers, and final readiness review.

## Artifact status values

Use these values in artifact headers and the artifact index:

- `planned`: expected by the workflow but not started
- `draft`: generated but not reviewed
- `reviewed`: reviewed by `product_critic` or `executive_editor`
- `refined`: updated from critique/gap-log feedback
- `blocked`: waiting on sponsor input, source material, or dependency

## Template

Start each artifact from `templates/ARTIFACT_TEMPLATE.md` unless the workflow
task card specifies a more specialized format.
