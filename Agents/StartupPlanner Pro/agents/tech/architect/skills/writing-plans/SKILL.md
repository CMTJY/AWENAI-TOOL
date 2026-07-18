---
name: writing-plans
description: Convert an approved specification or clear multi-step engineering request into an executable implementation plan. Use before changing code when work spans multiple files, components, agents, migrations, or verification stages.
---

# Writing Plans

Create a plan that another engineer or agent can execute without guessing. Plan at meaningful change boundaries rather than arbitrary minute-by-minute steps.

## Inspect before planning

Read the relevant code, tests, repository instructions, and existing conventions. Do not invent file paths, APIs, commands, or dependencies.

## Plan contract

```markdown
# <Feature> Implementation Plan

## Goal
## Inputs and frozen decisions
## Non-goals
## Architecture and integration points
## File ownership map

### Task <id>: <verifiable outcome>
- Depends on:
- Files allowed:
- Files prohibited/shared:
- Changes:
- Tests first:
- Verification commands:
- Expected evidence:
- Reviewer:
- Rollback or recovery:

## Cross-task integration
## Final verification
## Open risks or approvals
```

## Rules

- Each task must produce a verifiable artifact or behavior.
- Use exact paths only after confirming they exist or are intentionally created.
- Separate tasks that can be reviewed independently; combine tightly coupled edits.
- Mark shared files, database migrations, generated files, ports, and external resources as conflict surfaces.
- Include code snippets only where an interface or fragile transformation would otherwise be ambiguous.
- Define focused tests plus the final regression command.
- Do not require commits after every micro-step.
- Do not hide unresolved decisions behind `TODO` or placeholders.

## Execution choice

- Use `subagent-driven-development` when native subagents exist and tasks can be isolated.
- Use `executing-plans` for serial execution or when subagents are unavailable.
- Use `dispatching-parallel-agents` only for tasks proven independent.

Before handoff, check requirement coverage, dependency correctness, file conflicts, reviewer independence, and verification completeness.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `tech-architect`
- Role contract: read [../../architect.md](../../architect.md) before using this skill.
- Input: the current StartupPlanner Pro Task Packet and only its required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出 technical-design 和 implementation DAG，交回 core-orchestrator；不得审核自己的架构产物。
- Evidence: return artifact locations, checks performed, failures, and known gaps to the orchestrator.
