---
name: hydrate-project-context
description: Build real project context from code after setup-matt-pocock-skills scaffold exists.
disable-model-invocation: true
---

# Hydrate Project Context

Use this after `/setup-matt-pocock-skills` has created the `.github/` skeleton.

This skill converts placeholder context into grounded context by combining:

- a relentless `/grill-me` interview loop,
- direct codebase evidence,
- careful updates to `.github/context/` docs.

Do not treat this as a template fill exercise. The output must reflect how this repo actually works.

## Preconditions

Verify these exist before continuing:

- `.github/copilot-instructions.md`
- `.github/ai/agent-workflow.md`
- `.github/ai/issue-tracker.md`
- `.github/ai/triage-labels.md`
- `.github/context/shared-context.md`
- `.github/context/context-map.md`
- `.github/adr/`

If they are missing, stop and ask the user to run `/setup-matt-pocock-skills` first.

## Process

### 1. Run a grilling loop first

Run a `/grill-me` style interview before writing context docs.

Rules:

- Ask one question at a time.
- For each question, include your recommended answer.
- If a question can be answered by reading the codebase, read the codebase instead of asking.
- Keep grilling until ambiguity is removed, not until you are tired.

Minimum topics to resolve:

- Primary users/actors
- Core workflows and business outcomes
- Important nouns and their boundaries
- Invariants and constraints
- External systems and integration boundaries
- Operational constraints (deployment, environments, compliance, tenancy, etc.)
- Non-goals and explicit out-of-scope behaviors

Completion criterion:

You can state a concise domain summary that the user confirms as correct, with no unresolved high-impact ambiguity.

### 2. Build a code-derived evidence map

Read the repository deeply and build an internal evidence map before editing docs.

At minimum inspect:

- Entry points and runtime boundaries
- Domain models and state transitions
- API handlers and contracts
- Persistence schema and migration history
- Queue/event/message boundaries (if any)
- Authorization/authentication paths
- Test suites that encode domain behavior
- Existing docs and ADRs that constrain behavior

When statements from the interview conflict with code, surface the conflict and resolve it explicitly.

Completion criterion:

Every important domain claim you plan to document is backed by direct codebase evidence or explicit user confirmation.

### 3. Draft bounded contexts, then update docs

Before creating any module context file, do one full-scan pass across the entire codebase and propose bounded-context candidates first.

#### 3a. Draft bounded-context candidates (no file creation yet)

Start by assuming everything belongs in `.github/context/shared-context.md`.

After the full scan, produce a draft list of candidate module contexts and show it to the user before writing module files.

For each candidate, include:

- Candidate file path (example: `.github/context/module-1-context.md`)
- Why this boundary is distinct
- Terms that appear bounded to this module and should not live in shared context
- Evidence sources in code/docs
- Proposed decision: promote, keep in shared context, or defer

Ask for confirmation on this draft before generating module-specific context files.

#### 3b. Promote sparingly using explicit gates

Create a module context doc only when all gates pass:

- Distinct language gate: at least 5 stable terms mostly owned by one boundary
- Boundary gate: clear technical seam (API boundary, data slice, package/module boundary, event boundary, or ownership boundary)
- Ambiguity gate: at least 2 terms would be confusing if left only in shared context
- Stability gate: concepts are durable domain language, not short-lived implementation details

If any gate fails, keep those terms in `.github/context/shared-context.md`.

Sparsity defaults:

- Create at most 3 new module context docs in one run unless the user asks for more.
- If two candidate modules share too much vocabulary, merge them and keep one context doc.

#### 3c. Write context docs after approval

Update `.github/context/shared-context.md` so it contains stable repository-wide vocabulary, not implementation trivia.

Then update `.github/context/context-map.md` for AI navigation:

- Keep it navigation-only.
- Keep shared context as the default route.
- Add approved module context routes only.
- For each route, state when to read it and what it owns.

When needed, update or add ADRs under `.github/adr/` for hard-to-reverse, trade-off-heavy, surprising decisions.

Completion criteria:

- Shared terms are canonical and non-duplicated.
- Module context docs are created only for approved candidates that passed all gates.
- Context map contains a complete navigation view of shared plus approved module contexts.
- Any architectural constraints relied on by the context are represented in ADRs or explicitly called out as missing.

### 4. Validate consistency across the stack

Cross-check for drift:

- `.github/copilot-instructions.md`
- `.github/ai/agent-workflow.md`
- `.github/context/context-map.md`
- `.github/context/shared-context.md`
- Relevant files in `.github/adr/`

Fix contradictions instead of leaving TODO prose.

Completion criterion:

No unresolved contradictions remain between workflow docs, context docs, ADRs, and observed code behavior.

### 5. Present and confirm

Show the user:

- what changed,
- what was inferred from code versus confirmed by user,
- any open questions that still need product-owner decisions.

Only then finalize.

Completion criterion:

User confirms the context is accurate enough for downstream engineering skills.

## Guardrails

- Never overwrite meaningful user-authored context blindly.
- Prefer merge/update over replacement.
- Use canonical terms consistently; avoid synonyms once a term is chosen.
- If confidence is low, keep grilling and keep reading until confidence is high.
