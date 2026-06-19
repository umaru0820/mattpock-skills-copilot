---
name: domain-modeling
description: Build and sharpen a project's domain model. Use when the user wants to pin down domain terminology or a ubiquitous language, record an architectural decision, or when another skill needs to maintain the domain model.
---

# Domain Modeling

Actively build and sharpen the project's domain model as you design. This is the *active* discipline — challenging terms, inventing edge-case scenarios, and writing the glossary and decisions down the moment they crystallise. (Merely *reading* `.github/context/shared-context.md` for vocabulary is not this skill — that's a one-line habit any skill can do. This skill is for when you're changing the model, not just consuming it.)

## File structure

Most repos use `.github/context/shared-context.md`:

```
/
└── .github/
	├── context/
	│   ├── shared-context.md
	│   └── context-map.md
	└── adr/
		├── 0001-event-sourced-orders.md
		└── 0002-postgres-for-write-model.md
```

If `.github/context/context-map.md` exists, the repo has multiple contexts. The map points to where each one lives:

```
/
└── .github/
	├── context/
	│   ├── context-map.md
	│   ├── shared-context.md
	│   ├── ordering-context.md
	│   └── billing-context.md
	└── adr/
		├── 0001-event-sourced-orders.md
		└── 0002-postgres-for-write-model.md
```

Create files lazily — only when you have something to write. If `.github/context/shared-context.md` does not exist, create it when the first term is resolved. If no ADR folder exists, create `.github/adr/` when the first ADR is needed.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `.github/context/shared-context.md`, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account' — do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible — which is right?"

### Update .github/context/shared-context.md inline

When a term is resolved, update `.github/context/shared-context.md` right there. Don't batch these up — capture them as they happen. Use the format in [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).

`.github/context/shared-context.md` should be totally devoid of implementation details. Do not treat it as a spec, a scratch pad, or a repository for implementation decisions. It is a glossary document.

Legacy fallback: if a repository still uses legacy context/ADR locations, read and update those until migrated.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR. Use the format in [ADR-FORMAT.md](./ADR-FORMAT.md).
