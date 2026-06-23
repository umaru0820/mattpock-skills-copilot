# Context and ADR docs

How engineering skills should consume project context and decisions when exploring the codebase.

This file is intended for `.github/ai/agent-workflow.md`.

## Before exploring, read these

- `.github/context/shared-context.md` for shared vocabulary and repo-wide concepts.
- `.github/context/context-map.md` as a router to optional module-specific context docs.
- `.github/adr/` for architectural decisions that affect the area being changed.

If any of these files don't exist, proceed silently. Do not block execution on missing docs.

## Context model

- `shared-context.md` is the glossary and shared language.
- `context-map.md` is navigation only. It should point to module context docs where they exist.
- Module context docs are optional and should be created only when concept boundaries are distinct.

## File structure

Recommended layout:

```
.github/
    ai/
        agent-workflow.md
    context/
        shared-context.md
        context-map.md             (optional)
        design-system-context.md   (optional)
        app-shell-context.md       (optional)
        forms-context.md           (optional)
    adr/
        0000-context-document-structure.md
```

## Use glossary vocabulary

When output names a domain concept, use terms from shared context or relevant module context docs. Avoid untracked synonyms.

## Flag ADR conflicts

If output conflicts with an ADR, surface it explicitly instead of silently overriding.
