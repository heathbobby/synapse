# Concurrency Analysis

## Purpose

Define which Synapse orchestration tasks can run in parallel and which must remain sequential.

## Initial Policy

- Strategy artifacts may fan out by artifact family when each agent writes disjoint files.
- Concept-to-implementation iterations follow the Schedul-R sequence:
  infrastructure -> entities/models -> integrations -> features -> quality -> operations.
- The orchestrator may prepare the next iteration while the current one runs, but must not launch it until required upstream artifacts validate.

## Safe Parallelism

- Market research and competitive analysis can run in parallel after requirements exist.
- API architecture and integration architecture can run in parallel after data/entity models exist.
- QA strategy and acceptance criteria can run in parallel after feature specs exist.

## Unsafe Parallelism

- Feature specifications before integrations.
- Operations before quality/acceptance criteria.
- Any refinement that requires sponsor answers not yet captured in `docs/artifacts/OPEN_QUESTIONS.md`.
