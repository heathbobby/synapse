# Synapse Artifact Factory Runbook

This runbook explains how to operate Synapse's artifact-generation workflow with
the vendored `orchestration-framework/` from `heathbobby/cursor_orchestrator`.

## Runtime and committed files

Commit these:

- `.orchestration/config/framework.yaml`
- `.orchestration/config/agent-personas.yaml`
- `.orchestration/config/workflows/synapse-artifact-factory.yaml`
- `.cursor/agent.md`
- `.cursor/rules/*.mdc`
- `work_items/*.md`
- `docs/artifacts/README.md`
- `docs/artifacts/templates/*.md`

Do not commit these:

- `.orchestration/runtime/agent-sync/`
- `.orchestration/runtime/iterations/`
- local worktrees such as `../Synapse.worktrees`

## Command reference

The implemented CLI entry point is:

```bash
python3 orchestration-framework/cli.py <subcommand>
```

Useful commands:

```bash
# List command handlers.
python3 orchestration-framework/cli.py list

# Validate slash-command syntax and registered handler availability.
python3 orchestration-framework/cli.py validate "/orchestrator::start_workflow(synapse-artifact-factory, phase-0, source-brief-normalization)"

# Generate one iteration's runtime context, task cards, and dispatch memo.
python3 orchestration-framework/cli.py execute "/orchestrator::start_workflow(synapse-artifact-factory, phase-0, source-brief-normalization)"

# Dry-run Cursor CLI launch from generated task cards.
python3 orchestration-framework/cli.py execute "/orchestrator::launch_agents(source-brief-normalization, dry-run)"

# Evaluate a completed iteration without writing evaluation files.
python3 orchestration-framework/cli.py execute "/integrator::evaluate_iteration(source-brief-normalization, dry-run)"
```

`start_workflow` writes runtime files under `.orchestration/runtime/`, which is
gitignored. Synapse disables automatic worktree creation in `framework.yaml` so
sample generation is safe in a normal checkout. Enable `worktrees.enabled` when
you want the orchestrator to create one branch/worktree per role.

## Phase sequence

Run phases in order unless you intentionally branch a refinement experiment:

1. `phase-0`, `source-brief-normalization`
   - Initializes `ARTIFACT_INDEX.md`, `DECISION_LOG.md`, `OPEN_QUESTIONS.md`,
     and `SOURCE_BRIEF_CRITIQUE.md`.
2. `phase-1`, `discovery-foundation`
   - Produces requirements, personas, JTBD, assumptions, customer discovery,
     validation experiments, voice-of-customer, and discovery critique.
3. `phase-2`, `market-positioning`
   - Produces market analysis, TAM/SAM/SOM, timing, competitive analysis,
     positioning map, differentiation strategy, and market critique.
4. `phase-3`, `commercial-strategy`
   - Produces GTM, ICP, pricing/packaging, launch plan, business case, revenue
     model, unit economics, milestones/investment, risk register, and commercial
     critique.
5. `phase-4`, `technical-architecture`
   - Produces architecture, system context, data/integration model, roadmap,
     MVP plan, security/privacy model, threat model, compliance considerations,
     and architecture critique.
6. `phase-5`, `pitch-and-executive-synthesis`
   - Produces pitch deck outline, investor narrative, investor Q&A, executive
     summary, artifact gap log, and updated artifact index.
7. `phase-6`, `refinement-review-loop`
   - Turns critiques and gap logs into a revision backlog, refinement plan,
     executive revision notes, updated decision/open-question logs, and final
     readiness review.

## Agent handoff convention

Agents should post memos in `.orchestration/runtime/agent-sync/` when an
artifact is useful for downstream work. Use this header shape:

```markdown
# Ready-to-Consume: <artifact or task>

- **Date**: YYYY-MM-DD
- **Audience**: `@integrator @<downstream-role>`
- **Status**: `ready-to-consume`
- **Branch**: `<branch-name>`
- **SHA**: `<commit-sha>`
- **Work Item**: `<work item or generated task id>`
- **Deliverables**:
  - `docs/artifacts/...` (created/updated)
```

The memo scanner expects the `Date`, `Audience`, `Status`, `Branch`, `SHA`,
`Work Item`, and `Deliverables` labels when available.

## Artifact quality bar

Every generated artifact should:

- Follow `docs/artifacts/templates/ARTIFACT_TEMPLATE.md` when no more specific
  template exists.
- Identify owner role, status, phase, source inputs, evidence confidence,
  assumptions, decisions, risks, and open questions.
- Link upstream and downstream artifacts.
- Avoid unsourced certainty. Use explicit hypotheses when evidence is missing.
- Be suitable for a later refinement loop without relying on runtime-only notes.

Review artifacts should follow `docs/artifacts/templates/REVIEW_TEMPLATE.md`.
