# Deslop Generate Acceptance Criteria Body

## What this produces

A testable acceptance criteria document at `<deslop-root>/docs/acceptance-criteria.md` derived from `<deslop-root>/docs/documentation.md`.

## Analysis process

1. Use `documentation.md` content from context only when its recorded modification time matches the file's current modification time; otherwise read the file and record its modification time.
2. Extract user-visible outcomes, domain rules, constraints, edge cases, and non-goals from `documentation.md`.
3. Write acceptance criteria to:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

4. Use this structure, omitting `Edge Cases` and `Out of Scope` when `documentation.md` gives them no content:

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
7. Record the modification time of the written `acceptance-criteria.md` so later Deslop skills in the same session can detect user edits.
8. Return a completion summary that names `<deslop-root>/docs/acceptance-criteria.md`.
9. Tell the user to review `acceptance-criteria.md`.
10. Tell the user to run `$deslop-propose` or `$deslop-brainstorm-proposals` only after they consider `acceptance-criteria.md` correct.

## Gotcha list

**Input:**
- Do not use the original `<background>/` source folder to create acceptance criteria.

**Criteria:**
- Do not write implementation tasks, UI copy, architecture decisions, or solution proposals as acceptance criteria.
- Do not invent behavior that is not supported by `documentation.md`.
- Do not combine unrelated behaviors in one criterion.
- Do not use vague pass conditions such as "works correctly", "is user friendly", or "handles errors well".
