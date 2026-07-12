---
name: deslop-plan-prs
disable-model-invocation: true
description: Create a PR-by-PR execution plan from a completed Deslop proposal, documentation, and acceptance criteria. Use only when explicitly invoked as $deslop-plan-prs with a proposal file path; write files under `<deslop-root>/plan`.
argument-hint: "../<deslop-root>/proposals/<idea>.md"
---

# Deslop Plan PRs

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy.

## Validation process

1. Require an explicit proposal file path before working:

```txt
<deslop-root>/proposals/<idea>.md
```

2. Treat the parent of `proposals/` as `<deslop-root>`.
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
8. If validation passes, read `references/body.md` and follow it.
