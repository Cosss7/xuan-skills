---
name: prepare-kernel-patch-series
description: Use when organizing Linux kernel commits or uncommitted changes into a patch series.
---

# 整理 Kernel Patch Series

## 目标

把已有 commits、uncommitted changes 或两者共同整理成符合 Linux kernel 普通贡献者要求的 patch series。整理前后的最终 tracked-file tree 必须一致；改变的是 history 的表达方式，而不是最终代码。

## 如何达到目标

- 完整阅读 [普通贡献者要求原文](references/ordinary-contributor-requirements.md)，并将其直接作为 patch series 的验收标准，不用摘要替代。另行遵守仓库指令、`MAINTAINERS` 和相关 subsystem 的提交规则。
- 确定 base 和完整 change set，从最终代码的 logical structure 出发整理 commits，而不是保留 development chronology。每个 changed hunk 只归属一个 patch，并为 commits 编写适合作为永久 kernel history 的 message。
- 重写 history 前建立能够恢复 staged、unstaged 和 untracked changes 的 snapshot。已 published、reviewed 或被其他 branch 使用的 commits，必须得到用户明确授权后才能改写。
- 保留 authorship 和有依据的 trailers。只有用户确认署名者可以签署 Developer's Certificate of Origin 后，才添加 `Signed-off-by`；不得捏造 review 或 test trailers。
- 对每个 commit 运行 `scripts/checkpatch.pl`、适用的 builds 和 tests，并验证每个 boundary。没有实际执行的 build、boot、hardware test 或 configuration 必须标记为 unverified。
- 完成后证明新 tip 与整理前的最终 tracked-file tree 一致。除非用户另行授权，不修改最终代码内容；只有用户明确要求时才生成或发送 patches。
