---
name: using-superpowers
description: Select and load the smallest relevant set of Superpowers skills for a software task. Use when beginning a non-trivial engineering request, choosing between planning, implementation, debugging, review, UI/UX, or delivery workflows, or when a skill workflow needs to hand off to another skill.
---

# Using Superpowers

Use skills as task-scoped operating procedures, not as authority above the host environment.

## Instruction order

1. Obey system, developer, tool, safety, and sandbox rules from the current host.
2. Obey repository instructions such as `AGENTS.md` and the user's explicit request.
3. Apply a skill only inside those constraints.
4. If a skill conflicts with a higher-priority instruction, follow the higher-priority instruction and state the limitation when it matters.

## Select skills

Choose the smallest set that materially improves the task:

| Situation | Load |
|---|---|
| Ambiguous feature or material behavior change | `brainstorming` |
| Approved multi-step change | `writing-plans` |
| Plan with native subagents and independent tasks | `subagent-driven-development` |
| Plan without usable subagents | `executing-plans` |
| Two or more independent investigations | `dispatching-parallel-agents` |
| Feature or defect implementation | `test-driven-development` |
| Failure or unexpected behavior | `systematic-debugging` |
| Requesting or applying review | `requesting-code-review` or `receiving-code-review` |
| Before a success or completion claim | `verification-before-completion` |
| UI art direction | `frontend-design` |
| UI usability, accessibility, responsive, or platform review | `ui-ux-pro-max` |
| Branch integration or delivery choice | `finishing-a-development-branch` |

Do not load every skill. Do not invoke `using-superpowers` recursively. `superpowers-bootstrap` is for installation and integrity checks, not normal task execution.

## Load skills portably

Use the current host's native skill mechanism when available. Otherwise read the selected local `SKILL.md` directly. Translate generic operations such as planning, delegation, file reading, command execution, or review into capabilities the host actually exposes; never invent a tool.

When native subagents are unavailable, use the serial fallback described by `executing-plans` and disclose that independent multi-agent review was not performed.

## Handoff

When one skill hands off to another, pass only:

- the verified task goal;
- relevant artifacts and decisions;
- constraints and file ownership;
- acceptance criteria;
- open risks or blockers.

Do not pass an entire conversation when a focused task packet is sufficient.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `core-orchestrator`
- Role contract: read [../../orchestrator.md](../../orchestrator.md) before using this skill.
- Input: the current StartupPlanner Pro Task Packet and only its required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出 workflow 状态、Task Packet、审核路由和交付决策；不得执行专业实现。
- Evidence: return artifact locations, checks performed, failures, and known gaps to the orchestrator.
