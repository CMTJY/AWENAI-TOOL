---
name: dispatching-parallel-agents
description: Dispatch two or more genuinely independent investigations or implementation tasks through a host's native agent capability. Use only when tasks have no unresolved dependency, shared writable state, overlapping file ownership, or competing external resources.
---

# Dispatching Parallel Agents

Parallelize independent work, not merely different job titles.

## Independence gate

For every pair of candidate tasks, verify:

| Check | Required result |
|---|---|
| Data dependency | Neither consumes the other's unfinished output |
| File ownership | Writable paths do not overlap |
| Shared state | No shared database, port, device, branch, or mutable service |
| Decision dependency | Interfaces and contracts are already frozen |
| Integration | A named owner and final verification exist |

If any result fails, order the tasks sequentially or split the shared contract first.

## Task packet

Send each agent only the context it needs:

```yaml
task_packet:
  task_id: unique-id
  objective: verifiable outcome
  required_artifacts: []
  file_scope:
    allowed: []
    prohibited: []
  constraints: []
  acceptance_criteria: []
  expected_evidence: []
  reviewer: independent-agent-id
```

Do not broadcast the full conversation. Do not ask two agents to solve the same problem unless the task explicitly requires independent alternatives and a later decision gate.

## Dispatch and integrate

1. Use the host's native delegation mechanism; never launch another AI CLI through the shell.
2. Respect the host's concurrency limit.
3. Let each agent report status, artifact, changed files, evidence, and blockers.
4. Check returned changes for overlap or incompatible assumptions.
5. Run focused verification for each result.
6. Run integration verification on the combined state.
7. Route important artifacts to an independent reviewer.

If native agents are unavailable, use `executing-plans` and disclose serial execution.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `core-orchestrator`
- Role contract: read [../../orchestrator.md](../../orchestrator.md) before using this skill.
- Input: the current StartupPlanner Pro Task Packet and only its required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出 workflow 状态、Task Packet、审核路由和交付决策；不得执行专业实现。
- Evidence: return artifact locations, checks performed, failures, and known gaps to the orchestrator.
