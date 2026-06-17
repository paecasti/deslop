# Deslop Verify Implementation Body

## What This Produces

A concise code-inspection report file that states whether the implementation is `PASS`, `FAIL`, `PARTIAL`, or `INCONCLUSIVE` against the selected proposal, documentation, and acceptance criteria.

## Verification Process

1. Establish the implementation worktree to verify:
   - Use the current worktree by default.
   - Include committed and uncommitted implementation changes.
   - Use another worktree only when the user explicitly names it.
2. Read the Deslop sources of truth:
   - Exactly one selected proposal.
   - Documentation from context or `docs/documentation.md`.
   - Acceptance criteria from context or `docs/acceptance-criteria.md`.
3. Inspect only implementation code files needed to judge conformance.
4. Compare implemented behavior and changed surfaces against the selected proposal.
5. Compare implemented behavior against documentation definitions, constraints, non-goals, and user-visible expectations.
6. Check every acceptance criterion against implementation code and classify it as `covered`, `failed`, or `not checked`.
7. Use `failed` when implementation code contradicts or does not satisfy a criterion.
8. Use `not checked` when insufficient implementation code is available to evaluate a criterion.
9. For `failed` and `not checked`, include file and line references when available.
10. Do not mark a criterion `covered` from filenames, comments, TODOs, intended architecture, or declarations without reachable implementation code paths.
11. Do not use build, lint, test, browser, app-runtime, or manual UI evidence to classify acceptance criteria.
12. Create `<flow-folder>/verification/` if it does not exist.
13. Write the report to `<flow-folder>/verification/implementation-verification.md`.
14. In the report file, include every acceptance criterion status; include evidence only for criteria that are not `covered`.
15. In the final user message, use this format: `Result: <status>. Report: <path>. Coverage: <covered> covered, <failed> failed, <not checked> not checked.`
16. Do not modify source, tests, dependencies, lockfiles, generated artifacts, or configuration.

## Result Classification

- `PASS`: Implementation code conforms to the selected proposal, documentation, and acceptance criteria.
- `FAIL`: Implementation code contradicts the proposal or documentation, or fails a required acceptance criterion.
- `PARTIAL`: Some relevant code paths or acceptance criteria were not checked.
- `INCONCLUSIVE`: Required sources or implementation code files were unavailable.

## Report Format

```md
Result: PASS | FAIL | PARTIAL | INCONCLUSIVE

Verified:
- Implementation: <worktree or named worktree>
- Proposal: <proposal file or identifier>
- Documentation: <documentation source>
- Acceptance criteria: <acceptance criteria source>

Acceptance Criteria Coverage:
- covered: <count>
- failed: <count>
- not checked: <count>

Acceptance Criteria:
- <criterion id or name>: covered
- <criterion id or name>: failed | not checked
  Evidence: <why this is not covered; include file:line when available>

Unverified:
- <unverified area or "None">
```

## Gotcha List

**Scope:**
- Verify only; do not fix failures unless the user explicitly changes the task.
- Verify by code inspection only.
- Create only `<flow-folder>/verification/`; missing `docs/` or `proposals/` is a validation failure.
- Do not verify against a PR plan or task plan.
- Do not verify against an unselected proposal.
- Do not include evidence for `covered` criteria.
- Do not include per-criterion details or evidence in the final user message.
- Do not run or rely on compile, build, lint, tests, browser checks, app-runtime checks, or manual UI checks.
