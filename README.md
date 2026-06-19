# Matt Pocock Skills (Copilot-Adapted)

This repository is an adapted version of Matt Pocock's skills, focused on a GitHub Copilot workflow.

## What this repo provides

- Reusable engineering and productivity skills.
- A setup flow (`/setup-matt-pocock-skills`) that scaffolds a `.github/`-centric AI workflow for existing projects.
- A clear separation of:
	- operational guidance in `.github/ai/`
	- context and vocabulary in `.github/context/`
	- architecture decisions in `.github/adr/`
	- optional custom overlays in `.github/agents/`

## Design principles

- Explore before writing.
- Shared language and explicit issue workflow.
- Triage role consistency.
- ADRs for durable, non-obvious decisions.
- Compatibility-first migration from older conventions where needed.

## Current direction

The repository is being refined to remove Claude-first naming and align skills to explicit `.github/` paths, with `.github/context/shared-context.md` as the primary context glossary.