---
name: test-driven-development
description: Implement a feature, defect fix, refactor, or behavior change through an observable failing test followed by the smallest passing change and safe refactoring. Use when behavior can be verified automatically before production code is finalized.
---

# Test-Driven Development

Use tests to define behavior and prove the test can detect its absence.

## Select the test level

Choose the lowest level that proves the requirement without coupling to implementation details:

- unit test for isolated logic;
- contract or integration test for boundaries;
- component test for UI behavior;
- end-to-end test for a critical user journey;
- focused reproduction for a defect.

Prefer real behavior. Use mocks only at slow, unreliable, destructive, or external boundaries.

## Red, green, refactor

1. **Red:** write one test for one observable behavior.
2. Run it and confirm it fails for the expected missing behavior, not a syntax, setup, or environment error.
3. **Green:** make the smallest production change that satisfies the test.
4. Run the focused test and relevant nearby tests.
5. **Refactor:** improve structure without changing behavior while tests stay green.
6. Repeat for the next behavior.

For a bug, first reproduce the original symptom. When practical, temporarily remove or neutralize the fix to prove the regression test fails, then restore it and prove it passes.

## Proportional exceptions

Do not force a fake test for:

- documentation-only changes;
- data or configuration already covered by a validator;
- generated code whose generator is tested;
- disposable exploration that will not be shipped;
- environments where an automated test is impossible and the limitation is explicit.

Use deterministic validation, static checks, or a documented manual procedure instead. Material exceptions should be visible in the task result.

## Test quality

- Assert outcomes and externally visible state, not private implementation order.
- Keep each test name specific and each failure diagnostic.
- Cover relevant boundary, error, authorization, and concurrency cases.
- Avoid arbitrary sleeps; wait on observable conditions.
- Do not change a valid expectation merely to make a failing implementation pass.
- Do not add production-only hooks solely for tests when dependency injection or a boundary fixture is sufficient.

## Evidence

Return the test path, red command/result, green command/result, regression command/result, and any untested risk. Tests passing does not replace requirement review or final verification.
