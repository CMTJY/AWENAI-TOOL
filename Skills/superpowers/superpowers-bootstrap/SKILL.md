---
name: superpowers-bootstrap
description: Audit or initialize a local Superpowers collection before it is used or copied into another agent system. Use when checking installation integrity, resolving missing skills or references, establishing host capability fallbacks, or preparing a versioned skill baseline for redistribution.
---

# Superpowers Bootstrap

Prepare a complete, portable skill collection. Do not run this skill before every coding task.

## Integrity check

1. Read the collection-level `README.md` and `catalog.yaml`.
2. Confirm every catalog entry resolves to `<skill>/SKILL.md`.
3. Validate each skill's frontmatter and folder name.
4. Resolve every local reference from the skill that declares it.
5. Check third-party source and license notices in `SOURCES.md` and `LICENSES/`.
6. Record the baseline version before copying skills into another system.

Stop the copy if a required skill, reference, or license is missing.

## Host capability profile

Determine which capabilities are real in the current host:

```yaml
host_capabilities:
  local_file_read: true
  local_file_write: true
  command_execution: true
  task_tracking: true | false
  native_subagents: true | false
  parallel_subagents: true | false
  isolated_workspaces: true | false
```

Use native capabilities where present. When absent:

- task tracking → maintain a concise textual checklist;
- subagents → execute serially and label the result single-agent;
- parallel execution → derive order from dependencies;
- isolated workspace → work in place only when permitted and report the risk.

Do not require another model API, shell-launched AI CLI, or platform-specific wrapper.

## Canonical lifecycle

The lifecycle is conditional, not a mandatory chain for every task:

```text
clarify/design when needed
→ plan when multi-step
→ isolate when useful and authorized
→ implement with tests
→ verify
→ independent review
→ fix and re-verify
→ integrate or deliver with user authorization
```

Debugging may enter at any stage. UI skills apply only to interface work. Review feedback always returns to the original implementer before final verification.

## Copy boundary

When copying into another agent system:

- copy physical files; do not create symlinks or external runtime references;
- copy only role-relevant skills;
- include every referenced resource and required license;
- create a local `SKILL_INDEX.md` and source manifest;
- treat the copy as independently maintained after import.
