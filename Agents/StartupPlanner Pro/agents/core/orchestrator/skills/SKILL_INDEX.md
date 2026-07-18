# core-orchestrator 本地技能索引

本目录只服务 `core-orchestrator`。开始任务时先读取本索引，再按触发条件完整读取 1–3 个匹配的 `SKILL.md`。禁止读取 StartupPlanner Pro 之外的 Superpowers 源目录。

| Skill | 用途 |
|---|---|
| [brainstorming](./brainstorming/SKILL.md) | 当创业方向、目标用户、市场、产品形态或其他重大决策仍有歧义时，先形成经用户确认的方向简报。 |
| [superpowers-bootstrap](./superpowers-bootstrap/SKILL.md) | 检查本地技能集合完整性与宿主能力，只用于安装、审计和导入。 |
| [using-superpowers](./using-superpowers/SKILL.md) | 选择当前任务所需的最小技能集。 |
| [dispatching-parallel-agents](./dispatching-parallel-agents/SKILL.md) | 仅在任务无依赖、无共享可写状态时并行派发。 |
| [subagent-driven-development](./subagent-driven-development/SKILL.md) | 用 Task Packet、独立审核和返工闭环调度真实子 Agent。 |
| [executing-plans](./executing-plans/SKILL.md) | 没有真实子 Agent 时按计划串行执行。 |
| [using-git-worktrees](./using-git-worktrees/SKILL.md) | 在授权且有价值时建立或识别隔离工作区。 |
| [finishing-a-development-branch](./finishing-a-development-branch/SKILL.md) | 在验证与审核通过后安全处理分支交付选择。 |
| [verification-before-completion](./verification-before-completion/SKILL.md) | 所有完成、交接和交付结论前生成新鲜证据。 |

## 选择规则

- 只加载当前动作需要的技能，不把整个目录注入上下文。
- 重大方向缺失时必须先加载 `brainstorming`；方向门未通过前不得加载领域执行技能或派发下游任务。
- 角色文件、Task Packet 和验收标准优先约束本地技能。
- 缺少宿主能力时使用技能中声明的降级路径，不伪造委派、并行或验证。
- 本目录是独立副本；源包更新不会自动覆盖这里。
