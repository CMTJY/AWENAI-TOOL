# Sources and licenses

This collection contains locally modified derivatives. Folder names and source locations are retained for traceability; the local workflow and platform-neutral adaptations differ from upstream.

## obra/superpowers

- Source: https://github.com/obra/superpowers
- License: MIT
- Copyright: 2025 Jesse Vincent
- Local scope: workflow, planning, testing, debugging, review, worktree, and delivery skills except the two UI skills listed below.
- License copy: `LICENSES/obra-superpowers-MIT.txt`

Local modifications include platform-neutral tool language, proportional gates, corrected verification/review ordering, self-contained task packets, and removal of unresolved local references.

## Anthropic frontend-design

- Source: https://github.com/anthropics/skills/tree/main/skills/frontend-design
- License: Apache License 2.0
- Local files: `frontend-design/`
- License copy: `frontend-design/LICENSE.txt`

`frontend-design/SKILL.md` is modified from the upstream work and carries a prominent modification notice in its body.

## Next Level Builder UI UX Pro Max

- Source: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- License: MIT
- Copyright: 2024 Next Level Builder
- Local files: `ui-ux-pro-max/`
- License copy: `ui-ux-pro-max/LICENSE.txt`

The local derivative intentionally does not bundle the upstream Python search engine or CSV database. It provides a concise, self-contained workflow and locally maintained references.

## Redistribution

When a skill is copied into another agent system, copy its complete folder, including `references/` and license files, and record the source baseline in that system's manifest.
