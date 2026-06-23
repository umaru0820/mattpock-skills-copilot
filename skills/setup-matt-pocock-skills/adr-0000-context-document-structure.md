# ADR-0001: Context document structure

## Status

Accepted

## Context

The repository needs a consistent, Copilot-oriented document layout that separates execution workflow, domain context, reusable overlays, and architectural rationale.

## Decision

Use this structure:

- `.github/copilot-instructions.md` as top-level entrypoint.
- `.github/ai/` for operational workflow docs.
- `.github/agents/` for optional reusable custom overlays.
- `.github/context/` for glossary and context routing docs.
- `.github/adr/` for architecture decision records.

Use `shared-context.md` plus `context-map.md` as the baseline context model.

## Consequences

- Agent behavior is easier to reason about because operations and meaning are separated.
- Reusable overlays remain optional and task-oriented.
- Context docs scale from simple repos to module-heavy repos without forcing one file per folder.
- ADRs become discoverable under one stable path.
