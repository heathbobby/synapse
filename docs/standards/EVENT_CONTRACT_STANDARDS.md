# Event Contract Standards

## Purpose

Define event and integration conventions before implementation begins.

## Placeholder Standards

- Prefer explicit event ownership, schema versioning, and idempotent consumers.
- Document event producers, consumers, payload shape, retry behavior, and dead-letter handling.
- Treat event names and schemas as stable contracts once implementation starts.

## Open Decisions

- Event bus/runtime selection.
- Schema registry requirements.
- Observability and replay strategy.
