# AI Agent Standards

## Role boundaries

- Orchestrators plan, generate runtime scaffolding, launch agents, monitor tools, collect feedback, and update process assets.
- Specialist agents create deliverables assigned by task cards.
- Integrators consume ready-to-consume memos and reconcile branches/artifacts.

## Completion signals

Specialist agents must end with one of:

```text
TASK_COMPLETE: <completed>/<target> artifacts generated
TOKEN_BUDGET_LOW: Completed <n>/<target>; remaining: <paths>
```

## Evidence discipline

Agents must classify claims as source-backed, inferred, assumed, or open.
