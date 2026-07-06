---
name: deslop-plan-issue
disable-model-invocation: true
description: Create a single self-contained, commit-by-commit implementation issue from a completed Deslop proposal, documentation, and acceptance criteria. Use only when explicitly invoked as $deslop-plan-issue with a proposal file path; write a draft under `<deslop-root>/issue` and do not create the issue or modify implementation code.
argument-hint: "../<deslop-root>/proposals/<idea>.md <target-branch>"
---

# Deslop Plan Issue

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit proposal file path before working:

```txt
<deslop-root>/proposals/<idea>.md
```

2. Treat the parent of `proposals/` as `<deslop-root>`.
3. Require the proposal content from current context or the proposal file; do not re-read the file when its content is already in context.
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
8. Require an explicit target branch specified by the user; the implementing agent must do all the work on that predefined branch. If no branch is provided, ask the user for it and stop.
9. If validation passes, read `references/body.md` and follow it.
