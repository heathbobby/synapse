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
