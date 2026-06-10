---
name: xuan-subagent-driven-development
description: Invoke by other skill or manually invoke only.
---

<xuan-subagent-driven-development-skill>

# xuan-subagent-driven-development

Execute plan by dispatching fresh subagent per task, with two-stage review after each: spec compliance review first, then code quality review.

**Why subagents:** You delegate tasks to specialized agents with isolated context. By precisely crafting their instructions and context, you ensure they stay focused and succeed at their task. They should never inherit your session's context or history — you construct exactly what they need. This also preserves your own context for coordination work.

**Core principle:** Fresh subagent per task + two-stage review (spec then quality) = high quality, fast iteration

**Continuous execution:** Do not pause to check in with your human partner between tasks. Execute all tasks from the plan without stopping. The only reasons to stop are: BLOCKED status you cannot resolve, ambiguity that genuinely prevents progress, or all tasks complete. "Should I continue?" prompts and progress summaries waste their time — they asked you to execute the plan, so execute it.

**Context:** Work from whatever is already in the conversation context. If a plan doc has written before, follow it, declare the doc path to user.

<HARD-GATE>

**HARD-GATE:** 
- You MUST tell subagent invoke skill `xuan-tdd`
- You MUST create checklist tracking the tasks in the plan doc
- checklist last step is dispatch code reviewer subagent 把所有任务的修改当作一个整体 review
- Each task MUST 遵循下面的 process , 不允许跳过任何 step

</HARD-GATE>

## Process

<process>

**Step 1: Dispatch implementer subagent**

将 plan doc 中的任务按顺序调用 subagent 完成, 给 subagent 的提示词包括: 任务所需的上下文 ,  plan doc 和 design doc 的路径，要求 subagent 必须遵守， subagent 必须调用 skill xuan-test-driven-development , 完成后提交代码

**Step 2: Answer subagent questions**

如果 subagent 提问, 你应该回答并且提供相应的上下文

**Step 3: implementer subagent 开始工作**

等待 implementer subagent 完成分配的任务

**Step 4: Dispatch spec reviewer subagent**

给 spec reviewer subagent 的提示词包括: task 的完整内容, design/spec doc 的路径, 要求 subagent 检查任务的实现是否完全符合 design/spec doc, 是否遵循 tdd 要求, 测试覆盖的完善程度

If verification fails, 不能进行下一步，直到 let implementer subagent fix the spec gaps

**Step 5: Dispatch code quality reviewer subagent**

Dispatch reviewer subagent [code quality reviewer subaget prompt template](./code-quality-reviewer-prompt.md)

If verification fails, 不能进行下一步，直到 let implementer subagent fix the spec gaps

**Step 6: Mark the task as complete**

标记当前任务完成。如果还有未完成的任务， return to step 1 , 如果所有任务都完成，则结束 process

</process>

## Red Flags

**Never:**
- Start implementation on main/master branch without explicit user consent
- Skip reviews (spec compliance OR code quality)
- Proceed with unfixed issues
- Dispatch multiple implementation subagents in parallel (conflicts)
- Make subagent read plan file (provide full text instead)
- Skip scene-setting context (subagent needs to understand where task fits)
- Ignore subagent questions (answer before letting them proceed)
- Accept "close enough" on spec compliance (spec reviewer found issues = not done)
- Skip review loops (reviewer found issues = implementer fixes = review again)
- Let implementer self-review replace actual review (both are needed)
- **Start code quality review before spec compliance is ✅** (wrong order)
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

</xuan-subagent-driven-development-skill>
