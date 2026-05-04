# Scalable Orchestration Philosophy

Synapse preserves the central Schedul-R lesson: the orchestrator's job is to
make the system improve with every iteration, not to personally make every
iteration succeed.

## Principles

1. **Agents produce deliverables.** The orchestrator produces context, task
   cards, validation contracts, feedback, and integration decisions.
2. **Repeat the skeleton.** Every iteration uses generated `CONTEXT.md`,
   `COMPLETION_CRITERIA.md`, `README.md`, task cards, dispatch memos, and
   feedback/evaluation output.
3. **Use deterministic tools.** Command listing, workflow generation,
   launch dry-runs, evaluation, validation, and integration are CLI operations.
4. **Close feedback loops.** A critique or evaluation that does not change the
   next workflow, template, role, or completion criterion is not yet useful.
5. **Protect source material.** Raw sponsor inputs stay immutable in `raw/`.

## Tool avoidance warning signs

- Hand-writing artifact files in the orchestrator chat.
- Manually polling with sleep/list loops.
- Hand-writing agent prompts instead of generating task cards or launch prompts.
- Accepting repeated artifact issues without updating templates or criteria.

When any warning sign appears, stop the iteration and update the orchestration
system before continuing.
