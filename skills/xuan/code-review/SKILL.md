---
name: code-review
description: Review the changes since a fixed point (commit, branch, tag, or merge-base) along three axes — Code Quality, Spec, and Requirements. Runs all applicable reviews in parallel sub-agents and reports them side by side. Use when the user wants to review a branch, a PR, work-in-progress changes, or asks to "review since X".
---

<code-review-skill>

Three-axis review of the diff between `HEAD` and a fixed point the user supplies:

- **Code Quality** — is the code clear, reliable, maintainable, testable, and free of significant code smells?
- **Spec** — does the change respect existing repository constraints, and does it add any new ones?
- **Requirements** — does the code completely implement the originating PRD, ticket, issue, or acceptance criteria?

All three axes run as **parallel sub-agents** so they don't pollute each other's context, then this skill aggregates their findings.

## Terms

- **Repository constraint** — an established rule or contract governing the system's behaviour or structure, including invariants, architecture, module boundaries, dependency directions, interfaces, compatibility contracts, domain models, and business rules. It may be documented explicitly or established consistently by existing code and tests.
- **Spec Addition** — a new repository constraint introduced for a previously unspecified area, or a compatible extension covering an additional case without invalidating or changing an existing repository constraint.

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

Use these as evidence of code quality, not as repository constraints. Explicit repository constraints belong to the Spec axis.

The Code Quality axis also reviews concrete correctness and reliability risks, such as potential crashes or resource leaks, even when no Spec or Requirement defines the affected behaviour.

On top of whatever the repo documents, the Code Quality axis always carries the **smell baseline** below — a fixed set of Fowler code smells that applies even when a repo documents nothing. Two rules bind it:

- **The repo overrides.** A documented repo standard always wins; where it endorses something the baseline would flag, suppress the smell.
- **Always a judgement call.** Each smell is a labelled heuristic ("possible Feature Envy"), never a hard violation — and, like any standard here, skip anything tooling already enforces.

Each smell reads *what it is* → *how to fix*; match it against the diff:

- **Mysterious Name** — a function, variable, or type whose name doesn't reveal what it does or holds. → rename it; if no honest name comes, the design's murky.
- **Duplicated Code** — the same logic shape appears in more than one hunk or file in the change. → extract the shared shape, call it from both.
- **Feature Envy** — a method that reaches into another object's data more than its own. → move the method onto the data it envies.
- **Data Clumps** — the same few fields or params keep travelling together (a type wanting to be born). → bundle them into one type, pass that.
- **Primitive Obsession** — a primitive or string standing in for a domain concept that deserves its own type. → give the concept its own small type.
- **Repeated Switches** — the same `switch`/`if`-cascade on the same type recurs across the change. → replace with polymorphism, or one map both sites share.
- **Shotgun Surgery** — one logical change forces scattered edits across many files in the diff. → gather what changes together into one module.
- **Divergent Change** — one file or module is edited for several unrelated reasons. → split so each module changes for one reason.
- **Speculative Generality** — abstraction, parameters, or hooks added for needs the requirements don't have. → delete it; inline back until a real need shows.
- **Message Chains** — long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the walk behind one method on the first object.
- **Middle Man** — a class or function that mostly just delegates onward. → cut it, call the real target direct.
- **Refused Bequest** — a subclass or implementer that ignores or overrides most of what it inherits. → drop the inheritance, use composition.
- **Defensive Programming** — code guards a corner case that the originating requirement or ticket neither describes nor constrains, implicitly inventing behaviour outside the stated contract. → report the unrequested behaviour and ask for the contract to be clarified before preserving the guard.

### 4. Identify the spec sources

Look for evidence of the repository's existing constraints in `specs/`, `CONTEXT-MAP.md`, `CONTEXT.md`, glossaries, ADRs, architecture and module documentation, interface definitions, schemas, business-rule documentation, and relevant existing code or tests.

Treat stable behaviour and patterns in existing code and tests as repository constraints even when they are not documented separately. Do not invent constraints: every claimed violation or addition must cite its evidence.

The Spec axis reports two categories separately:

- **Violations** — changes that contradict, replace, weaken, remove, or otherwise invalidate an existing repository constraint.
- **Additions** — Spec Additions introduced by the diff. Report these without presuming they are problems.

Classify an extension as an Addition only when it preserves existing cases, does not contradict an existing repository constraint, and does not make previously conforming implementations or consumers non-conforming. Otherwise classify it as a Violation.

### 5. Spawn the sub-agents in parallel

Use the `general-purpose` subagent for each.

**Code Quality sub-agent prompt** — include:

- The full diff command and commit list.
- The code quality sources found in step 3, **plus the smell baseline from step 3** pasted in full — the sub-agent has no other access to it.
- The brief: "Report — per file/hunk where relevant — (a) concrete correctness or reliability risks; (b) clarity, maintainability, testability, abstraction, error-handling, or unnecessary-complexity problems; and (c) any baseline smell, naming it and quoting the hunk. Explain the concrete consequence of every judgement call. Treat smells as heuristics, skip anything tooling enforces, and do not assess Spec or Requirements conformance. Under 400 words."

**Spec sub-agent prompt** — include:

- The full diff command and commit list.
- The spec sources found in step 4.
- The definitions of **Repository constraint** and **Spec Addition**, plus the classification rule from step 4.
- The brief: "Report Violations and Additions separately. Cite the evidence for every finding, including stable existing code or tests when they are the source. Do not invent constraints or treat Additions as inherently problematic. Do not assess Code Quality or Requirements fulfillment. Under 400 words."

**Requirements sub-agent prompt** — include:

- The full diff command and commit list.
- The path or fetched contents of the PRD, ticket, issue, acceptance criteria, or spec.
- The brief: "Report: (a) requirements that are missing or partial; (b) behaviour in the diff that wasn't asked for; (c) requirements that look implemented but where the implementation looks wrong; and (d) requirements that cannot be traced to implementation and relevant tests. Quote the requirement for each finding. Do not assess Code Quality or Spec conformance. Under 400 words."

If the requirement source is missing, skip the Requirements sub-agent and report that this axis cannot be verified.

### 6. Aggregate

Present the three reports under `## Code Quality`, `## Spec`, and `## Requirements` headings, verbatim or lightly cleaned. Do **not** merge or rerank findings — the three axes are deliberately separate (see _Why three axes_).

Under Spec, keep **Violations** and **Additions** separate. If the requirement source is missing, report that Requirements could not be verified; do not report it as passing.

End with a one-line summary: total findings per axis, and the worst issue _within each axis_ (if any). Don't pick a single winner across axes — that's the reranking the separation exists to prevent.

## Why three axes

A change can pass one axis and fail another:

- High-quality code can implement the wrong thing → **Code Quality pass, Requirements fail.**
- Code can satisfy the ticket while violating an existing repository constraint → **Requirements pass, Spec fail.**
- Code can satisfy both Spec and Requirements while still being difficult to maintain → **Spec and Requirements pass, Code Quality fail.**
- A valid change can introduce a new repository constraint → report it as a Spec **Addition**, not automatically as a defect.

Reporting them separately stops one axis from masking another.

</code-review-skill>
