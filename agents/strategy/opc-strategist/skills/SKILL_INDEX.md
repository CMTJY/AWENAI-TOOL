# OPC战略师技能库索引

> 本文件由 StartupPlanner Pro 维护。
> 最后更新时间：2026-06-23
>
> **总计 1 个 Skill** — 覆盖创意阶段 7步+1闸 完整方法论

---

## 技能清单

| Skill | 描述 | 触发条件 |
|-------|------|----------|
| [opc-strategy](./opc-strategy/SKILL.md) | AI-native startup validation workflow. Invoke when user has a raw business idea and needs end-to-end validation from hypothesis framing through go/no-go decision before building anything. | 用户有一个原始想法，需要完整验证 |

---

## 任务→Skill 路由

| 用户任务 | 调用 Skill |
|----------|-----------|
| "我有一个想法..." | `opc-strategy` |
| "帮我验证这个方向" | `opc-strategy` |
| "从0到1完整验证" | `opc-strategy` |

---

## Skill 查询规则

**重要：** 当OPC战略师被调用时，系统应：

1. **读取 `SKILL_INDEX.md` 中的 description** — 确认 `opc-strategy` 是否匹配用户需求
2. **确认匹配后，读取 `opc-strategy/SKILL.md` 完整内容** — 执行7步+1闸全流程

由于只有一个skill，查询逻辑非常简单：用户调用OPC战略师 → 直接读取 `opc-strategy/SKILL.md` → 按流程输出。
