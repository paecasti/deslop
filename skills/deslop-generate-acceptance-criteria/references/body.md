# Deslop Generate Acceptance Criteria Body

## What this produces

A testable acceptance criteria document at `<deslop-root>/docs/acceptance-criteria.md` derived from `<deslop-root>/docs/documentation.md`.

## Analysis process

1. Use `documentation.md` content from context when already available; otherwise read the file.
2. Extract user-visible outcomes, domain rules, constraints, edge cases, and non-goals from `documentation.md`.
3. Write acceptance criteria to:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

4. Use this structure:

```md
# Acceptance Criteria

## Scope

## Criteria

### AC-001: <short outcome name>
Given <initial context>
When <action or event>
Then <observable result>

## Edge Cases

## Out of Scope
```

5. Number criteria sequentially as `AC-001`, `AC-002`, `AC-003`.
6. Keep each criterion independently testable by a human, automated test, or review checklist.
7. Return a completion summary that names `<deslop-root>/docs/acceptance-criteria.md`.
8. Tell the user to review `acceptance-criteria.md`.
9. Tell the user to run `$deslop-propose` or `$deslop-brainstorm-proposals` only after they consider `acceptance-criteria.md` correct.

## Gotcha list

**Input:**
- Do not use the original `<background>/` source folder to create acceptance criteria.
- Do not continue when documentation is neither in context nor available in `documentation.md`.
- Do not read `documentation.md` before the validation process passes.
- Do not read `documentation.md` when its contents are already available in current context.

**Criteria:**
- Do not write implementation tasks, UI copy, architecture decisions, or solution proposals as acceptance criteria.
- Do not invent behavior that is not supported by `documentation.md`.
- Do not combine unrelated behaviors in one criterion.
- Do not use vague pass conditions such as "works correctly", "is user friendly", or "handles errors well".

**Output:**
- Include `Out of Scope` when `documentation.md` states exclusions or non-goals.
- Point the user to review `acceptance-criteria.md` before running `$deslop-propose` or `$deslop-brainstorm-proposals`.
