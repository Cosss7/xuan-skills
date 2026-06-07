# xuan-skills

A curated collection of AI agent skills, combining discipline from [obra/superpowers](https://github.com/obra/superpowers) and engineering workflow from [mattpocock/skills](https://github.com/mattpocock/skills). Compatible with any agent that supports SKILL.md (Claude Code, Cursor, Codex, Gemini, Zed, and others).

## Install

```bash
npx skills add Cosss7/xuan-skills
```

Or install a specific skill:

```bash
npx skills add Cosss7/xuan-skills --skill xuan-tdd
```

## Structure

```
skills/
├── superpowers/              (12 skills — from obra/superpowers)
├── mattpocock-engineering/   (7 skills — from mattpocock/skills engineering)
└── mattpocock-productivity/  (4 skills — from mattpocock/skills productivity)
```

Skills are prefixed with `xuan-`. Each skill is a directory containing `SKILL.md` with YAML frontmatter and optional supporting files.

## Modification Tracking

Skills that are modified, fused, or newly created include a `DIFF.md` in their skill directory documenting what changed and why. Skills copied as-is from upstream (rename only) do not have this file.

See [TRACKING.md](./TRACKING.md) for a per-skill summary of source, upstream commit, and modification status. Use this to sync changes from upstream repositories.

## Conventions

- **REQUIRED SUB-SKILL:** Use `xuan-<name>` — when another skill must run first
- **REQUIRED BACKGROUND:** You MUST understand `xuan-<name>` — prerequisite knowledge
- Docs output: `docs/ai-traces/specs/`, `docs/ai-traces/plans/`, `docs/ai-traces/adr/`
