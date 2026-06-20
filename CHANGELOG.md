## v1.0.0

Initial Copilot-adapted baseline for this repository fork.

### Highlights

- Repositioned the repository around a GitHub Copilot-oriented workflow.
- Reworked `/setup-matt-pocock-skills` to scaffold a `.github/`-centric structure for existing projects.
- Added seed templates for:
  - `.github/README.md`
  - `.github/copilot-instructions.md`
  - `.github/ai/agent-workflow.md`
  - `.github/ai/issue-tracker.md`
  - `.github/ai/triage-labels.md`
  - `.github/context/context-map.md`
  - `.github/context/shared-context.md`
  - `.github/adr/0001-context-document-structure.md`
- Updated core engineering skills to prefer explicit `.github` paths for context and ADR consumption.
- Standardized terminology to explicitly reference `.github/context/shared-context.md` instead of ambiguous labels.

### Breaking Changes

- Removed Claude-first and legacy distribution artifacts from this fork:
  - `CLAUDE.md`
  - `.claude-plugin/`
  - `.changeset/`
  - `docs/`
  - `.out-of-scope/`
  - `package.json`
- Removed non-target skill buckets from this fork:
  - `skills/deprecated/`
  - `skills/personal/`

### Notes

- This changelog is reset for this adapted repository line and does not track upstream `mattpocock/skills` release history.

## v1.0.1
- Versioning with **Github Actions** via **semsev** convention.
- Released version (Eg. v.1.2.3) is saved to **Github Tags**.