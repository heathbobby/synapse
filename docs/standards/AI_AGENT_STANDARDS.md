# AI Agent Standards

- **Status**: draft canonical foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Last updated**: 2026-05-03
- **Purpose**: Define implementation-agnostic standards for agent roles,
  evidence discipline, output quality, completion signals, and handoffs.

## Scope and Source of Truth

These standards apply to orchestrators, specialist agents, integrators,
reviewers, and any future agent runtime adapter used by Synapse workflows.

- Canonical `docs/` artifacts are the implementation contract.
- Raw and research sources are inputs only; agents must not edit `raw/` or
  `research/` files unless a future canonical rule grants explicit authority.
- Claims must preserve uncertainty instead of converting assumptions or open
  questions into committed product, architecture, stack, compliance, or runtime
  decisions.
- Agent instructions should stay technology-neutral unless a canonical
  architecture decision already selects a concrete stack, provider, protocol, or
  deployment model.

## Role Boundaries

- **Orchestrators** plan workflows, generate runtime scaffolding, launch agents,
  monitor tools, collect feedback, recover from partial completions, and update
  process assets.
- **Specialist agents** create or update deliverables assigned by task cards
  within the named scope, sources, file paths, and completion criteria.
- **Integrators** consume ready-to-consume memos, reconcile branches or
  artifacts, resolve cross-file consistency issues, and decide whether outputs
  are ready to merge.
- **Reviewers** evaluate product, architecture, quality, security/privacy,
  dependency, or evidence gates; they do not imply implementation approval unless
  the task card names that authority.

Agents must not expand role scope silently. If required work is outside the
assigned role or deliverables, the agent should record the gap as an open
question, blocker, or follow-up task.

## Required Task Packet Inputs

Before execution, an agent task should include:

| Input | Requirement |
| --- | --- |
| Role and objective | Named role, intended outcome, and bounded scope. |
| Canonical sources | Required `docs/` sources and any approved non-doc context. |
| Deliverables | Exact artifact paths or implementation outputs. |
| Prohibited edits | Files, directories, or decisions the agent must not change. |
| Dependencies | Upstream docs, decisions, stories, approvals, or agent outputs. |
| Acceptance criteria | Testable or reviewable success criteria. |
| Validation expectations | Deterministic checks, review checks, tests, or explicit limits. |
| Handoff audience | Downstream role, integrator, reviewer, or orchestrator. |

If critical inputs are missing, the agent should proceed only when the work can
be safely framed as discovery or refinement; otherwise it should report a
blocker.

## Evidence Discipline

Agents must classify material claims as:

| Evidence class | Meaning |
| --- | --- |
| `source-backed` | Directly supported by cited canonical sources or approved context. |
| `inferred` | Reasonably derived from sources but not directly stated. |
| `assumed` | Needed to proceed but not yet validated. |
| `open` | Unknown or requiring product, architecture, security, or stakeholder decision. |

Evidence expectations:

- Cite canonical file paths or IDs for source-backed claims when practical.
- Mark inferred and assumed claims in the output or handoff summary when they
  affect scope, architecture, data contracts, validation, security/privacy,
  dependencies, or operations.
- Convert missing information into open questions instead of inventing product
  behavior, event transports, storage models, tenancy, compliance posture,
  provider choices, or UI/runtime technology.
- Reusable learnings should name the target for promotion after review:
  canonical docs, workflow templates, persona definitions, standards,
  validators, or backlog items.

## Output Quality Criteria

Agent outputs are reviewable only when they include:

- Changed artifacts or generated deliverables, with paths.
- Source and evidence summary, including assumptions and open questions.
- Scope boundaries and any intentionally deferred work.
- Validation performed and validation not performed.
- Risks, blockers, dependency impacts, and recommended recovery or follow-up.
- Handoff notes for the named reviewer, integrator, or downstream agent.
- Confirmation that prohibited files and directories were not edited.

For backlog and implementation-preparation work, outputs must also align with
`docs/work_items/TECHNICAL_REFINEMENT_GATES.md`, including architecture,
data/integration, validation, observability, security/privacy, dependency, and
agent-output gate expectations.

## Completion Signals

Specialist agents must end with one of these standard signals:

```text
TASK_COMPLETE: <completed>/<target> artifacts generated
TOKEN_BUDGET_LOW: Completed <n>/<target>; remaining: <paths>
BLOCKED: <blocking decision/source/dependency>; impact: <affected deliverables>
PARTIAL_COMPLETE: Completed <n>/<target>; remaining: <paths>; recovery: <recommended split>
```

Signal usage:

- Use `TASK_COMPLETE` only when all assigned deliverables are complete and the
  required validation or review checks have been performed or explicitly
  recorded as not performed.
- Use `TOKEN_BUDGET_LOW` when remaining work is primarily capacity-related and
  can continue from the listed paths or sections.
- Use `BLOCKED` when a missing decision, source, approval, dependency, access
  boundary, or open architecture question prevents safe completion.
- Use `PARTIAL_COMPLETE` when some deliverables are useful but the task requires
  a follow-up recovery split before downstream work can rely on the full output.

## Validation and Handoff

Agents should run or describe the most relevant validation available for the
work type:

- Deterministic checks where feasible, such as required files, required
  sections, metadata presence, traceability, schema or contract consistency, and
  completion-signal format.
- Review checks when deterministic validation is not feasible, with the required
  reviewer role named.
- Runtime or test execution only when the task and repository context support
  it; do not invent test infrastructure or stack commitments.

Handoffs should make downstream safety clear:

- State whether output is ready for implementation, ready for review,
  ready-to-consume by another role, blocked, or partial.
- Name downstream dependencies that can proceed and those that must wait.
- For multi-agent work, identify shared-file risks, merge contracts, or
  required integrator reconciliation.
- If feedback reveals a recurring process issue, recommend whether to update
  standards, templates, validators, task packets, or backlog gates.

## Safety and Governance

- Agents must respect explicit persona permissions, allowed tools, adapter
  access, and prohibited edits.
- Sensitive data, tenancy, retention, compliance, and access-control topics must
  be classified as known, assumed, open, or not applicable; unresolved items
  should block implementation claims.
- Human approval requirements must be preserved for policy-sensitive, high-risk,
  release, SME-validation, or compliance-sensitive steps.
- Persona, workflow template, knowledge asset, and standard changes that affect
  future agent behavior require attribution and review before promotion.
