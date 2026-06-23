---
name: xuan-split-tasks
description: Invoke by other skill or manually invoke only.
---

<xuan-split-tasks-skill>

# xuan-split-tasks

Break a plan into independently-grabbable coding tasks using vertical slices (tracer bullets), write to plan doc.

<HARD-GATE>

- You MUST create checklist tracking each step of the process below
- Quiz the user for each HITL slice task until all tasks become AFK
- Vertical tracer bullet slice task

</HARD-GATE>

## Process

<process>

### 1. Gather context

Work from whatever is already in the conversation context. If a spec or design doc has written before, follow it, declare the doc path to user.

### 2. Explore the codebase (optional)

If you have not already explored the codebase, do so to understand the current state of the code. Tasks titles and descriptions should use the project's domain glossary vocabulary, and respect ADRs in the area you're touching.

Look for opportunities to prefactor the code to make the implementation easier. "Make the change easy, then make the easy change."

### 3. Draft vertical slices

Break the plan into **tracer bullet** tasks. Each task is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

<vertical-slice-rules>

- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Any prefactoring should be done first

</vertical-slice-rules>

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: HITL / AFK
- **Blocked by**: which other slices (if any) must complete first
- **User stories covered**: which user stories this addresses (if the source material has them)

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the dependency relationships correct?
- Should any slices be merged or split further?
- All unresolved decisions until HITL tasks become AFK.

Iterate until the user approves the breakdown.

### 5. Write the tasks to issues doc

**Save all approved tasks to to the temporary directory of the user's OS** - not the current workspace
- In dependency order (blockers first)
- All tasks in one file
- Use the issues-doc-template below.

<issues-doc-template>

**Every issues doc MUST start with this header:**

```markdown
# [Feature Name] issues

> **For agentic workers:** REQUIRED SUB-SKILL: Use skill `tdd` to implement this plan task-by-task.

**Design/Spec:** [relative path reference to design doc or spec doc or prd]

**Goal:** [One sentence describing what this builds]

---
```

**Task Structure:**

```markdown
### Task N: [short descriptive name]

**why:**

**what:**

**how:**

</issues-doc-template>

### 6.Self-Review

After writing the complete issues doc, look at the spec with fresh eyes and check the issues against it. This is a checklist you run yourself — not a subagent dispatch.

**1. Spec coverage:** Skim each section/requirement in the spec. Can you point to a task that implements it? List any gaps.

**2. Placeholder scan:** Search your plan for red flags — any of the patterns from the "No Placeholders" section above. Fix them.

**3. Type consistency:** Do the types, method signatures, and property names you used in later tasks match what you defined in earlier tasks? A function called `clearLayers()` in Task 3 but `clearFullLayers()` in Task 7 is a bug.

**4. Temeplate:** All follow the template.

**5. Task order:** In dependency order (blockers first)

If you find issues, fix them inline. No need to re-review — just fix and move on. If you find a spec requirement with no task, add the task.

</process>

</xuan-split-tasks-skill>
