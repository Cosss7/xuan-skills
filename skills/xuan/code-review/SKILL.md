---
name: code-review
description: Review Git changes from a fixed point across Code Quality, Spec, and Requirements. Use for branch, PR, or work-in-progress reviews.
---

<code-review-skill>

Three-axis review of the diff between `HEAD` and a fixed point the user supplies:

- **Code Quality** evaluates implementation **form** — is the code clear, reliable, maintainable, testable, and free of significant code smells?
- **Spec** evaluates repository **contract** — does the change respect existing repository constraints, and does it add any new ones?
- **Requirements** evaluates task **intent** — does the code completely implement the originating PRD, ticket, issue, or acceptance criteria?

All three axes run as **parallel sub-agents** so they don't pollute each other's context, then this skill aggregates their findings.

## Terms

- **Repository constraint** — an established rule or contract governing the system's behaviour or structure, including invariants, architecture, module boundaries, dependency directions, interfaces, compatibility contracts, domain models, and business rules. It may be documented explicitly or established consistently by existing code and tests.
- **Violation** — a change that contradicts, replaces, weakens, removes, or otherwise invalidates an existing repository constraint.
- **Spec Addition** — a new repository constraint introduced for a previously unspecified area, or a compatible extension covering an additional case without invalidating or changing an existing repository constraint.

Classify an extension as a Spec Addition only when it preserves existing cases, does not contradict an existing repository constraint, and does not make previously conforming implementations or consumers non-conforming. Otherwise classify it as a Violation.

## Process

### 1. Pin the fixed point

Whatever the user said is the fixed point — a commit SHA, branch name, tag, `main`, `HEAD~5`, etc. If they didn't specify one, ask for it.

Capture the diff command once: `git diff <fixed-point>...HEAD` (three-dot, so the comparison is against the merge-base). Also note the list of commits via `git log <fixed-point>..HEAD --oneline`.

Before going further, confirm the fixed point resolves (`git rev-parse <fixed-point>`) and the diff is non-empty. A bad ref or empty diff should fail here — not inside three parallel sub-agents.

### 2. Identify the requirement/ticket source

Look for the originating requirement, in this order:

1. Issue references in the commit messages (`#123`, `Closes #45`, GitLab `!67`, etc.) — fetch via the workflow in `docs/agents/issue-tracker.md`.
2. A path the user passed as an argument.
3. A PRD/ticket file under `docs/`, or `.scratch/` matching the branch name or feature.
4. If nothing is found, ask the user where the requirement/ticket is. If they say there isn't one, the **Requirements** sub-agent will skip and report "no requirements available".

### 3. Identify the code quality sources

Look for repository guidance and stable coding practices relevant to readability, maintainability, testability, naming, abstraction, error handling, complexity, and design quality.

Use conventions about implementation form as heuristic evidence of Code Quality. Treat rules or stable patterns governing observable behaviour or permitted system structure as repository constraints under Spec.

The Code Quality axis also reviews concrete correctness and reliability risks, such as potential crashes or resource leaks, even when no Spec or Requirement defines the affected behaviour.

On top of whatever the repo documents, the Code Quality axis always carries the **smell baseline** below — a fixed set of Fowler code smells that applies even when a repo documents nothing. Two rules bind it:

- **The repo overrides.** Documented repository guidance always wins; where it endorses something the baseline would flag, suppress the smell.
- **Always a judgement call.** Each smell is a labelled heuristic, never a hard violation; skip anything tooling already enforces.

Apply this smell baseline:

- **Mysterious Name** — a function, variable, or type whose name doesn't reveal what it does or holds.
- **Duplicated Code** — changed code repeats logic within the diff or duplicates logic already present elsewhere in the codebase.
- **Feature Envy** — code depends more on another module's data than its own.
- **Data Clumps** — the same few fields or params keep travelling together (a type wanting to be born).
- **Primitive Obsession** — a primitive or string standing in for a domain concept that deserves its own type.
- **Repeated Switches** — the same `switch`/`if`-cascade on the same type recurs across the change.
- **Shotgun Surgery** — one logical change forces scattered edits across many files in the diff.
- **Divergent Change** — one file or module is edited for several unrelated reasons.
- **Speculative Generality** — abstraction, parameters, or hooks added for needs that do not currently exist.
- **Message Chains** — long `a.b().c().d()` navigation the caller shouldn't depend on.
- **Middle Man** — a class or function that mostly just delegates onward.
- **Refused Bequest** — a subclass or implementer that ignores or overrides most of what it inherits.
- **Overly Defensive Code** — redundant guards, fallbacks, or exception handling protect against states already excluded by types, validation, or established invariants; for example, rechecking for null after a validated non-null boundary.

### 4. Identify the spec sources

Look for evidence of the repository's existing constraints in `specs/`, `CONTEXT-MAP.md`, `CONTEXT.md`, glossaries, ADRs, architecture and module documentation, interface definitions, schemas, business-rule documentation, and relevant existing code or tests.

Treat stable behavioural or structural patterns in existing code and tests as repository constraints even when they are not documented separately. Do not invent constraints: cite the evidence for every Violation and Spec Addition. Report the two categories separately, and do not presume a Spec Addition is a problem.

### 5. Spawn the sub-agents in parallel

Use a separate `general-purpose` sub-agent for each axis. Give each the diff command, commit list, relevant sources and terms, and permission to inspect surrounding code. Require evidence for every finding, prohibit cross-axis review, and keep each finding concise.

- **Code Quality** evaluates implementation **form** — include the sources and smell baseline from step 3. Report concrete reliability or maintainability problems and applicable smells; explain the consequence of each judgement call.
- **Spec** evaluates repository **contract** — include the sources from step 4 and the Terms definitions. Report Violations and Spec Additions separately.
- **Requirements** evaluates task **intent** — include the requirement source from step 2. Report missing, partial, or incorrect implementation and behaviour outside task intent, especially corner-case behaviour that the requirements neither request nor constrain; cite the requirement for each finding.

The review is complete only when every changed file and hunk has been examined under every applicable axis, every finding cites evidence, and each axis reports findings, no findings, or an unverifiable status. Account for every stated requirement by tracing it to implementation and relevant tests or reporting it as missing, partial, or unverifiable.

### 6. Aggregate

Present the reports under `## Code Quality`, `## Spec`, and `## Requirements`, with Violations and Spec Additions separate under Spec. Do not merge or rerank findings across axes. End with the finding count for each axis.

</code-review-skill>
