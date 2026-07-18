# StartupPlanner Pro 文档导航

本目录集中保存面向维护者和使用者的说明。角色运行规则仍以项目根目录 `AGENTS.md`、角色文件和配置 YAML 为准。

## 核心入口

| 文档 | 用途 |
|---|---|
| [项目总览](../README.md) | 项目定位、使用方式、目录和关键约束 |
| [运行协议](../AGENTS.md) | AI Agent 必须遵循的调度、委派、审核与降级规则 |
| [部门与角色](departments.md) | 所有部门、角色 ID、文件位置和职责边界 |
| [协作规范](methodology/agent-collaboration.md) | Task Packet、Artifact、状态机、文件隔离和质量门禁 |
| [方向发现门](methodology/direction-discovery.md) | 开放式创业 / BP 请求的重大歧义扫描、用户确认和放行规则 |
| [工作流模板说明](../agents/templates/README.md) | 工作流 DAG 的格式、约束和维护规则 |

## 方法论

- [创业阶段](methodology/startup-phases.md)
- [商业计划书写作指南](methodology/bp-writing-guide.md)
- [智能体协作规范](methodology/agent-collaboration.md)
- [方向发现与用户确认门](methodology/direction-discovery.md)

## 交付模板

- [商业计划书模板](templates/bp-template.md)
- [财务模型模板](templates/financial-model-template.md)
- [市场报告模板](templates/market-report-template.md)
- [路线图模板](templates/roadmap-template.md)

## 文档放置规则

- 项目根 `README.md` 只做面向用户的总览和入口。
- 项目根 `AGENTS.md` 只做运行时协议，不承载介绍性内容。
- 部门说明统一维护在 `docs/departments.md`，不在各部门目录重复创建 README。
- `agents/templates/README.md` 是唯一保留在运行目录中的局部 README，用于解释紧邻的工作流 YAML。
- 角色自己的能力、输入输出和边界写在角色 Markdown；技能说明写在角色的 `skills/SKILL_INDEX.md`。
