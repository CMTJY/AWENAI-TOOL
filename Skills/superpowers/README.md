# Superpowers 技能集合

这是面向软件工程任务的 17 个可组合技能。集合本身是通用源包；其他 Agent 系统若要使用，应复制所需技能及其资源和许可证，并在目标系统内独立维护。

## 使用原则

- 先按 `catalog.yaml` 选择最小技能集，不要把全部技能同时加载。
- 技能服从宿主系统、仓库规则和用户授权。
- 只有真实独立的任务才并行；没有原生子 Agent 时使用串行降级。
- 所有完成、审查和交付结论都要有当前验证证据。
- `superpowers-bootstrap` 只用于集合安装、审计和复制基线，不是每个任务的入口。

## 生命周期

```text
需要时澄清与设计
→ 多步骤任务写计划
→ 需要时建立隔离工作区
→ 测试驱动实现或系统调试
→ 新鲜验证
→ 独立规格审查与代码质量审查
→ 原执行者修订并重新验证
→ 用户授权后的集成或交付
```

## 分类

| 分类 | 技能 |
|---|---|
| 入口与维护 | `using-superpowers`, `superpowers-bootstrap`, `writing-skills` |
| 设计与计划 | `brainstorming`, `writing-plans` |
| 执行与调度 | `executing-plans`, `subagent-driven-development`, `dispatching-parallel-agents` |
| 工程质量 | `test-driven-development`, `systematic-debugging`, `verification-before-completion` |
| 审查 | `requesting-code-review`, `receiving-code-review` |
| 工作区与交付 | `using-git-worktrees`, `finishing-a-development-branch` |
| UI/UX | `frontend-design`, `ui-ux-pro-max` |

## 完整性

每个技能必须满足：

1. 目录名与 frontmatter `name` 一致。
2. frontmatter 只有 `name` 和 `description`。
3. 所有本地引用存在，并随技能一起复制。
4. 第三方技能的许可证和修改声明完整。
5. `SKILL.md` 不依赖某个宿主平台的专有工具名，除非技能明确只服务该平台。

来源和许可证见 `SOURCES.md`。机器可读目录见 `catalog.yaml`。
