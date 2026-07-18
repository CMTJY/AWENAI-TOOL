---
name: systematic-debugging
description: Diagnose a bug, test failure, build error, performance problem, integration issue, or unexpected behavior before proposing a fix. Use when the cause is not already proven by direct evidence.
---

# Systematic Debugging

Find and verify the root cause before implementing a remedy.

## 1. Establish the failure

- Read the complete error, stack, logs, and failing assertion.
- Record the smallest reliable reproduction and expected behavior.
- Separate deterministic failures from intermittent or environment-specific failures.
- Inspect recent relevant changes and configuration without assuming causality.

If the failure cannot be reproduced, improve observation instead of guessing.

## 2. Trace evidence

Trace the failing value, event, or state backward across each boundary:

```text
observed symptom
← component output
← component input
← caller or producer
← first point where actual diverges from expected
```

For multi-component systems, capture inputs, outputs, configuration, timing, and correlation identifiers at boundaries. Do not log secrets or sensitive personal data.

Compare the broken path with a similar working path and list meaningful differences.

## 3. Test one hypothesis

State:

```text
Hypothesis: <specific cause>
Evidence: <observations supporting it>
Disproof test: <smallest test that could prove it wrong>
```

Change one variable or add one diagnostic at a time. If disproved, remove speculative changes and form a new hypothesis.

## 4. Fix and prove

1. Add the smallest automated reproduction when feasible.
2. Use `test-driven-development` to implement a root-cause fix.
3. Run the focused reproduction, relevant regression suite, and original user path.
4. Remove temporary diagnostics unless they provide safe ongoing observability.
5. Document the cause, fix, evidence, and remaining uncertainty.

## Escalation

After repeated unsupported fixes or when each attempt exposes deeper coupling, stop changing code. Reassess the architecture, task scope, environmental assumptions, and ownership with the user or technical lead. Repeating the same attempt with no new evidence is not progress.
