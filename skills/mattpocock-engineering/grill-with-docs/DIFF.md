# Changelog: grill-with-docs

## Design Context

Previously as-is (rename only from upstream mattpocock/skills `grill-with-docs`). v1 adds a hard gate to prevent implementation before design approval.

## Upstream Source

**Source:** `grill-with-docs` (mattpocock/skills)
- Commit: `e74f006`
- Purpose: Terminology alignment and architectural decision capture through structured grilling

## Changes

| Element | Upstream | Modified |
|---------|----------|----------|
| HARD-GATE | None | Added `<HARD-GATE>` block — prevents any implementation action until design is presented and user-approved |

## Reason

Aligns with design's hard-gate discipline. As a standalone skill, grill-with-docs could be invoked mid-implementation without a guard. The hard gate ensures the skill serves its intended purpose (terminology alignment and design stress-testing) and is not used as a shortcut past the design phase.

## Cross-Reference Updates

- None. The skill has no cross-references to other skills.
