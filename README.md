# xuan-skills

A curated collection of AI agent skills, combining discipline from [obra/superpowers](https://github.com/obra/superpowers) and engineering workflow from [mattpocock/skills](https://github.com/mattpocock/skills). Compatible with any agent that supports SKILL.md (Claude Code, Cursor, Codex, Gemini, Zed, and others).

## Install

Repository-owned skills may use the `xuan-` prefix. The prefix is optional for new or enhanced skills; upstream copies may keep their original names.

```bash
npx skills@latest add Cosss7/xuan-skills
```
Or install all skills global:

```bash
npx skills@latest add Cosss7/xuan-skills -g --skill '*'
```

Or install a specific skill:

```bash
npx skills@latest add Cosss7/xuan-skills --skill xuan-tdd
```

## Upgrade / Update

```bash
npx skills@latest update -g 
```

## Remove / Uninstall

interactive remove

```bash
npx skills@latest remove -g
```

## Structure

```
skills/
├── mattpocock-engineering/   (from mattpocock/skills engineering)
├── mattpocock-productivity/  (from mattpocock/skills productivity)
└── xuan/         (xuan customed)
```
