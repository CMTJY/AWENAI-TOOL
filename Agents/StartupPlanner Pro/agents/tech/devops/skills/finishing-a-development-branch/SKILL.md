---
name: finishing-a-development-branch
description: Close verified and reviewed development work by presenting safe integration or preservation choices. Use when tests and required reviews have passed and the user must choose whether to keep, merge, publish, or discard a branch or workspace.
---

# Finishing a Development Branch

This skill guides a decision; it does not grant authority to merge, push, publish, delete, or discard work.

## Preconditions

1. Run `verification-before-completion` with fresh evidence.
2. Confirm required specification and code-quality reviews passed.
3. Inspect Git status, current branch, upstream, base branch, commits, and worktree ownership.
4. Report uncommitted or unrelated changes before presenting integration choices.

Do not proceed while required tests or reviews fail.

## Present context-aware choices

Offer only choices supported by the current environment, such as:

- keep the branch and workspace unchanged;
- create a local commit when authorized;
- push and open a pull request when explicitly requested and credentials exist;
- merge locally when explicitly requested and safe;
- discard only after showing the exact branch, commits, files, and workspace affected.

Do not force a fixed menu when an option is impossible or outside scope.

## Execute safely

- Re-check the exact target immediately before any destructive action.
- Require explicit confirmation for discard, force-delete, overwrite, or cleanup.
- Never force-push unless the user explicitly asks.
- After a merge, run verification on the merged state before deleting a branch.
- Preserve worktrees needed for pull-request revisions.
- Remove only a worktree recorded as project-owned by `using-git-worktrees`.
- Use native host controls when the host manages branches or worktrees.

## Completion record

Report:

```yaml
delivery:
  branch:
  base_branch:
  action_taken:
  commit_or_pr:
  verification_evidence:
  workspace_preserved: true | false
  cleanup_performed: []
  remaining_user_actions: []
```

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `tech-devops`
- Role contract: read [../../devops.md](../../devops.md) before using this skill.
- Input: the assigned Task Packet and only approved required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出 delivery_artifact；生产动作、合并、推送或清理仍需用户或 orchestrator 授权。
- Evidence: report exact checks, artifact locations, failures, skipped checks, and residual risks.
