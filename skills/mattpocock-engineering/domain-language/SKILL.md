---
name: domain-language
description: Build and sharpen a project's domain language. Use when the user wants to pin down domain terminology or a ubiquitous language, resolve fuzzy or overloaded terms, test conceptual boundaries, or when another skill needs to maintain CONTEXT.md. Do not use merely to read an existing glossary.
---

# Domain Language

Actively build and sharpen the language a project uses for its domain. Challenge terms, invent edge-case scenarios, and update the glossary the moment terminology crystallises.

Merely reading `CONTEXT.md` is not an invocation of this skill. Use it when changing the language, not just consuming it.

## File structure

Most repos have a single context:

```
/
├── CONTEXT.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```
/
├── CONTEXT-MAP.md
├── src/
│   ├── ordering/
│   │   └── CONTEXT.md
│   └── billing/
│       └── CONTEXT.md
```

Create files lazily. If no `CONTEXT.md` exists, create one only when the first term is resolved.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account' — do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible — which is right?"

### Update CONTEXT.md inline

When a term is resolved, update `CONTEXT.md` right there. Don't batch these up — capture them as they happen. Use the format in [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).

`CONTEXT.md` should be totally devoid of implementation details. Do not treat `CONTEXT.md` as a spec, a scratch pad, or a repository for implementation decisions. It is a glossary and nothing else.

### Route settled knowledge to the right artifact

Use these boundaries:

- **Glossary entry (`CONTEXT.md`)** — the canonical name and concise meaning of a domain concept.
- **Domain rule or feature behaviour (spec)** — behaviour that can be verified, including invariants, workflows, and acceptance criteria. If the current workflow does not own a spec, surface the rule to it instead of putting the rule in the glossary.
- **Consequential settled choice (ADR)** — why one durable option was chosen over real alternatives. Invoke `/decision-recording` to decide whether it qualifies and to create or update the ADR.
- **Temporary or easily reversible implementation choice** — record nowhere unless another workflow explicitly needs it.

Do not turn every clarified term into a decision. A definition belongs in the glossary; the reasoning behind a consequential boundary or policy may independently warrant an ADR.
