# xuan-superpowers

我从 superpowers 工作流中得到灵感自己创建的 coding 工作流，结合 matt 的 skill 重新构建

## workflow

`grill-with-docs` -> `xuan-to-prd`

If feature is big need doc tracking -> `xuan-to-issues`

Else -> `xuan-split-tasks`

Finally -> `xuan-implement`

## User-invoked

Reachable only when you type them (`disable-model-invocation: true`).

- **[xuan-implement](./xuan-implement/SKILL.md)** — from `subagent-driven-developement`, 大幅简化
- **[xuan-to-issues](./xuan-to-issues/SKILL.md)** — from `to-issues`, 修改默认的文档路径, 不需要配置 issue tracker
- **[xuan-to-prd](./xuan-to-prd/SKILL.md)** — from `to-prd`, 修改默认的文档路径, 不需要配置 issue tracker
- **[xuan-split-tasks](./xuan-split-tasks/SKILL.md)** — from `to-issues`, 将拆分的任务写入临时目录的单一文件中

## Model-invoked

no-op
