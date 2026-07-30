---
name: decision-recording
description: Evaluate and record consequential settled decisions as concise Architecture Decision Records. Use when the user asks to create or update an ADR, or when a design, domain-boundary, architecture, integration, or durable technology choice crystallizes and another skill needs to decide whether it warrants an ADR.
---

# Decision Recording

Record why a consequential choice was made so future work does not unknowingly re-litigate or reverse it. Record only settled decisions; use the surrounding design or grilling workflow to resolve open questions first.

## Classify the knowledge

Before writing, route the knowledge to the right artifact:

- **Canonical domain term or meaning** — update `CONTEXT.md` through `/domain-language`.
- **Domain rule, feature behaviour, or acceptance criterion** — put it in the relevant spec.
- **Consequential settled choice with durable trade-offs** — consider an ADR.
- **Temporary or easily reversible implementation choice** — usually record nowhere.

A decision about a domain boundary or product policy may warrant an ADR when its rationale must survive, even though the domain terms themselves remain in `CONTEXT.md`. Technical architecture decisions use the same qualification test.

## Qualify the decision

Create or update an ADR only when all three are true:

1. **Hard to reverse** — changing the choice later has meaningful cost.
2. **Surprising without context** — a future reader could reasonably question or undo it.
3. **Result of a real trade-off** — genuine alternatives were considered and one was chosen for specific reasons.

If any criterion is missing, skip the ADR and say briefly where the knowledge belongs, if anywhere.

## Locate the record

Read repository-local agent instructions and existing ADRs before choosing a path.

- Put system-wide decisions in the repository's system-wide ADR directory, normally `docs/adr/`.
- In a multi-context repository, put context-specific decisions in that context's ADR directory.
- Keep a decision system-wide when it constrains multiple contexts.

Do not duplicate an existing record. Update it when the decision is unchanged but its context needs clarification. Supersede it when the project has made a new decision; preserve the old record and link both directions when the repository's convention supports statuses.

## Record the decision

If the user explicitly requested an ADR, or the surrounding workflow already authorizes documentation updates, write it once the decision qualifies. Otherwise, offer to record it before creating the file.

Use [ADR-FORMAT.md](./ADR-FORMAT.md). Capture the context, chosen option, decisive reasoning, and only the non-obvious consequences or rejected alternatives worth preserving. Keep the record as short as the decision allows.
