---
name: deslop-plan-issue
disable-model-invocation: true
description: Create a self-contained commit-by-commit issue from a completed Deslop proposal. Use only when explicitly invoked as $deslop-plan-issue; resolve the proposal from the argument or active session context, require a target branch, and only write the draft under `<deslop-root>/issue`.
argument-hint: "[../<deslop-root>/proposals/<idea>.md] <target-branch>"
---

# Deslop Plan Issue

## Validation process

1. Resolve the proposal path from an explicit proposal-file argument when provided, otherwise from `active_proposal`; an explicit proposal overrides memory, and a missing, stale, or ambiguous proposal must be requested before continuing.
2. Require `<deslop-root>/proposals/<idea>.md`, derive its root, and remember both normalized paths as `active_proposal` and `active_deslop_root`.
3. Require the proposal content from current context or the proposal file.
4. Require documentation from current context or this file:

```txt
<deslop-root>/docs/documentation.md
```

5. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` first and stop.
6. Require acceptance criteria from current context or this file:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

7. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to run `$deslop-generate-acceptance-criteria` first and stop.
8. Require a target branch from the remaining invocation input; the implementing agent must do all work on that predefined branch. If absent, ask the user and stop.
9. If validation passes, read `references/body.md` and follow it.
