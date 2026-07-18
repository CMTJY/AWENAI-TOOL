---
name: requesting-code-review
description: Prepare and route a bounded code-review request after a coherent implementation unit or before integration. Use when an independent reviewer needs requirements, change scope, evidence, and a diff or artifact without inheriting the implementer's full conversation.
---

# Requesting Code Review

Request review with enough context to judge correctness without biasing the reviewer toward the implementer's reasoning.

## Review packet

```yaml
review_request:
  task_id:
  objective:
  requirements_or_plan:
  acceptance_criteria: []
  change_scope:
    changed_files: []
    prohibited_or_unrelated_files: []
  comparison:
    base_ref:
    head_ref:
    diff_or_artifact:
  verification_evidence: []
  known_risks: []
  requested_gates:
    - specification-compliance
    - code-quality
```

Git references are optional; use a local diff or explicit file list when commits do not exist.

## Reviewer contract

The reviewer must be independent from the implementer and return:

```yaml
review:
  status: passed | revision | failed
  gate: specification-compliance | code-quality
  criterion_results: []
  defects:
    - severity: critical | major | minor
      evidence:
      impact:
      required_change:
      recheck:
```

Run specification compliance first. Only after it passes, review correctness, security, maintainability, performance, compatibility, and test quality.

Do not ask a reviewer to implement fixes. Route defects to the original implementer, then request re-review of affected gates.
