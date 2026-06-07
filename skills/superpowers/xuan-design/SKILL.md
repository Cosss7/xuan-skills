---
name: xuan-design
description: Use before any creative work — exploring user intent, aligning terminology, grilling decision branches, and producing a spec before implementation. Combines brainstorming's design flow with grill-with-docs' terminology alignment and ADR creation.
---

# xuan-design — Design Through Shared Understanding

## Overview

Turn fuzzy ideas into fully-formed specs through a disciplined 5-phase process. Align terminology, grill decision branches, capture architecture decisions, and produce a written spec before any implementation.

**Core principle:** Design is an iterative dialogue, not a document. Write decisions down only after shared understanding is reached.

**Hard gate:** Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until the design is approved in Phase 4 and a spec is written.

## When to Use

**Always before:**
- New features or components
- Architecture changes
- Workflow changes
- Any implementation task

**Exceptions (ask your human partner):**
- Throwaway prototypes (use xuan-prototype instead)
- Bug fixes with clear reproduction

## Phase 1: Explore + Clarify Requirements

1. **Explore project context** — read files, docs, recent commits, existing CONTEXT.md
2. **Ask clarifying questions** — one at a time, understand purpose, constraints, success criteria
   - Prefer multiple choice when possible
   - If scope is too large for one spec, flag it: break into sub-projects
3. **Terminology alignment (iterative)** — when the user uses a fuzzy or loaded term:
   - Propose a precise canonical term
   - Check against existing CONTEXT.md glossary
   - If resolved, update CONTEXT.md immediately
4. **Visual companion** — if upcoming questions benefit from visual treatment (mockups, diagrams, layouts), offer a browser companion. One message, nothing else. Wait for consent.

## Phase 2: Explore Approaches

1. Propose 2-3 different approaches with trade-offs
2. Lead with your recommended option and reasoning
3. **Grill the chosen branch(es):**
   - Stress-test with concrete scenarios
   - Probe edge cases that force precision about boundaries
   - Cross-reference stated intent against actual code
   - Stop when user cannot clarify further or says "enough"

## Phase 3: Solidify Decisions

1. User confirms the chosen approach
2. **ADR (only when all three are true):**
   - Hard to reverse
   - Surprising without context
   - Result of a real trade-off with genuine alternatives
   - Use: `docs/ai-traces/adr/YYYY-MM-DD-title.md`
3. Update CONTEXT.md with any new resolved terms (not implementation details)

## Phase 4: Present Design + Approve

1. Present design section by section. Scale each section to its complexity.
   - Cover: architecture, components, data flow, error handling, testing
2. Ask after each section: "Does this look right?"
3. After all sections are approved: write the spec to `docs/ai-traces/specs/YYYY-MM-DD-topic-design.md`
4. **Spec self-review:**
   - Placeholder scan: any TBD, TODO, incomplete sections?
   - Internal consistency: do sections contradict each other?
   - Scope check: focused enough for one implementation plan?
   - Ambiguity check: could any requirement be read two ways?
5. Ask user to review the written spec. Wait for approval.

## Phase 5: Transition to Implementation

1. Invoke `xuan-writing-plans` to create a detailed implementation plan
2. Do NOT invoke any implementation skill directly

## Key Principles

- **One question at a time** — don't overwhelm
- **Terminology first** — shared language prevents wasted design
- **YAGNI ruthlessly** — strip unnecessary features
- **Alternatives before commitment** — 2-3 approaches, not one
- **Grill don't guess** — stress-test decisions with concrete scenarios
- **ADR sparingly** — only when hard to reverse, surprising, or a real trade-off
- **Design gate** — no code before approved design

## Visual Companion

When visual questions are ahead (mockups, layouts, diagrams, comparisons), offer the browser companion:

> "Some of what we're working on might be easier to explain if I can show it to you in a web browser. I can put together mockups, diagrams, comparisons, and other visuals as we go. Want to try it? (Requires opening a local URL)"

This offer MUST be its own message. Wait for response. If declined, proceed text-only.

## Red Flags — STOP

- Writing code before design approval
- Skipping terminology alignment ("we all know what X means")
- Proposing only one approach
- Skipping ADR for a hard-to-reverse decision
- Writing spec while still unclear about requirements
- Moving to implementation without user approving the written spec

**These all mean: Go back to Phase 1 or Phase 2. Don't proceed.**
