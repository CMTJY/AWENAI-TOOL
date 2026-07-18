---
name: brainstorming
description: Turn an ambiguous feature, product behavior, architecture change, or UI concept into an approved design brief before implementation. Use when material requirements or trade-offs are unresolved; skip for mechanical edits with clear acceptance criteria.
---

# Brainstorming

Resolve decisions that would otherwise cause rework. Keep the conversation proportional to the change.

## Decide the depth

| Change | Approach |
|---|---|
| Typo, rename, mechanical configuration | Confirm scope and proceed |
| Local behavior with clear acceptance criteria | Produce a short design note |
| New feature, architecture, workflow, or ambiguous UI | Run the full process |

## Process

1. Inspect the existing project, constraints, and related patterns.
2. State the problem, users, desired outcome, non-goals, and unresolved decisions.
3. Ask only questions whose answers materially change the design; ask one focused question at a time when interaction is required.
4. Present two or three viable approaches with trade-offs and a recommendation. A recommendation remains `proposed`; it is not the user's selection.
5. Produce a design brief and request approval only for material decisions. For startup, business-plan, product-direction, target-market, or other irreversible scope choices, keep the state at `awaiting-confirmation` until the user selects an option or explicitly delegates the choice.

## Design brief

```markdown
# Design Brief: <topic>

## Goal and success criteria
## Current context and constraints
## In scope / out of scope
## Chosen approach and alternatives rejected
## Components, interfaces, and data flow
## Failure states, security, and operational risks
## Test and verification strategy
## Open decisions requiring approval
```

Save the brief only when the project or user requests a persistent artifact. Do not commit files, create branches, or start implementation without authorization.

## Exit criteria

Proceed to `writing-plans` when:

- material decisions are resolved by the user, or are covered by explicit bounded/full delegation with recorded evidence;
- the chosen design fits existing project conventions;
- success criteria are testable;
- risks and non-goals are visible.

Do not close a startup or business-plan direction decision merely by recording it as an assumption. A recommended option must remain `proposed` or `awaiting-confirmation` unless `selection_authority` is `bounded` or `full`; `full` direct selection also requires the user to say that no second confirmation is needed.

If the task is now small and direct, implementation may proceed without a separate plan.
