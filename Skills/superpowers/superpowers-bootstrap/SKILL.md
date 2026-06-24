---
name: superpowers-bootstrap
description: Use when starting any coding task in TRAE with superpowers skills - establishes workflow, tool mapping, and which skill to invoke next
---
# Superpowers for TRAE — Bootstrap
## 概述
obra/superpowers 是一套为 AI 编程助手设计的工程化开发方法论技能集。它强制 AI 按规范流程开发：先设计、再计划、再 TDD 实现、最后审查。

本文件是 superpowers 在 TRAE 环境中的适配入口。TRAE 的 Skill 工具通过 `name` 字段引用技能，与 Claude Code 通过 `Skill` 工具加载的方式语义一致。

## 已安装的 Skills（按执行顺序）
所有 superpowers 原始 SKILL.md 文件均已下载到当前项目的 `.trae/skills/<skill-name>/SKILL.md` 中。

| 阶段 | Skill 名称 | 触发时机 |
|------|-----------|---------|
| 0. 入口 | **superpowers-bootstrap**（本文件）| 任何编码任务开始时 |
| 1. 设计 | **brainstorming** | 有新功能/组件/改动需求时 |
| 2. 分支隔离 | **using-git-worktrees** | 设计完成后，开始实现前 |
| 3. 写计划 | **writing-plans** | 设计已批准，准备写代码前 |
| 4. 执行 | **subagent-driven-development** 或 **executing-plans** | 有计划后，按任务执行 |
| 5. TDD | **test-driven-development** | 任何实现步骤中写代码前 |
| 6. 调试 | **systematic-debugging** | 遇到 bug/测试失败时 |
| 7. 代码审查 | **requesting-code-review** | 任务之间 / 提交前 |
| 8. 完成 | **finishing-a-development-branch** | 所有任务完成后 |
| 9. 验证 | **verification-before-completion** | 标记任务完成前 |
| 10. 接收审查 | **receiving-code-review** | 收到审查反馈后 |
| 11. 并行 | **dispatching-parallel-agents** | 需要并发子任务时 |
| 12. 元技能 | **writing-skills** | 创建/修改自定义 skill 时 |
| UI-A. 创意视觉 | **frontend-design** | 需要独特美学方向、视觉冲击力、"反 AI 味"时 |
| UI-B. 设计规范 | **ui-ux-pro-max** | 需要系统化设计规范、配色/字体选型、UX 准则时 |

## 工作流总览（必须严格按顺序）
```
用户需求 → brainstorming（做设计）→ using-git-worktrees（分支隔离）→ writing-plans（写计划）→ executing-plans / subagent-driven-development（执行，每步都用 TDD）→ requesting-code-review（审查）→ finishing-a-development-branch（收尾）→ verification-before-completion（验证）
```

**硬性规则：在没有完成设计（brainstorming）和写计划（writing-plans）之前，绝对不可以直接写代码。**

## TRAE 工具映射
superpowers 原文档中提到的工具在 TRAE 中对应：

| superpowers 原文 | TRAE 等价方式 |
|-----------------|---------------|
| `Skill` 工具 + `name: xxx` | 直接在对话中引用 skill 名，或使用 SKILL.md |
| `@skill-name/SKILL.md` 引用 | 使用 file:// 路径引用 `.trae/skills/<name>/SKILL.md` |
| subagent（子代理）| 使用 `general_purpose_task` 工具，将单任务描述作为独立子任务派发 |
| TodoWrite | TRAE 内置 TodoWrite 工具 |
| Claude Code /plugins 系统 | 不适用，本项目通过 `.trae/skills/` 目录提供 |

## 在 TRAE 中如何使用
### 方式 1：直接在对话中触发（推荐）
当你问 AI "做一个 XX 功能" 或"修一个 bug"时，AI 应该先加载本 bootstrap skill，然后按流程：

1. 说一句："我先用 superpowers 流程来处理。正在调用 brainstorming 做设计。"
2. 使用 `brainstorming` skill 完成设计
3. 设计通过后，使用 `writing-plans` skill 写实施计划
4. 写代码前每步都用 `test-driven-development` skill
5. 遇到 bug 用 `systematic-debugging`
6. 完成前用 `verification-before-completion` 验证

### 方式 2：单独调用某个 skill
例如：
- "用 TDD 方式实现一个 XXX" → 直接调用 `test-driven-development`
- "这个 bug 帮我按系统方式排查" → 调用 `systematic-debugging`
- "帮我写一个实施计划" → 调用 `writing-plans`

## UI/UX Skill 调用规则

本项目安装了两个 UI/UX 专项 skill，它们互补使用，**不可互相替代**。

### 何时调用 `frontend-design`（创意视觉方向）

**核心定位**：决定"长什么样"——美学方向、视觉风格、创意表达

**必须调用场景**：
- 从零创建新页面/新组件，需要确定视觉风格方向
- 用户要求"美化 UI"、"让页面更好看"、"换个风格"
- 需要避免"AI 味"（通用字体、紫色渐变、千篇一律的布局）
- 需要独特的视觉冲击力和记忆点（如像素风、复古风、赛博朋克等）
- 重构页面视觉风格（换肤、改版）

**调用时机**：在 `brainstorming` 设计阶段，当涉及视觉方向决策时，优先调用 `frontend-design` 确定美学方向。

### 何时调用 `ui-ux-pro-max`（设计规范体系）

**核心定位**：决定"怎么做对"——设计规范、配色/字体选型、UX 准则、交互标准

**必须调用场景**：
- 需要从 161 套配色方案中选择适合的调色板
- 需要字体搭配推荐（57 组字体配对）
- 需要遵循 UX 准则（无障碍、触控尺寸、动画时长等 99 条规范）
- 审查 UI 代码是否符合设计规范（间距、对比度、响应式等）
- 需要按产品类型匹配设计风格（游戏、SaaS、电商等 161 种产品类型）
- 创建或维护设计系统/组件库

**调用时机**：在确定美学方向后（`frontend-design` 之后），或在实现/审查 UI 代码时调用 `ui-ux-pro-max` 确保规范达标。

### 两者协作流程

```
视觉需求 → frontend-design（定美学方向）→ ui-ux-pro-max（确保规范达标）→ 实现
```

**典型场景示例**：

| 用户需求 | 调用顺序 |
|---------|---------|
| "美化首页" | frontend-design → ui-ux-pro-max |
| "这个页面配色不好看" | ui-ux-pro-max（选配色） |
| "让植宠页面有像素游戏的感觉" | frontend-design（定像素风方向）→ ui-ux-pro-max（确保触控/动画规范） |
| "审查 UI 代码有没有问题" | ui-ux-pro-max |
| "从零做一个新页面" | frontend-design → ui-ux-pro-max |
| "按钮太小了不好点" | ui-ux-pro-max（触控尺寸规范） |

## 重要提示
1. **Skills 是流程规范，不是建议**。如果一个 skill 说"必须先写测试再写代码"，就不能反过来。
2. **不要跳过 brainstorming**。即使你认为需求简单，也必须先做设计并让用户确认。
3. **TDD 是硬性要求**。写代码前必须先写失败的测试。如果没有测试框架，先创建测试框架。
4. **UI/UX 需求必须调用对应 skill**。涉及视觉/美化时不可跳过 `frontend-design` 或 `ui-ux-pro-max`。
5. **文件路径约定**：
   - 设计文档保存到：`docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`
   - 实施计划保存到：`docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`
6. **Git 流程**：在独立分支（或 git worktree）上开发，不在 main 分支直接写代码。

## 版本与来源
- 上游项目（工程流程）：https://github.com/obra/superpowers
- UI/UX 创意视觉：https://github.com/anthropics/skills（frontend-design）
- UI/UX 设计规范：https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- 安装方式：通过 `download-superpowers-skills.ps1` 从 raw.githubusercontent.com 拉取
- 更新方法：重新运行 `download-superpowers-skills.ps1`

## 下一步（给 AI 的提示）
如果你读到这个文件，意味着你现在处于 superpowers 工作流中。请根据用户当前需求，从以下技能中选择下一步要调用的：

- 新功能/新需求 → 调用 `brainstorming`
- 已有设计但没计划 → 调用 `writing-plans`
- 有计划准备写代码 → 调用 `executing-plans`（每步用 `test-driven-development`）
- 遇到 bug → 调用 `systematic-debugging`
- 即将完成 → 调用 `verification-before-completion`
- **美化 UI / 视觉风格 / 新页面设计** → 先调用 `frontend-design`（定美学方向），再调用 `ui-ux-pro-max`（确保规范）
- **配色/字体/UX 规范审查** → 调用 `ui-ux-pro-max`
