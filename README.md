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
python3 orchestration-framework/cli.py execute "/orchestrator::start_workflow(synapse-artifact-factory, phase-1, discovery-foundation)"
```

The primary project workflow lives at
`.orchestration/config/workflows/synapse-artifact-factory.yaml`, with persona
definitions in `.orchestration/config/agent-personas.yaml`.

Runtime task cards, memos, and iteration outputs are generated under
`.orchestration/runtime/` and are intentionally gitignored.
