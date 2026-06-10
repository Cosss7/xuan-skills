# Changelog: finishing-a-development-branch

## Upstream Source

**Source:** `obra/superpowers/skills/finishing-a-development-branch` — commit `f2cbfbe`

## Changes from Upstream

### Updated: Config paths

- `~/.config/superpowers/worktrees/` → `~/.config/xuan/worktrees/`

This affects the provenance check that determines whether the tool owns cleanup of a worktree.

### Updated: Cross-references

- `superpowers:test-driven-development` → `test-driven-development`
- `superpowers:verification-before-completion` → `verification-before-completion`

### Updated: Frontmatter name

- `name: finishing-a-development-branch` → `name: finishing-a-development-branch`

### Not Changed

- All 4 options (merge/PR/keep/discard) and their flows
- Environment detection (normal repo vs named worktree vs detached HEAD)
- Test verification before any option is presented
- Confirmation requirement for discard
- All red flags and common mistakes
