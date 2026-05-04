# Applying Learnings Playbook

Every orchestration iteration must end by collecting feedback and applying at
least one explicit learning decision.

## Required loop

1. Run the iteration through framework commands.
2. Evaluate outputs and runtime evidence.
3. Capture feedback in `.orchestration/knowledge/evaluations/` or a linked
   review artifact.
4. Identify patterns, not isolated mistakes.
5. Update the workflow, persona, template, context, or validation threshold that
   prevents repeat failure.
6. Record the change in `docs/refinement/LESSONS_LEARNED.md`.
7. Commit the process improvement with the artifact changes.

## Pattern to action matrix

| Pattern | Signal | Required action |
| --- | --- | --- |
| Token budget pressure | Partial deliverables, `TOKEN_BUDGET_LOW`, or many near-empty files | Split the next iteration, lower role scope, or add a recovery pass. |
| Scope confusion | Future-MVP work appears in current artifacts | Strengthen `CONTEXT.md` scope boundaries and workflow completion criteria. |
| Tool avoidance | Prompts, reports, or validation are hand-written | Update runbook/rules with literal framework commands. |
| Quality drift | Artifacts have inconsistent sections | Add or improve templates and concrete examples. |
| Silent completion | No memo or completion signal | Update persona completion protocol and task-card instructions. |

If the same mistake appears twice, promote the fix to a reusable template or
persona change.
