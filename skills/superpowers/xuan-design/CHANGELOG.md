# Changelog: xuan-design

## Design Context

This skill was created by combining two different approaches to upfront design from the upstream repositories, after a grill-with-docs session that analyzed their differences and decided on a fusion.

## Upstream Sources

**Source A: `brainstorming`** (obra/superpowers)
- Commit: `3f80f1c`
- Purpose: Product requirement exploration before any implementation
- Process: 9-step checklist — explore context, ask clarifying questions, propose 2-3 approaches, present design section by section, write spec, self-review, user review, transition to writing-plans
- Key trait: Hard gate — no code without approved design
- Output: `docs/superpowers/specs/` design document

**Source B: `grill-with-docs`** (mattpocock/skills)
- Commit: `e74f006`
- Purpose: Terminology alignment and architectural decision capture
- Process: Challenge user's language against CONTEXT.md, sharpen fuzzy terms, stress-test with concrete scenarios, update CONTEXT.md inline, write ADRs sparingly
- Key trait: One question at a time, walk every decision branch until shared understanding
- Output: Updated CONTEXT.md + ADRs in `docs/adr/`

## Fusion Rationale

The two sources address different problems:
- brainstorming explores **what to build** (requirements, scope, options)
- grill-with-docs explores **how to think about it** (shared language, domain relationships, architecture decisions)

A project needs both, and they were historically invoked separately. The fusion creates a single end-to-end design phase that:
1. Starts with requirement exploration (brainstorming style)
2. Aligns terminology iteratively as fuzzy terms emerge (grill style)
3. Grills decision branches after narrowing options (grill style)
4. Captures architecture decisions (grill style's ADR)
5. Produces a spec and transitions to implementation (brainstorming style)

## Key Design Decisions

### 1. Terminology alignment is iterative, not upfront

**Decision:** Don't check CONTEXT.md glossary at the start of the session. Instead, align terms when fuzzy language emerges during requirement discussion.

**Why:** If the user says "I want to build an e-commerce system", we don't know if it's B2B/B2C, physical/digital, single/multi-tenant until we ask questions. Premium glossary alignment risks defining terms that don't apply.

### 2. Grill happens on chosen branches, not all possible branches

**Decision:** First present 2-3 approaches, let user pick, then grill the chosen direction. Not: grill every possible approach before narrowing.

**Why:** "Grill all decision branches" is infinite — there's always another edge case. The termination condition is "user cannot clarify further or says 'enough'."

### 3. ADR after decision confirmation, not mid-grilling

**Decision:** Write ADR in Phase 3 (Solidify Decisions), after the user confirms an approach. Not while grilling is still in progress.

**Why:** An ADR records a decision. Until the decision is confirmed, there's nothing to record. Mid-grilling ADRs get rewritten every time the user changes their mind.

### 4. Design approval gate is inherited from brainstorming

**Decision:** The hard gate ("no code before approved design") is retained from brainstorming. Phase 4 requires section-by-section user approval, then a written spec, then user review of the spec, before any implementation.

**Why:** grill-with-docs had no such gate — it assumes decisions are captured during conversation. The brainstorming gate forces explicit sign-off, which prevents premature implementation.

### 5. Phase 5 transitions to xuan-writing-plans

**Decision:** After spec is approved, the skill hands off to `xuan-writing-plans` for implementation planning. Not to any other skill.

**Why:** Consistent with brainstorming's original design. writing-plans decomposes the spec into bite-sized executable tasks.

## Process Flow (Final)

```
Phase 1: Explore + Clarify Requirements
  - Explore project context (files, docs, commits, CONTEXT.md)
  - Clarifying questions (one at a time)
  - Terminology alignment (as fuzzy terms emerge)
  - Visual companion offer (optional)

Phase 2: Explore Approaches
  - Propose 2-3 approaches with trade-offs + recommendation
  - User picks
  - Grill chosen branch(es) with concrete scenarios
  - Stop when user cannot clarify further or says "enough"

Phase 3: Solidify Decisions
  - User confirms approach
  - ADR (only when hard-to-reverse / surprising / real trade-off)
  - Update CONTEXT.md with resolved terms

Phase 4: Present Design + Approve
  - Present design section by section
  - User approves each section
  - Write spec to docs/ai-traces/specs/
  - Spec self-review (placeholders, consistency, scope, ambiguity)
  - User reviews written spec
  - User approves → proceed

Phase 5: Transition
  - Invoke xuan-writing-plans
```

## Rejected Alternatives

**Alternative: Keep brainstorming and grill-with-docs as separate skills**
- Rejected because: Users would need to know which to invoke and when. A single design phase that covers both requirement exploration and terminology alignment is more cohesive.

**Alternative: Name it "brainstorming" (original superpowers name)**
- Rejected because: The fused skill includes significant grill behavior that "brainstorming" doesn't convey. The `xuan-design` name reflects its role as the design phase of the development lifecycle.

**Alternative: Start with CONTEXT.md glossary check (grill style)**
- Rejected because: Premature terminology alignment wastes effort when scope is unknown.

## Cross-Reference Updates

- References `xuan-writing-plans` for Phase 5 transition
- References `xuan-prototype` as exception ("use xuan-prototype instead")
- No `superpowers:` cross-refs in original skill
