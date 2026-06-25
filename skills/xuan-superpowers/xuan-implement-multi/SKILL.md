---
name: xuan-implement
description: User-invoked only.
---

<xuan-implement-skill>

# xuan-implement

Execute plan by dispatching fresh subagent per task.

**Why subagents:** You delegate tasks to specialized agents with isolated context. By precisely crafting their instructions and context, you ensure they stay focused and succeed at their task. They should never inherit your session's context or history — you construct exactly what they need. This also preserves your own context for coordination work.

**Core principle:** Fresh subagent per task + two-stage review (spec then quality) = high quality, fast iteration

**Continuous execution:** Do not pause to check in with your human partner between tasks. Execute all tasks from the plan without stopping. The only reasons to stop are: BLOCKED status you cannot resolve, ambiguity that genuinely prevents progress, or all tasks complete. "Should I continue?" prompts and progress summaries waste their time — they asked you to execute the plan, so execute it.

**Context:** Work from whatever is already in the conversation context. If a plan doc has written before, follow it, declare the doc path to user. Plan doc or issues doc.

<HARD-GATE>

**HARD-GATE:** 
- You MUST tell subagent invoke skill `tdd` not other test driven development skills
- You MUST tell subagent **MUST follow** skill `tdd`
- You MUST create checklist tracking the tasks in the plan doc
- Checklist last step is dispatch code reviewer subagent to use `/review` to review the work
- Each task MUST follow the process below. No step may be skipped

</HARD-GATE>

## Anti-Pattern

**There is task for writing test so subagent can not follow `tdd`**: subagent only care about the task dispatched to it, MUST follow skill `tdd` in any case

**Subagent call other test driven development skill**: subagent NEVER invoke other test driven development skill

## Process

<process>

**Step 1: Dispatch implementer subagent**

Pick the next incomplete task from the plan doc in order and dispatch new implementer subagent to complete it. 

The subagent prompt MUST include: 
  - task context
  - plan doc and design/spec doc paths reference
  - MUST follow both docs
  - invoke skill tdd
  - commit code when done

**Step 2: Answer subagent questions**

If the subagent asks questions, answer them with the necessary context

**Step 3: Dispatch reviewer subagent**

Subagent review spec gaps and code quality.

MUST tell the reviewer subagent: 
  - the complete task description
  - the design/spec doc, issues doc reference
  - MUST check: 
    - (a) full compliance with the design/spec doc
    - (b) adherence to TDD requirements
  - use `/review` review code quality

If verification fails, you MUST let implementer subagent fix the spec gaps or code before go to the next step

**Step 4: Mark the task as complete**

Mark this task complete. If unfinished tasks remain, return to Step 1. Otherwise, the process is complete

</process>

## Red Flags

**Never:**
- Start implementation on main/master branch without explicit user consent
- Skip reviews (spec compliance OR code quality)
- Proceed with unfixed issues
- Dispatch multiple implementation subagents in parallel (conflicts)
- Skip scene-setting context (subagent needs to understand where task fits)
- Ignore subagent questions (answer before letting them proceed)
- Accept "close enough" on spec compliance (spec reviewer found issues = not done)
- Skip review loops (reviewer found issues = implementer fixes = review again)
- Let implementer self-review replace actual review (both are needed)
- Move to next task while either review has open issues

**If subagent asks questions:**
- Answer clearly and completely
- Provide additional context if needed
- Don't rush them into implementation

**If reviewer finds issues:**
- Implementer (same subagent) fixes them
- Reviewer reviews again
- Repeat until approved
- Don't skip the re-review

**If subagent fails task:**
- Dispatch fix subagent with specific instructions
- Don't try to fix manually (context pollution)

</xuan-implement-skill>
