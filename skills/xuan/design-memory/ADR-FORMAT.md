# ADR Format

Follow repository-local instructions when they define an ADR location. Otherwise, system-wide ADRs live in `docs/adr/`; in a multi-context repository, context-specific ADRs live under that context's `docs/adr/`.

Use sequential numbering within the selected directory: `0001-slug.md`, `0002-postgres-for-write-model.md`, etc.

Create the selected ADR directory lazily, only when the first ADR is needed there.

## Template

```md
# {Short title of the decision}

{1-3 sentences: what's the context, what did we decide, and why.}
```

That's it. An ADR can be a single paragraph. The value is in recording *that* a decision was made and *why*, not in filling out sections.

## Optional sections

Only include these when they add genuine value. Most ADRs won't need them.

- **Status** frontmatter (`accepted | deprecated | superseded by ADR-NNNN`) — useful when decisions are revisited
- **Considered Options** — only when the rejected alternatives are worth remembering
- **Consequences** — only when non-obvious downstream effects need to be called out

## Numbering

Scan the selected ADR directory for the highest existing number and increment by one.
