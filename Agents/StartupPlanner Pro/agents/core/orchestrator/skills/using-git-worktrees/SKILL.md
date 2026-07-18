---
name: using-git-worktrees
description: Create or verify an isolated Git workspace for feature work when isolation is useful, authorized, and supported by the host. Use before risky or concurrent implementation; skip when already isolated, outside Git, or the user requires work in place.
---

# Using Git Worktrees

Prefer existing host-managed isolation. Never create or remove a worktree the host owns without explicit support.

## Decide

1. Confirm the directory is a Git repository.
2. Detect whether the current checkout is already a linked or host-managed worktree.
3. Check repository instructions and the user's preference.
4. Ask before creating a new worktree unless authorization is already explicit.
5. If isolation is unnecessary or unavailable, work in place and report that choice.

## Native-first creation

Use the host's native worktree capability when available. Otherwise use `git worktree` from the repository's main checkout.

Before a project-local worktree is created:

- choose a resolved path under `.worktrees/` or the repository's documented location;
- verify that location is ignored by Git;
- use a dedicated branch name;
- do not modify `.gitignore` or commit solely for setup without authorization.

Example Git fallback:

```text
git worktree add <resolved-worktree-path> -b <branch-name>
```

Use the shell syntax appropriate to the current operating system; do not copy POSIX commands into PowerShell unchanged.

## Baseline

In the isolated workspace:

1. Inspect project instructions before installing dependencies.
2. Use the repository's documented setup command.
3. Run a focused clean-baseline test or validation.
4. Report the absolute workspace path, branch state, and baseline result.

Do not automatically install packages merely because a manifest exists.

## Ownership and cleanup

Record whether the worktree is `host-owned`, `project-owned`, or `user-owned`. Only `project-owned` worktrees created in this workflow may be removed by the corresponding delivery workflow, and only after verifying the exact path and receiving required confirmation.

## StartupPlanner Pro Integration

This is an independently maintained local copy imported from baseline `superpowers-portable-2026-07-18`.

- Local owner: `core-orchestrator`
- Role contract: read [../../orchestrator.md](../../orchestrator.md) before using this skill.
- Input: the current StartupPlanner Pro Task Packet and only its required artifacts.
- Boundary: never read or depend on the repository-level `Skills/superpowers` source at runtime.
- Handoff: 输出 workflow 状态、Task Packet、审核路由和交付决策；不得执行专业实现。
- Evidence: return artifact locations, checks performed, failures, and known gaps to the orchestrator.
