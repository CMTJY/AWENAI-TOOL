---
name: subagent-driven-development
description: Coordinate an approved implementation plan using native subagents, bounded task packets, and independent specification and code-quality review. Use when tasks can be isolated and the host provides real delegation; otherwise use executing-plans.
---

# Subagent-Driven Development

Keep the controller focused on state and integration. Give each worker a bounded task with explicit evidence requirements.

## Preconditions

- The implementation plan is approved and internally consistent.
- The host exposes real subagent or delegated-task capability.
- File ownership and mutable resources are known.
- Reviewers can be different from the implementer.

If these conditions do not hold, use `executing-plans`.

## Controller workflow

1. Extract the plan into task packets and a dependency graph.
2. Dispatch only tasks whose dependencies have passed review.
3. Use parallel dispatch only after the independence gate in `dispatching-parallel-agents` passes.
4. On return, verify the artifact and change scope before trusting the status.
5. Run two review gates:
   - specification compliance;
   - code quality, security, maintainability, and test quality.
6. Return defects to the original implementer with a bounded revision packet.
7. Re-run the failed review and affected verification after changes.
8. Integrate only passed artifacts, then run final verification.

## Implementer packet

```yaml
implementation_task:
  objective: verifiable outcome
  context: minimal relevant context
  required_artifacts: []
  file_scope: {allowed: [], prohibited: []}
  constraints: []
  acceptance_criteria: []
  tests_required: []
  verification_required: []
  expected_return:
    - changed_files
    - test_evidence
    - verification_evidence
    - risks_and_gaps
```

The implementer must use `test-driven-development` for behavior changes, stay inside scope, and report `complete`, `needs-context`, or `blocked`. A success statement is not evidence.

## Review packets

Specification reviewer:

```yaml
review_focus: specification-compliance
inputs: [requirements, task-packet, implementation-artifact, diff]
output: [passed-or-revision, criterion-results, defects]
```

Code-quality reviewer:

```yaml
review_focus: code-quality
inputs: [approved-spec-review, implementation-artifact, diff, tests]
checks: [correctness, security, maintainability, performance, test-quality]
output: [passed-or-revision, severity-ranked-defects]
```

Do not allow an implementer to approve its own work. Do not start code-quality review before specification review passes.

## Revision control

For every defect include severity, evidence location, required change, and re-verification command. Retry only with new information, clearer scope, a smaller task, or a more appropriate agent. Escalate architecture or requirement conflicts instead of repeating the same attempt.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `core-orchestrator`
- Role contract: read [../../orchestrator.md](../../orchestrator.md) before using this skill.
- Input: the current StartupPlanner Pro Task Packet and only its required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出 workflow 状态、Task Packet、审核路由和交付决策；不得执行专业实现。
- Evidence: return artifact locations, checks performed, failures, and known gaps to the orchestrator.
