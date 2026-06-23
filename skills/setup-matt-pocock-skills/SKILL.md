---
name: setup-matt-pocock-skills
description: Configure this repo for engineering skills in a .github-first workflow: issue tracker rules, triage vocabulary, context map, and ADR layout. Run once before first use of the other engineering skills.
disable-model-invocation: true
---

# Setup Matt Pocock's Skills

Scaffold the per-repo configuration that engineering skills assume in a Copilot-oriented layout:

- **Issue tracker** — where issues live (GitHub by default; local markdown is also supported out of the box)
- **Triage labels** — the strings used for the five canonical triage roles
- **Context docs** — shared vocabulary and optional module context docs
- **ADRs** — durable architectural decisions and rationale

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists; don't assume:

- `git remote -v` and `.git/config` — is this a GitHub repo? Which one?
- `.github/copilot-instructions.md`
- `.github/README.md`
- `.github/ai/`
- `.github/agents/`
- `.github/context/`
- `.github/adr/`
- Existing AI instruction or prompt files anywhere in the repo
- Existing issue workflow docs and label docs
- Existing context docs and ADR docs in any legacy location
- `.tasks/` — sign that a local-markdown issue tracker convention is already in use

Summarize findings first:

- What already exists in `.github/`
- What existing content should be reused or merged
- What legacy files should be referenced during migration
- What new files are missing

### 2. Present findings and ask

Summarise what's present and what's missing. Then walk the user through the three decisions **one at a time** — present a section, get the user's answer, then move to the next. Don't dump all three at once.

Assume the user does not know what these terms mean. Each section starts with a short explainer (what it is, why these skills need it, what changes if they pick differently). Then show the choices and the default.

**Section A — Issue tracker.**

> Explainer: The "issue tracker" is where issues live for this repo. Skills like `to-issues`, `triage`, `to-prd`, and `qa` read from and write to it — they need to know whether to call `gh issue create`, write a markdown file under `.tasks/`, or follow some other workflow you describe. Pick the place you actually track work for this repo.

Default posture: these skills were designed for GitHub. If a `git remote` points at GitHub, propose that. If a `git remote` points at GitLab (`gitlab.com` or a self-hosted host), propose GitLab. Otherwise (or if the user prefers), offer:

- **GitHub** — issues live in the repo's GitHub Issues (uses the `gh` CLI)
- **GitLab** — issues live in the repo's GitLab Issues (uses the [`glab`](https://gitlab.com/gitlab-org/cli) CLI)
- **Local markdown** — issues live as files under `.tasks/<feature>/` in this repo (good for solo projects or repos without a remote)
- **Other** (Jira, Linear, etc.) — ask the user to describe the workflow in one paragraph; the skill will record it as freeform prose

If — and only if — the user picked **GitHub** or **GitLab**, ask one follow-up:

> Explainer: Open-source repos often receive feature requests as pull requests, not just issues — a PR is an issue with attached code. If you turn this on, `/triage` pulls *external* PRs into the same queue and runs them through the same labels and states as issues (collaborators' in-flight PRs are left alone). Leave it off if PRs aren't a request surface for you.

- **PRs as a request surface** — yes / no (default: no). Record the answer in `.github/ai/issue-tracker.md`. For local-markdown and other trackers, skip this question — there are no PRs.

**Section B — Triage label vocabulary.**

> Explainer: When the `triage` skill processes an incoming issue, it moves it through a state machine — needs evaluation, waiting on reporter, ready for an AFK agent to pick up, ready for a human, or won't fix. To do that, it needs to apply labels (or the equivalent in your issue tracker) that match strings *you've actually configured*. If your repo already uses different label names (e.g. `bug:triage` instead of `needs-triage`), map them here so the skill applies the right ones instead of creating duplicates.

The five canonical roles:

- `needs-triage` — maintainer needs to evaluate
- `needs-info` — waiting on reporter
- `ready-for-agent` — fully specified, AFK-ready (an agent can pick it up with no human context)
- `ready-for-human` — needs human implementation
- `wontfix` — will not be actioned

Default: each role's string equals its name. Ask the user if they want to override any. If their issue tracker has no existing labels, the defaults are fine.

**Section C — Domain docs.**

> Explainer: Some skills read context docs to learn the project's domain language, and ADR docs for past architectural decisions. The context model here is: one shared glossary file plus a context map that routes to optional module files.

Confirm the layout:

- **Shared context required** — `.github/context/shared-context.md`
- **Context map required** — `.github/context/context-map.md` (navigation only, not glossary)
- **Module context docs optional** — create only when useful or explicitly requested

### 3. Confirm and edit

Show the user a draft of:

- `.github/README.md`
- `.github/copilot-instructions.md`
- `.github/ai/agent-workflow.md`
- `.github/ai/issue-tracker.md`
- `.github/ai/triage-labels.md`
- `.github/context/context-map.md`
- `.github/context/shared-context.md`
- `.github/adr/0000-context-document-structure.md`

Let them edit before writing.

### 4. Write

Create or update this structure:

```text
.github/
	README.md
	copilot-instructions.md
	ai/
		agent-workflow.md
		issue-tracker.md
		triage-labels.md
	agents/
	context/
		context-map.md
		shared-context.md
	adr/
		0000-context-document-structure.md
```

Rules:

- Never overwrite meaningful user-authored content blindly.
- If a target file exists, merge/update carefully where practical.
- If replacement would discard meaningful content, ask before replacing.
- `.github/agents/` may remain empty.
- Do not generate `.github/agents/*.agent.md` files by default.
- If creating agent overlays later, names must be lowercase kebab-case with `.agent.md` suffix.

Use seed templates in this skill folder as the starting point:

- [github-readme.md](./github-readme.md) — `.github/README.md`
- [copilot-instructions.md](./copilot-instructions.md) — `.github/copilot-instructions.md`
- [domain.md](./domain.md) — `.github/ai/agent-workflow.md`
- [issue-tracker-github.md](./issue-tracker-github.md) — GitHub issue tracker
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md) — GitLab issue tracker
- [issue-tracker-local.md](./issue-tracker-local.md) — local-markdown issue tracker
- [triage-labels.md](./triage-labels.md) — `.github/ai/triage-labels.md`
- [context-map.md](./context-map.md) — `.github/context/context-map.md`
- [shared-context.md](./shared-context.md) — `.github/context/shared-context.md`
- [adr-0000-context-document-structure.md](./adr-0000-context-document-structure.md) — `.github/adr/0000-context-document-structure.md`

For "other" issue trackers, write `.github/ai/issue-tracker.md` from scratch using the user's description.

### 5. Done

Tell the user the setup is complete and which engineering skills now read from this structure. Mention they can edit `.github/ai/*.md`, `.github/context/*.md`, and `.github/adr/*.md` directly later — re-running this skill is only necessary if they want to switch issue trackers or restart from scratch.
