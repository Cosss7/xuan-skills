# Changelog: xuan-design

## Design Context

This skill was created by combining two different approaches to upfront design from the upstream repositories. The initial fusion (v1) treated grill behavior as embedded rules within a 5-phase process. This was revised (v2) after identifying that the initial fusion lacked the concrete supporting files and entry instructions from grill-with-docs.

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

## Fusion Rationale (v1, superseded)

The two sources address different problems:
- brainstorming explores **what to build** (requirements, scope, options)
- grill-with-docs explores **how to think about it** (shared language, domain relationships, architecture decisions)

v1 fused them into a 5-phase flow with grill behavior embedded as rules within phases. This approach failed to preserve grill-with-docs' structural elements: `<what-to-do>`, `ADR-FORMAT.md`, and `CONTEXT-FORMAT.md`. The grill behavior was diluted into rules scattered across phases, losing its distinct interaction pattern.

## Fusion Design (v2)

**Approach:** Keep both source skills as intact as possible. brainstorming provides the overall flow (checklist); grill-with-docs is inserted as a discrete sub-process node.

**Process Flow:**

```
 1. Explore project context
 2. Offer visual companion (optional)
 3. Ask clarifying questions (one at a time)
 4. Propose 2-3 approaches → user picks one
        │
        ▼
 5. ┌──────────────────────────────────────────────┐
    │ Grill with docs (sub-process)                 │
    │ • <what-to-do> — interview relentlessly        │
    │ • Challenge against glossary                   │
    │ • Sharpen fuzzy language                       │
    │ • Stress-test with concrete scenarios          │
    │ • Cross-reference with code                    │
    │ • Update CONTEXT.md inline                     │
    │ • Offer ADRs sparingly → docs/adr/0001-slug.md │
    │ • One question at a time                       │
    │ Exit: user confirms or says "enough"           │
    └──────────────────────────────────────────────┘
        │
        ▼
 6. Present design (section by section, reference ADRs)
 7. Write spec → docs/ai-trace/specs/
 8. Spec self-review
 9. User reviews written spec
10. Transition → xuan-writing-plans
```

### Key changes from v1

| Element | v1 (old) | v2 (new) |
|---------|----------|----------|
| Structure | 5 phases | 10-step checklist (brainstorming style) |
| Grill behavior | Rules embedded in Phases 1-2 | Discrete sub-process node (step 5) |
| Step 3 terminology alignment | Challenge + update CONTEXT inline | Left untouched — all grill in step 5 |
| ADR path | `docs/ai-trace/adr/YYYY-MM-DD-title.md` | `docs/adr/0001-slug.md` (grill-with-docs style) |
| `<what-to-do>` | None | Grill-with-docs `<what-to-do>` verbatim in step 5 |
| ADR-FORMAT.md | Missing | Added (from grill-with-docs) |
| CONTEXT-FORMAT.md | Missing | Added (from grill-with-docs) |
| HARD-GATE | Inline rule in overview | `<HARD-GATE>` block (brainstorming style) |
| Exceptions | Prototype + bug fixes | Removed (no exceptions in original brainstorming) |

### Supporting files retained from brainstorming

- `visual-companion.md` — browser-based mockup/diagram companion (unchanged)
- `spec-document-reviewer-prompt.md` — prompt template for spec review subagent (unchanged)
- `scripts/` — server runtime for visual companion (unchanged)

## Cross-Reference Updates

- References `xuan-writing-plans` for step 10 transition
- References `xuan-grill-with-docs` for step 5 grilling
- No `superpowers:` cross-refs in original skill

## Changes in v3

| Element | v2 | v3 |
|---------|-----|-----|
| Grill content | Inline copy of grill-with-docs `<what-to-do>` + `<supporting-info>` (~80 lines) | Reference to invoke `xuan-grill-with-docs` skill |
| Step 5 wording | "enter grill-with-docs mode" | "invoke xuan-grill-with-docs to stress-test decisions" |
| Terminal state | `writing-plans` | `xuan-writing-plans` |
| Step 10 transition | Invoke `writing-plans` | Invoke `xuan-writing-plans` |
| Visual companion ref | `skills/brainstorming/visual-companion.md` | `visual-companion.md` |

### Rationale

- **Deduplication**: Removed 80-line inline copy of grill-with-docs content. The skill is now invoked independently, avoiding maintenance of duplicate content across two skills.
- **Naming consistency**: All cross-references now use the `xuan-` prefix, matching project convention.
