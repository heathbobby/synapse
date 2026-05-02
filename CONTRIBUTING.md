# Contributing to Synapse

This project uses the **Generic Orchestration Framework** for multi-agent coordination.

## Orchestration Workflow

When working on tasks that benefit from AI agent coordination, use the orchestration framework.

Synapse's primary artifact workflow is:

```bash
python orchestration-framework/cli.py execute "/orchestrator::start_workflow(synapse-artifact-factory, phase-0, source-brief-normalization)"
```

Run phases after their upstream artifacts exist:

- `phase-0, source-brief-normalization`
- `phase-1, discovery-foundation`
- `phase-2, market-positioning`
- `phase-3, commercial-strategy`
- `phase-4, technical-architecture`
- `phase-5, pitch-and-executive-synthesis`
- `phase-6, refinement-review-loop`

Project-specific role contracts live in `.orchestration/config/agent-personas.yaml`.
The operational runbook is `docs/orchestration/artifact-factory-runbook.md`.

### Quick Start

1. **Start a workflow**:
   ```bash
   /orchestrator::start_workflow(<workflow-name>, <phase>, <iteration>)
   ```

2. **Agents execute tasks**:
   ```bash
   /<role>::start_task(<work-item-id>)
   # or
   /<role>::start_next
   ```

3. **Integrate ready work**:
   ```bash
   /integrator::apply_ready
   ```

4. **Validate iteration**:
   ```bash
   /integrator::validate_iteration(<iteration-name>)
   ```

## Worktree-Based Development

When multiple agents work concurrently, each agent uses its own git worktree to prevent conflicts.

### Create a Worktree

```bash
git switch main
git worktree add -b <type>/<scope>/<short-desc> \
  ../Synapse.worktrees/<agent>/<type>-<short-desc> \
  main
```

### Work in Your Worktree

```bash
cd ../Synapse.worktrees/<agent>/<branch>
# Make changes, commit, etc.
```

### Announce Ready-to-Consume

Post a memo to `.orchestration/runtime/agent-sync/`:

```markdown
- **Date**: 2026-05-02
- **Audience**: `@integrator`
- **Status**: `ready-to-consume`
- **Branch**: `<branch>`
- **SHA**: `<sha>`
- **Work Item**: <work-item-id>
- **Deliverables**:
  - <path1> (created/updated)
  - <path2> (created/updated)
```

See `.orchestration/runtime/agent-sync/COMMAND_SHORTHAND.md` for complete command reference.

## Integration

The integrator role manages convergence of ready-to-consume work:

```bash
/integrator::apply_ready
```

This will:
- Scan `.orchestration/runtime/agent-sync/` for ready-to-consume memos
- Cherry-pick or merge agent work
- Run merge gate checks (validation, tests, coverage)
- Update memos to ready-to-merge

## Configuration

Framework configuration is in: `.orchestration/config/framework.yaml`

Customize:
- Project name and trunk branch
- Worktree location
- Agent roles
- Merge gate settings
- Token budget limits

## Getting Help

- Review command shorthand: `.orchestration/runtime/agent-sync/COMMAND_SHORTHAND.md`
- Review completed iterations in `.orchestration/runtime/iterations/`
