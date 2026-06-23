# Repository Agent Entry Point

Read in this order:

1. `.github/ai/agent-workflow.md`
2. `.github/ai/issue-tracker.md`
3. `.github/ai/triage-labels.md`
4. `.github/context/context-map.md`
5. `.github/context/shared-context.md`
6. Relevant files in `.github/adr/`

## How to use these docs

- Use `.github/ai/` for execution process and operations.
- Use `.github/context/` for project language and conceptual boundaries.
- Use `.github/adr/` for architectural intent and tradeoffs.
- Use `.github/agents/` only when a specific overlay is selected.

## Overlay behavior

If a custom overlay is selected from `.github/agents/`, apply it as an additive layer on top of this file and do not replace base workflow rules.
