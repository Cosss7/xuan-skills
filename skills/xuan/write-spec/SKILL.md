---
name: write-spec
description: User-invoked only. Turn investigated decisions into durable specs.
disable-model-invocation: true
---

# Write Spec

把新功能、或既有功能补建需求，收敛成一份或多份长期可维护的正式 spec。

## 目标

使 spec 成为功能或需求的长期行为真相源，让不了解原始讨论的人也能理解、实现、验证和演进该功能。

## 全局原则

只描述规范行为、领域边界、集成契约和可验证结果。除非某项实现细节本身已经成为必须保留的约束，否则不要固定类名、函数名、存储机制、HTTP 路径、算法或实施步骤。不要加入任务拆分、负责人、排期或完整讨论历史。

- 对于已有实现，始终区分目标模型、当前实现映射、现状偏差、已有保障和演进验收。当前实现与目标模型冲突时，以目标模型表达演进方向，同时如实记录偏差。
- 对于全新功能，用现有系统约束和集成边界替代当前实现映射，不要编造尚不存在的行为。
- decision log 保存事实、讨论来源、推荐理由、用户决定和覆盖关系；正式 spec 只保留理解、实现、验证和演进功能所需的最终一致结论。
- 当前实现映射可以引用稳定的模块路径和 symbol，但不要依赖容易漂移的行号。

## Workflow

### 1. 定位需求与输出

先阅读 repository-local instructions、已有 spec、领域文档和相关 ADR，再判断当前任务属于：

- 新功能或新需求；
- 为完整的既有功能补建 spec。

确认要规范的领域范围和相邻边界，不把 `write-spec` 限定成从代码反向生成文档。

确定正式 spec 的预定路径，优先级为：

1. 用户明确指定的路径；
2. repository-local instructions；
3. repository 根目录下的 `specs/`。

把 `AGENTS.md`、`CLAUDE.md`、`CONTEXT.md` 等文件声明的 spec 输出位置视为 repository-local instructions；即使目标目录尚未创建也必须遵循。只有 repository 没有任何相关约定时，才 fallback 到 `specs/`。

根据实际领域边界决定写一份还是多份 spec，并使用能表达各自权威范围的文件名。不要套用固定目录模板。

为本次工作确定 topic 和 decision log 路径。默认使用 `.scratch/<topic>-decisions.md`。decision log 是工作记录，不是正式 spec，不要在流程结束时自动删除。

### 2. 调查可确认的事实

阅读相关代码、测试、spec、文档、配置和历史决定，建立当前行为与约束的证据基础。能从 repository 中查明的事实不要询问用户。

若规范依赖 repository 外的协议、第三方 API 或当前版本行为，查阅对应的 primary sources；把它们作为事实证据，不要用外部资料替用户决定产品行为。

根据任务类型调整调查重点：

- 新功能：调查相邻模块、既有约束、可复用能力和消费者。
- 既有功能补建：从实现和测试中提取事实，但不要自动把偶然实现固化成目标规则。

区分三类内容：已确认事实、尚未确认的事实、必须由用户决定的规范分支。不得把推断写成用户决定。

### 3. 建立待决策模型

在提问前先形成足够完整的候选模型和 decision tree。按实际领域检查目标、范围、术语、参与者、权威所有者、正常行为、状态与事件、逻辑契约、数据与身份、失败与恢复、时间与并发、持久化、消费者及 UI 可观察行为。

这些维度用于发现边界，不是固定章节模板。只保留与当前功能有关的内容。

为每个规范分支准备 Agent recommendation 及理由。编辑性且不改变语义的选择由 Agent 自行处理；会改变行为、领域边界或演进方向的假设必须交给用户确认。不要把已由用户指令、repository-local instructions 或既有事实决定的事项重新包装成问题。

### 4. 运行 Grilling

Load `/grilling`, then run a grilling session for the entire decision-making phase. Give it the topic, the decision log path, the investigated facts, the unresolved specification branches, and the proposed recommendations. Explicitly exclude settled facts and editorial choices such as document placement and formatting.

让 Grilling 持续追问到 shared understanding。不要在 `write-spec` 中复制其批次纪律或自行缩短该阶段。Grilling 完成后，控制权回到本 workflow。

### 5. 执行一致性审计

启动一个 fresh-context subagent 执行 read-only audit。只向它提供 decision log 路径、相关代码/测试/既有 spec 路径和本阶段的审计目标，不提供主 Agent 的结论、预期答案或修复建议。

要求 subagent 完整阅读 decision log 和给定 artifacts，沿决定之间的依赖关系审计，并返回带证据出处的 findings：

- 后来的决定是否明确覆盖并修正旧决定；
- 术语、状态、事件、契约和消费者行为是否彼此一致；
- 正常路径、失败路径、恢复、时间、并发和持久化是否存在矛盾；
- 目标模型、当前实现映射、现状偏差、已有保障和演进验收是否被混淆；
- 每项规范行为是否具有可观察、可验证的结果。

审计是根据实际领域寻找冲突，不是机械执行固定 checklist。主 Agent 复核 findings；发现新的规范分支时，返回 Grilling，不得自行补答案。

只有所有会影响规范行为、领域边界或演进方向的决定都已确认，才可宣布讨论闭合。不影响规范的未知事实可以保留为明确的已知未知项；阻塞性问题不得带入正式 spec。

### 6. 请求成稿授权

向用户说明：

- shared understanding 已达到；
- 预定生成的一份或多份 spec 及其路径；
- 仍保留但不阻塞规范的已知未知项。

然后明确询问是否开始写正式 spec。只有用户明确要求写 spec 或开始成稿，才进入下一阶段。

### 7. 编写正式 spec

围绕以下核心结构组织正式 spec，不使用固定 PRD 模板：

- 目标与范围；
- 状态；
- 状态转换；
- 状态的消费者与状态转换的触发者；
- 业务规则，重点描述状态相关规则；
- 消费者与触发者的业务规则；
- 当前实现映射与现状偏差；
- 已有保障与演进验收。

把必要术语、权威所有者、失败、恢复、时间、并发、持久化和可观察结果放入最相关的核心部分，不为它们机械增加独立章节。

如果消费者或触发者的业务规则、交互场景较复杂，创建独立的消费者/触发者 spec。核心 spec 保留参与者清单、它们与状态模型的关系、共享规则和摘要；独立 spec 完整拥有详细规则与场景。两份文档必须互相引用并明确各自的权威边界，避免重复维护同一规则。

### 8. 验证成稿

完成后启动一个新的 fresh-context subagent。只向它提供新建或修改的 spec、decision log、相关代码/测试/既有规范路径，要求执行 read-only artifact audit 并返回带证据出处的 findings。

要求 subagent 交叉核对：

- 没有遗漏已确认决定，也没有把未确认内容写成规范；
- 被覆盖的旧决定没有残留；
- 跨文档术语、引用和权威边界一致；
- 验收结果足以验证目标行为；
- 文档没有无意锁死实现，也没有混入 implementation plan。

主 Agent 复核 findings 后直接修正编辑性问题。若验证发现新的语义决定，停止成稿，返回 Grilling，并在重新收敛后再次取得写入授权。

最终报告生成或修改的 spec 路径，并保留 decision log。

## 边界

- 不实现功能，不修改 production code。
- 不制作 prototype。
- 不编排跨会话工作。
- 不集成 issue tracker，也不生成 ticket 或 implementation plan。
- 不使用固定 PRD 模板替代以状态与行为为中心的 spec 结构。
