# Deslop Verify Implementation Body

## What This Produces

A concise verification report at `<deslop-root>/verification/implementation-verification.md` that states whether the implementation is `PASS`, `FAIL`, `PARTIAL`, or `INCONCLUSIVE` against the selected proposal, documentation, and acceptance criteria.

## Verification Process

1. Establish the implementation worktree to verify:
   - Use the current worktree by default.
   - Include committed and uncommitted implementation changes.
   - Use another worktree only when the user explicitly names it.
2. Read the Deslop sources of truth:
   - The proposal given at invocation, from context when already available, otherwise read the file.
   - Documentation from context or `docs/documentation.md`.
   - Acceptance criteria from context or `docs/acceptance-criteria.md`.
3. Inspect the project's existing test architecture:
   - Existing unit test framework, scripts, dependencies, and naming conventions.
   - Existing unit test locations, fixtures, mocks, and helper patterns.
   - Whether acceptance criteria can be exercised through isolated functions, services, modules, or components without browser, manual UI, live app runtime, network, database, or external service dependencies.
4. Use unit-test mode when the project already supports unit tests and at least one acceptance criterion can be tested without changing source architecture, dependencies, lockfiles, or test configuration.
5. Use static-inspection mode when the project lacks a usable unit test setup or the relevant behavior is not reachable through unit-testable boundaries.

## Unit-Test Mode

1. Map every acceptance criterion to `unit-testable` or `not unit-testable`.
2. For each `not unit-testable` criterion, record the reason in the report.
3. Create focused unit tests for each `unit-testable` criterion using existing test framework, style, file naming, fixtures, and mocks.
4. Test observable behavior required by the acceptance criteria; do not test implementation details unless the criterion requires them.
5. Run the narrowest existing unit test command that covers the created tests.
6. Record the exact test command, generated test files, pass/fail result, and relevant failure output.
7. Classify criteria with passing tests as `covered`.
8. Classify criteria with failing tests as `failed`.
9. Classify criteria that cannot be represented as unit tests as `not unit-testable`.
10. If the unit test command cannot run because of environment or dependency failure unrelated to the implementation, classify affected criteria as `not checked` and include the command output.

## Static-Inspection Mode

1. State that the architecture does not currently support useful acceptance-criteria unit tests.
2. Recommend refactoring the application to expose testable units before future verification.
3. Inspect only implementation code files needed to judge conformance.
4. Compare implemented behavior and changed surfaces against the selected proposal.
5. Compare implemented behavior against documentation definitions, constraints, non-goals, and user-visible expectations.
6. Check every acceptance criterion against implementation code and classify it as `covered`, `failed`, or `not checked`.
7. Use `failed` when implementation code contradicts or does not satisfy a criterion.
8. Use `not checked` when insufficient implementation code is available to evaluate a criterion.
9. For `failed` and `not checked`, include file and line references when available.
10. Do not mark a criterion `covered` from filenames, comments, TODOs, intended architecture, or declarations without reachable implementation code paths.

## Report Process

1. Create `<deslop-root>/verification/` if it does not exist.
2. Write the report to `<deslop-root>/verification/implementation-verification.md`.
3. Include every acceptance criterion status.
4. Include evidence for criteria that are `failed`, `not checked`, or `not unit-testable`.
5. Include the refactoring recommendation when static-inspection mode is used.
6. In the final user message, use this format: `Result: <status>. Report: <path>. Mode: <unit tests | static inspection>. Tests: <passed | failed | not run>. Coverage: <covered> covered, <failed> failed, <not checked> not checked, <not unit-testable> not unit-testable.`

## Result Classification

- `PASS`: Unit-test mode has all unit-testable criteria passing and no failed or not checked criteria, or static-inspection mode covers every criterion without contradiction.
- `FAIL`: Any unit test fails because the implementation does not satisfy an acceptance criterion, or static inspection shows implementation code contradicts the proposal, documentation, or acceptance criteria.
- `PARTIAL`: At least one criterion is `not checked` or `not unit-testable`, with no failed criterion.
- `INCONCLUSIVE`: Required sources, implementation code files, or verification prerequisites were unavailable.

## Report Format

```md
Result: PASS | FAIL | PARTIAL | INCONCLUSIVE
Mode: unit tests | static inspection

Verified:
- Implementation: <worktree or named worktree>
- Proposal: <proposal file name under `proposals/`>
- Documentation: <documentation source>
- Acceptance criteria: <acceptance criteria source>

Unit Test Feasibility:
- Decision: usable | unavailable | partially usable
- Reason: <why this mode was selected>
- Refactoring recommendation: <recommendation when unit tests are unavailable, otherwise "None">

Tests:
- Command: <command or "Not run">
- Result: passed | failed | not run
- Test files: <created test files or "None">

Acceptance Criteria Coverage:
- covered: <count>
- failed: <count>
- not checked: <count>
- not unit-testable: <count>

Acceptance Criteria:
- <criterion id or name>: covered
  Evidence: <test name or code evidence>
- <criterion id or name>: failed | not checked | not unit-testable
  Evidence: <why this is not covered; include test output or file:line when available>

Unverified:
- <unverified area or "None">
```

## Gotcha List

**Scope:**
- Verify only; do not fix implementation failures unless the user explicitly changes the task.
- Create only verification reports and focused unit test files needed for acceptance-criteria verification.
- Do not modify implementation source, dependencies, lockfiles, generated artifacts, or test configuration.
- Create only `<deslop-root>/verification/` inside the Deslop root; missing `docs/` is a validation failure.
- Do not verify against a PR plan or task plan.
- Do not verify against any proposal other than the one given at invocation; do not browse other files under `proposals/`.
- Always record the verified proposal's file name in the report's `Verified:` section.
- Do not include per-criterion details or evidence in the final user message.

**Testing:**
- Use existing unit test tooling only.
- Do not install packages or add test frameworks.
- Do not use browser checks, manual UI checks, live app runtime checks, network calls, databases, or external services as unit-test evidence.
- Do not create brittle tests that assert private implementation details when behavior can be tested.
- Do not classify an untestable criterion as failed solely because it is not unit-testable.
