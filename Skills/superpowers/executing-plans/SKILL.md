---
name: executing-plans
description: Execute an approved implementation plan serially when native subagents are unavailable, inappropriate, or the tasks are tightly coupled. Use with explicit checkpoints, test evidence, and review handoffs.
---

# Executing Plans

Use this as the honest single-agent fallback. Do not claim parallel work or independent review.

## Process

1. Read the plan and repository instructions completely.
2. Verify prerequisites, paths, dependencies, and baseline tests.
3. Raise only blockers that materially prevent execution; otherwise record assumptions and continue.
4. Execute tasks in dependency order.
5. For each task:
   - mark it in progress using the host's available tracking method;
   - stay within the declared file scope;
   - use `test-driven-development` for behavior changes;
   - use `systematic-debugging` for failures;
   - run the task's verification command;
   - record changed files, evidence, and remaining risks.
6. Run integration and final verification after all tasks.
7. Request independent review when the host can provide it; otherwise disclose that review was a self-review.

## Stop conditions

Stop and report when:

- a required artifact or permission is missing;
- the plan conflicts with current code or repository rules;
- another user's change would be overwritten;
- verification repeatedly fails without a supported new hypothesis;
- completing the next step requires external publication, deletion, merge, or another ungranted action.

Use `finishing-a-development-branch` only after verification and review are complete.
