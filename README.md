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

## Releasing

- Run **Actions → Release → Run workflow** and choose `release_type`:
  - `major`: bump to `X+1.0.0`
  - `minor`: bump to `X.Y+1.0`
  - `patch`: bump to `X.Y.Z+1`
- The workflow reads the latest `v*` semver tag (or starts from `v1.0.0` if none exist), then creates and pushes the next immutable `v<next>` tag and a GitHub Release.
- Before tagging, it requires a matching changelog heading in `CHANGELOG.md`: `## v<next>` or `## <next>`.
- Install/re-install from an immutable tag/ref (for example `v1.2.3`) rather than a moving branch.