# Synapse

Synapse is currently configured as a greenfield, artifact-driven project. The
repository includes a Cursor-compatible multi-agent orchestration setup for
generating and refining product, market, go-to-market, business case, pitch,
and technical architecture artifacts.

## Orchestration quick start

The reusable framework is vendored in `orchestration-framework/` from
`heathbobby/cursor_orchestrator`.

Install the Python dependency:

```bash
python3 -m pip install -r orchestration-framework/requirements.txt
```

List available framework commands:

```bash
python3 orchestration-framework/cli.py list
```

Start the first Synapse artifact iteration:

```bash
python3 orchestration-framework/cli.py execute "/orchestrator::start_workflow(synapse-artifact-factory, phase-0, source-brief-normalization)"
```

The primary project workflow lives at
`.orchestration/config/workflows/synapse-artifact-factory.yaml`, with persona
definitions in `.orchestration/config/agent-personas.yaml`.

The workflow follows a source-brief -> specialist generation -> critique ->
executive synthesis -> refinement loop:

1. `phase-0`, `source-brief-normalization`
2. `phase-1`, `discovery-foundation`
3. `phase-2`, `market-positioning`
4. `phase-3`, `commercial-strategy`
5. `phase-4`, `technical-architecture`
6. `phase-5`, `pitch-and-executive-synthesis`
7. `phase-6`, `refinement-review-loop`

Runtime task cards, memos, and iteration outputs are generated under
`.orchestration/runtime/` and are intentionally gitignored.

See `docs/orchestration/artifact-factory-runbook.md` for the full operating
model, artifact families, dry-run commands, and memo conventions.

## Schedul-R concept-to-implementation operating model

The repository also includes a Schedul-R-inspired workflow for moving from
source material to implementation-ready documentation:

```bash
python3 orchestration-framework/cli.py execute "/orchestrator::start_workflow(synapse-concept-to-implementation, phase-0, concept-extraction)"
```

That workflow lives at
`.orchestration/config/workflows/synapse-concept-to-implementation.yaml` and
uses the boot files under `docs/refinement/`:

- `MASTER_ORCHESTRATOR_INIT.md`
- `agent-roles/MASTER_ORCHESTRATOR.md`
- `ORCHESTRATION_PLAYBOOK.md`
- `SCALABLE_ORCHESTRATION_PHILOSOPHY.md`
- `APPLYING_LEARNINGS_PLAYBOOK.md`

Key invariants copied from the Schedul-R process:

- Raw seed material belongs in `raw/`, is protected by `.cursorignore`, and
  should not be edited by agents.
- Canonical truth lives under `docs/requirements`, `docs/architecture`,
  `docs/planning`, `docs/standards`, and `docs/work_items`.
- The orchestrator delegates deliverables to role agents; it does not author
  implementation artifacts directly.
- Iterations must close the feedback loop by updating templates, roles, or
  process docs when recurring failures are found.
