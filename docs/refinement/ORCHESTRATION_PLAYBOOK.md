# Synapse Orchestration Playbook

This playbook adapts the Schedul-R concept-to-implementation operating model to
Synapse while using the vendored `orchestration-framework/` CLI as the control
surface.

## Operating loop

For every iteration:

1. Assess current canonical docs, task cards, feedback, and validation reports.
2. Identify the next highest-priority phase/iteration.
3. Generate runtime scaffolding with:
   ```bash
   python3 orchestration-framework/cli.py execute "/orchestrator::start_workflow(<workflow>, <phase>, <iteration>)"
   ```
4. Launch role agents through generated task cards or:
   ```bash
   python3 orchestration-framework/cli.py execute "/orchestrator::launch_agents(<iteration>, dry-run)"
   ```
5. Validate deliverables and evaluate iteration output.
6. Record feedback and apply lessons to templates, personas, rules, or workflow
   config before starting the next comparable iteration.

## Workflow selection

- Use `synapse-artifact-factory` to produce strategy artifacts: requirements,
  market, GTM, business case, pitch, architecture, and refinement reviews.
- Use `synapse-concept-to-implementation` to follow the Schedul-R-style path:
  source extraction, canonical docs, backlog, progressive MVP documentation,
  QA/operations, audit, and implementation handoff.

## Iteration skeleton

Every iteration must have:

- `CONTEXT.md`
- `COMPLETION_CRITERIA.md`
- `README.md`
- task cards under `.orchestration/runtime/agent-sync/tasks/`
- deterministic validation/evaluation output
- feedback or lessons captured under `.orchestration/knowledge/`

## Delegation rule

The orchestrator creates plans, context, task cards, and framework improvements.
It does not directly author deliverables assigned to specialist roles.
