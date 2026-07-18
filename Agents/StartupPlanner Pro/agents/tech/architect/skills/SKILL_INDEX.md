# tech-architect 本地技能索引

本目录只服务 `tech-architect`。开始任务时先读取本索引，再按触发条件完整读取 1–3 个匹配的 `SKILL.md`。禁止读取 StartupPlanner Pro 之外的 Superpowers 源目录。

| Skill | 用途 |
|---|---|
| [brainstorming](./brainstorming/SKILL.md) | 为实质性且仍有歧义的技术决策形成设计简报。 |
| [writing-plans](./writing-plans/SKILL.md) | 把技术设计转换为可执行、可审核的任务计划。 |
| [requesting-code-review](./requesting-code-review/SKILL.md) | 形成完整且无上下文污染的代码审查包。 |
| [verification-before-completion](./verification-before-completion/SKILL.md) | 所有完成、交接和交付结论前生成新鲜证据。 |
| [systematic-debugging](./systematic-debugging/SKILL.md) | 用证据、根因追踪和单一假设处理技术问题。 |

## 选择规则

- 只加载当前动作需要的技能，不把整个目录注入上下文。
- 角色文件、Task Packet 和验收标准优先约束本地技能。
- 缺少宿主能力时使用技能中声明的降级路径，不伪造委派、并行或验证。
- 本目录是独立副本；源包更新不会自动覆盖这里。
