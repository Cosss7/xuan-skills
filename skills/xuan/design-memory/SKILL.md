---
name: design-memory
description: Build and preserve a project's durable design memory by sharpening domain language in CONTEXT.md and recording consequential settled decisions as Architecture Decision Records. Use when terminology or conceptual boundaries need clarification, when the user asks to create, update, supersede, or assess an ADR, or when another design workflow needs to preserve language or rationale that has crystallized. Do not use merely to read existing project context.
---

# Design Memory

Actively sharpen and preserve the project's shared understanding as design unfolds. Challenge ambiguous language, test conceptual boundaries, and record settled knowledge as soon as it crystallizes. Reading existing context is not an invocation of this skill; use it when changing the project's language or durable rationale.

## File structure

Most repositories have one context:

```text
/
├── CONTEXT.md
├── docs/adr/
└── src/
```

If a root `CONTEXT-MAP.md` exists, the repository has multiple contexts. It points to each context and its documentation:

```text
/
├── CONTEXT-MAP.md
├── docs/adr/                          ← system-wide decisions
└── src/
    ├── ordering/
    │   ├── CONTEXT.md
    │   └── docs/adr/                 ← context-specific decisions
    └── billing/
        ├── CONTEXT.md
        └── docs/adr/
```

Follow repository-local instructions and existing conventions first. Otherwise, use a root `CONTEXT.md` and `docs/adr/`. Create files and directories lazily, only when settled knowledge needs recording.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with `CONTEXT.md`, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account' — do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

Stress-test domain relationships with specific scenarios. Invent edge cases that force precision about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. Surface contradictions: "Your code cancels entire Orders, but you just said partial cancellation is possible — which is right?"

### Route settled knowledge

- **Canonical domain term or meaning** — update the relevant `CONTEXT.md`.
- **Domain rule, feature behaviour, or acceptance criterion** — put it in the relevant spec, or surface it to the workflow that owns the spec.
- **Durable choice made through genuine trade-offs** — evaluate it for an ADR.
- **Temporary or easily reversible implementation choice** — record nowhere unless another workflow explicitly needs it.

Do not turn every clarified term into a decision. Definitions belong in the glossary; the rationale behind a consequential boundary or policy may independently warrant an ADR.

### Update the glossary inline

When a term is resolved, update `CONTEXT.md` immediately rather than batching changes. Use [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).

Keep `CONTEXT.md` free of implementation details. It is a glossary, not a spec, scratch pad, or record of implementation decisions.

### Record ADRs sparingly

Create a new ADR only when all three are true:

1. Reversing the decision would have meaningful cost.
2. A future reader could reasonably question or undo it without the rationale.
3. Genuine alternatives were considered and rejected for specific reasons.

Otherwise, skip the ADR and briefly state where the knowledge belongs, if anywhere. Existing ADRs may be clarified without requalifying the original decision.

Read existing ADRs before writing. Do not duplicate an existing decision. Keep decisions that constrain multiple contexts system-wide; place context-specific decisions with that context. Update an ADR when its decision is unchanged, and supersede it when a new decision replaces it. Preserve and cross-link both records when repository conventions support it.

Write an ADR only when the user requested it or the invoking workflow authorizes documentation changes. Otherwise, report that it qualifies and recommend recording it.

Use [ADR-FORMAT.md](./ADR-FORMAT.md). Preserve the context, decision, decisive reasoning, and only the consequences or rejected alternatives worth remembering.
