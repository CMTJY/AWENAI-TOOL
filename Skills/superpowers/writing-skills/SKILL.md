---
name: writing-skills
description: Create, revise, or validate an agent skill with clear triggers, concise procedures, progressive disclosure, complete local references, and realistic usage checks. Use for SKILL.md authoring and skill-library maintenance, not ordinary product implementation.
---

# Writing Skills

Write a compact operating guide for another capable agent. Include only knowledge and procedure that materially improve execution.

## Understand the use

Define concrete trigger examples, non-trigger examples, expected outputs, common failure modes, and the degree of freedom appropriate to the task.

## Design the bundle

```text
skill-name/
├── SKILL.md
├── references/   # detailed knowledge loaded only when needed
├── scripts/      # deterministic reusable operations
└── assets/       # files copied or transformed into outputs
```

Create only resources the workflow actually needs. Do not add per-skill README, changelog, installation guide, or duplicate quick reference.

## Write SKILL.md

- Use a folder and `name` containing lowercase letters, digits, and hyphens.
- Put only `name` and `description` in YAML frontmatter.
- Make the description state capability and concrete trigger contexts.
- Use imperative instructions in the body.
- Keep the core workflow concise and preferably under 500 lines.
- Move variants, long tables, schemas, and examples to one-level-deep references.
- Link every resource directly from `SKILL.md` and state when to load it.
- Do not reference files, skills, tools, or paths that do not exist in the target system.
- Describe generic operations unless the skill is intentionally platform-specific.

## Validate behavior

1. Run the repository's skill validator on the folder.
2. Check frontmatter, folder/name equality, UTF-8 readability, and every local link.
3. Test at least one expected trigger, one non-trigger, and one pressure or edge case.
4. Verify the agent follows the procedure without hidden context or unavailable tools.
5. Remove redundant explanation and close only failure modes observed or strongly implied by the domain.

For a modified third-party skill, retain its required license and attribution and mark the file as changed.

## Review checklist

- The description routes correctly.
- The body contains no higher-priority instruction claims.
- Required inputs, outputs, stop conditions, and verification are explicit.
- The skill degrades honestly when an optional capability is absent.
- References are complete, local, and non-duplicative.
- Examples are short, correct, and adaptable.
- The target agent can use the skill without depending on another repository unless that dependency is intentional and documented.
