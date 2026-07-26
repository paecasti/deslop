# Deslop Verify Implementation Body

## What this produces

A concise verification report at `<deslop-root>/verification/implementation-verification.md` that classifies the implementation as `PASS`, `FAIL`, or `PARTIAL` against the selected proposal, documentation, and acceptance criteria.

## Verification process

1. Verify the current worktree, including committed and uncommitted changes; use another worktree only when explicitly named.
2. Read the invoked proposal, `docs/documentation.md`, and `docs/acceptance-criteria.md`. Reuse context only when its recorded modification time matches the file; otherwise read the file and record its modification time.
3. Inspect the existing unit-test tooling, commands, conventions, locations, fixtures, and mocks, and whether criteria are reachable through isolated boundaries.
4. Use unit-test mode when at least one criterion can be tested without changing source architecture, dependencies, lockfiles, or test configuration; otherwise use static-inspection mode.

## Unit-test ownership and placement

1. Organize tests by subject under test and identify the highest public boundary responsible for each behavior.
2. Map each production subject to its canonical test location and naming conventions, mirroring relative paths across separate test roots, projects, packages, or assemblies.
3. Reuse existing tests and add missing cases only to the canonical location; create a file only when existing tooling discovers it without configuration changes.
4. Form the minimum evidence set of one or more tests for each criterion; one test may support multiple criteria without duplication.
5. Ask the user before writing when the responsible subject or unit-test target remains ambiguous.

## Unit-test mode

1. Apply the ownership rules to form a complete evidence set for every criterion. If an essential part cannot be unit tested, classify the criterion as `not unit-testable`, record why, and do not inspect it statically.
2. Test observable behavior rather than implementation details unless the criterion requires them.
3. Run the narrowest command covering the evidence sets; record the command, test files used or changed, result, and a concise relevant failure excerpt.
4. Classify a criterion as `covered` when every required test passes, `failed` when any required test fails because of the implementation, or `not checked` when no required test failed but at least one could not run for an unrelated environment or dependency reason.

## Static-inspection mode

1. Inspect only reachable implementation paths needed to compare the selected proposal, documentation definitions and constraints, and every acceptance criterion.
2. Classify a criterion as `covered` only from reachable supporting code, `failed` when code contradicts or does not satisfy it, or `not checked` when evidence is insufficient.
3. For `failed` and `not checked`, include `file:line` evidence when available; never infer coverage from filenames, comments, TODOs, or declarations alone.
4. Recommend refactoring only when inspection reveals a concrete testability seam.

## Report process

1. Create `<deslop-root>/verification/` when needed and write `implementation-verification.md` using the format below.
2. Keep one row per criterion with its complete concise evidence set; separate multiple `file::test` references with semicolons.
3. Add `Findings` only for useful failure, limitation, next-action, or concrete refactoring detail; omit it and other optional lines when empty.
4. In the final user message, use: `Result: <status>. Report: <path>. Mode: <unit tests | static inspection>. Tests: <passed | failed | not run>. Coverage: <covered> covered, <failed> failed, <not checked> not checked, <not unit-testable> not unit-testable.`

## Result classification

- `PASS`: Every criterion is `covered`.
- `FAIL`: Any unit test fails because the implementation does not satisfy an acceptance criterion, or static inspection shows implementation code contradicts the proposal, documentation, or acceptance criteria.
- `PARTIAL`: At least one criterion is `not checked` or `not unit-testable`, with no failed criterion.

## Report format

```md
# Implementation Verification

Result: PASS | FAIL | PARTIAL
Mode: unit tests | static inspection
Scope: <worktree or named worktree> | <proposal file name under `proposals/`>
Tests: <passed | failed | not run> [; `<exact command>`] [; <test files used or changed>]
Reason: <include only when mode selection or inability to run tests needs explanation>

| Criterion | Status | Evidence |
|---|---|---|
| <criterion id or name> | covered | <one or more `file::test` references separated by semicolons, or `file:line` code evidence> |
| <criterion id or name> | failed \| not checked \| not unit-testable | <test references, concise reason, relevant failure excerpt, or `file:line`> |

## Findings

- <include only useful failure, limitation, next-action, or concrete refactoring detail; omit this section when there are no findings>
```

## Gotcha list

**Scope:**
- Verify only; do not fix implementation failures unless the user explicitly changes the task.
- Create or modify only the verification report and canonical unit-test files; do not modify implementation source, dependencies, lockfiles, generated artifacts, or test configuration.
- Create only `<deslop-root>/verification/` inside the Deslop root.
- Verify only against the invoked proposal, documentation, and acceptance criteria; do not use plans or browse other proposals.
- Do not include per-criterion details or evidence in the final user message.

**Testing:**
- Use existing unit-test tooling only; do not install packages or frameworks.
- Do not use browser checks, manual UI checks, live app runtime checks, network calls, databases, or external services as unit-test evidence.
