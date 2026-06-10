# Changelog: setup

## Upstream Source

**Source:** `mattpocock/skills/skills/engineering/setup-matt-pocock-skills` — commit `4369256`

## Changes from Upstream

### Renamed

- `setup-matt-pocock-skills` → `setup`
- Updated title and all internal references

### Stripped Matt-Specific References

- Removed all mentions of "Matt Pocock" and "mattpocock"
- Repository references updated from `mattpocock/skills` to `Cosss7/xuan-skills`
- Skill references updated from `/setup-matt-pocock-skills` to `/setup`

### Updated: Frontmatter description

Before: `"Use once per repo to configure everything needed to use the mattpocock skills"` (paraphrased)
After: `"Use once per repo before any other skill — configures issue tracker connection, triage labels, and domain doc layout for xuan workflow skills."`

### Not Changed

- All 5 seed files (issue-tracker-github.md, issue-tracker-gitlab.md, issue-tracker-local.md, triage-labels.md, domain.md) — content unchanged
- The output config path remains `docs/agents/` (it's a project-level path, not repo-level)
- All setup flow and configuration logic
