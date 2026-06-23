# AI Workflow Structure

This folder holds repository-level AI workflow artifacts.

## Folder roles

- `copilot-instructions.md` is the primary entrypoint for agents in this repository.
- `ai/` contains operational workflow instructions (how the agent should work).
- `agents/` contains optional reusable overlays for specific stacks, versions, or tasks.
- `context/` contains shared vocabulary and optional module context docs (what the codebase means).
- `adr/` contains architecture decision records and rationale.

## Where to add new docs

- Add process and execution rules to `ai/`.
- Add glossary and domain vocabulary to `context/`.
- Add non-obvious durable design decisions to `adr/`.
- Add task-specific overlays to `agents/` only when they are reusable.

## Agent overlay naming

Files in `agents/` must use:

- lowercase
- kebab-case
- `.agent.md` suffix

Example: `angular-v9.agent.md`
