---
name: receiving-code-review
description: Evaluate and resolve code-review feedback before changing implementation. Use when review comments are unclear, technically questionable, conflicting, multi-item, or require verified revisions and re-review.
---

# Receiving Code Review

Treat review feedback as technical input to verify, not as an instruction to accept blindly or reject defensively.

## Process

1. Read all feedback and group related items.
2. Restate each requested outcome and identify unclear or conflicting items.
3. Verify the comment against requirements, code, tests, compatibility constraints, and existing decisions.
4. Classify each item:
   - accept;
   - request clarification;
   - reject with evidence;
   - escalate because it changes scope or architecture.
5. Resolve accepted items one coherent change at a time.
6. Run focused and regression verification.
7. Return evidence and request re-review for affected gates.

## Resolution record

```yaml
review_resolution:
  review_id:
  items:
    - defect_id:
      disposition: fixed | clarified | rejected | escalated
      reasoning:
      changed_files: []
      verification: []
  remaining_items: []
```

Prioritize security and correctness blockers, then functional and maintainability issues, then minor improvements. Do not combine unrelated refactors with review fixes.

Push back when a suggestion contradicts verified requirements, breaks supported compatibility, introduces unused scope, or is disproved by code and tests. Escalate conflicts with frozen architecture or user decisions rather than silently overriding them.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `tech-mobile-dev`
- Role contract: read [../../mobile-dev.md](../../mobile-dev.md) before using this skill.
- Input: the assigned Task Packet, approved upstream artifacts, declared file scope, and acceptance criteria.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出包含平台、设备或模拟器边界的 implementation_result，交给 tech-code-reviewer。
- Evidence: include changed files, focused and regression checks, failures, and known gaps.
