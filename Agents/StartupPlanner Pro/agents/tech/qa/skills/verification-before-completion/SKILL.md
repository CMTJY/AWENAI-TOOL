---
name: verification-before-completion
description: Produce fresh evidence before claiming a task, fix, build, review, or release is complete. Use immediately before status transitions, handoffs, commits, pull requests, merges, deployments, or user-facing success claims.
---

# Verification Before Completion

Match every claim to current evidence.

## Verification gate

1. List the claims you intend to make.
2. Identify the command, inspection, or acceptance check that proves each claim.
3. Run the complete check on the current state.
4. Read the exit status and relevant output; count failures, skips, warnings, and uncovered requirements.
5. Report the actual result. If evidence does not support the claim, state the failure or limitation instead.

## Evidence matrix

| Claim | Minimum evidence |
|---|---|
| Focused behavior works | Focused automated test or reproducible manual check |
| Regression risk controlled | Relevant suite results |
| Build succeeds | Build command with successful exit |
| Static quality passes | Formatter/linter/type-check output as applicable |
| Requirements met | Criterion-by-criterion checklist with artifact locations |
| Delegated work completed | Inspect returned artifact/diff and independently run checks |
| Release is ready | Build artifact, integration tests, configuration, rollback and health checks |

One check cannot prove a different claim: a linter is not a build, unit tests are not an end-to-end path, and an agent's success message is not independent evidence.

## Evidence record

```yaml
verification:
  scope:
  checks:
    - claim:
      command_or_method:
      result: passed | failed | partial
      evidence:
  skipped_checks: []
  known_gaps: []
  conclusion: passed | failed | blocked
```

Use timestamps or environment details when results are time- or environment-sensitive. Never conceal skipped checks or pre-existing failures.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `tech-qa`
- Role contract: read [../../qa.md](../../qa.md) before using this skill.
- Input: the assigned Task Packet and only approved required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出独立 test_report 和 go/no-go/conditional 建议；缺陷退回原开发者。
- Evidence: report exact checks, artifact locations, failures, skipped checks, and residual risks.
