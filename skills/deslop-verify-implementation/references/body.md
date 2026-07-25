# Deslop Verify Implementation Body

## What this produces

A concise verification report at `<deslop-root>/verification/implementation-verification.md` that states whether the implementation is `PASS`, `FAIL`, `PARTIAL`, or `INCONCLUSIVE` against the selected proposal, documentation, and acceptance criteria.

## Verification process

1. Establish the implementation worktree to verify:
   - Use the current worktree by default.
   - Include committed and uncommitted implementation changes.
   - Use another worktree only when the user explicitly names it.
2. Read the Deslop sources of truth, using content from context only when its recorded modification time matches the file's current modification time, and otherwise reading the file and recording its modification time:
   - The proposal given at invocation.
   - Documentation from `docs/documentation.md`.
   - Acceptance criteria from `docs/acceptance-criteria.md`.
3. Inspect the project's existing test architecture:
   - Existing unit test framework, scripts, dependencies, and naming conventions.
   - Existing unit test locations, fixtures, mocks, and helper patterns.
   - Whether acceptance criteria can be exercised through isolated functions, services, modules, or components without browser, manual UI, live app runtime, network, database, or external service dependencies.
4. Use unit-test mode when the project already supports unit tests and at least one acceptance criterion can be tested without changing source architecture, dependencies, lockfiles, or test configuration.
5. Use static-inspection mode when the project lacks a usable unit test setup or the relevant behavior is not reachable through unit-testable boundaries.

## Unit-test ownership and placement

1. Organize unit tests by subject under test, not by proposal, acceptance criterion, or verification run.
2. For each unit-testable criterion, identify the public class, function, service, module, or component that owns the behavior.
3. Follow the project's existing placement convention:
   - When tests are colocated, use the canonical test file beside the production subject.
   - When tests use a separate tree, mirror the subject's path relative to its production root under the corresponding unit-test root.
   - When tests use separate projects, packages, or assemblies, select the unit-test target corresponding to the production target and mirror the relative production path inside it.
4. Use the project's canonical test filename, class, namespace, package, and suite naming conventions for that subject.
5. Before writing, inspect the canonical test file and relevant existing tests. Reuse an existing test as evidence when it already proves the criterion.
6. Add missing cases to the canonical test file. Create that file only when it does not exist and the existing test tooling will discover it without configuration changes.
7. When behavior crosses multiple collaborators, place the test at the highest public boundary responsible for that behavior; do not duplicate it in every collaborator's test file.
8. If multiple equally plausible unit-test targets or subjects remain, ask the user before writing test files.

## Unit-test mode

1. Map every acceptance criterion to `unit-testable` or `not unit-testable`.
2. For each `not unit-testable` criterion, record the reason in the report; do not attempt to verify it through static inspection or any other means.
3. For each `unit-testable` criterion, apply the ownership and placement rules, reusing existing coverage before adding a focused test case.
4. Test observable behavior required by the acceptance criteria; do not test implementation details unless the criterion requires them.
5. Run the narrowest existing unit test command that covers the selected tests.
6. Record the exact test command, test files used or changed, pass/fail result, and a concise relevant failure excerpt when tests fail.
7. Classify criteria with passing tests as `covered`.
8. Classify criteria with failing tests as `failed`.
9. Classify criteria that cannot be represented as unit tests as `not unit-testable`.
10. If the unit test command cannot run because of environment or dependency failure unrelated to the implementation, classify affected criteria as `not checked` and include the command output.

## Static-inspection mode

1. State that the architecture does not currently support useful acceptance-criteria unit tests.
2. When inspection reveals a concrete testability seam, record a concise refactoring recommendation; do not add a generic recommendation.
3. Inspect only implementation code files needed to judge conformance.
4. Compare implemented behavior and changed surfaces against the selected proposal.
5. Compare implemented behavior against documentation definitions, constraints, non-goals, and user-visible expectations.
6. Check every acceptance criterion against implementation code and classify it as `covered`, `failed`, or `not checked`.
7. Use `failed` when implementation code contradicts or does not satisfy a criterion.
8. Use `not checked` when insufficient implementation code is available to evaluate a criterion.
9. For `failed` and `not checked`, include file and line references when available.
10. Do not mark a criterion `covered` from filenames, comments, TODOs, intended architecture, or declarations without reachable implementation code paths.

## Report process

1. Create `<deslop-root>/verification/` if it does not exist.
2. Write the report to `<deslop-root>/verification/implementation-verification.md`.
3. Keep the report compact: summarize the verified worktree, proposal, mode, and test execution before the criteria table.
4. Include every acceptance criterion as one table row with its status and concise evidence.
5. Add `Findings` only when a criterion is `failed`, `not checked`, or `not unit-testable`, or when there is a concrete refactoring recommendation. Use it for useful detail or next action, not to restate table rows.
6. Omit empty sections and coverage counts that can be derived from the criteria table.
7. In the final user message, use this format: `Result: <status>. Report: <path>. Mode: <unit tests | static inspection>. Tests: <passed | failed | not run>. Coverage: <covered> covered, <failed> failed, <not checked> not checked, <not unit-testable> not unit-testable.`

## Result classification

- `PASS`: Unit-test mode has all criteria covered by passing tests, with no `failed`, `not checked`, or `not unit-testable` criteria, or static-inspection mode covers every criterion without contradiction.
- `FAIL`: Any unit test fails because the implementation does not satisfy an acceptance criterion, or static inspection shows implementation code contradicts the proposal, documentation, or acceptance criteria.
- `PARTIAL`: At least one criterion is `not checked` or `not unit-testable`, with no failed criterion.
- `INCONCLUSIVE`: Required sources, implementation code files, or verification prerequisites were unavailable.

## Report format

```md
# Implementation Verification

Result: PASS | FAIL | PARTIAL | INCONCLUSIVE
Mode: unit tests | static inspection
Scope: <worktree or named worktree> | <proposal file name under `proposals/`>
Tests: <passed | failed | not run> [; `<exact command>`] [; <test files used or changed>]
Reason: <include only when mode selection or inability to run tests needs explanation>

| Criterion | Status | Evidence |
|---|---|---|
| <criterion id or name> | covered | <test name or `file:line` code evidence> |
| <criterion id or name> | failed \| not checked \| not unit-testable | <concise reason, relevant failure excerpt, or `file:line`> |

## Findings

- <include only useful failure, limitation, next-action, or concrete refactoring detail; omit this section when there are no findings>
```

## Gotcha list

**Scope:**
- Verify only; do not fix implementation failures unless the user explicitly changes the task.
- Create or modify only verification reports and canonical unit-test files needed for acceptance-criteria verification.
- Do not modify implementation source, dependencies, lockfiles, generated artifacts, or test configuration.
- Create only `<deslop-root>/verification/` inside the Deslop root.
- Do not verify against a PR plan or task plan.
- Do not verify against any proposal other than the one given at invocation; do not browse other files under `proposals/`.
- Always record the verified proposal's file name in the report's `Scope:` line.
- Do not include per-criterion details or evidence in the final user message.
- Do not repeat coverage counts, canonical documentation paths, acceptance-criteria paths, or empty sections in the report.

**Testing:**
- Use existing unit test tooling only.
- Do not create test files named after a proposal, acceptance criterion, or verification run.
- Do not duplicate behavior across test files when an existing canonical test already proves it.
- Do not install packages or add test frameworks.
- Do not use browser checks, manual UI checks, live app runtime checks, network calls, databases, or external services as unit-test evidence.
- Do not create brittle tests that assert private implementation details when behavior can be tested.
- Do not classify an untestable criterion as failed solely because it is not unit-testable.
