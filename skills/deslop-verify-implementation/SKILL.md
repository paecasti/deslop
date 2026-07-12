---
name: deslop-verify-implementation
disable-model-invocation: true
description: Verify completed Deslop implementation against one proposal, documentation, and acceptance criteria from a Deslop root. Use when explicitly invoked as $deslop-verify-implementation with a proposal file path; create unit tests when the architecture supports them, otherwise inspect code.
argument-hint: "../<deslop-root>/proposals/<idea>.md"
---

# Deslop Verify Implementation

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
3. Require the proposal content from current context or the proposal file.
4. Require access to the implementation code in the current worktree, whether its changes are committed, uncommitted, or both.
5. Require documentation from current context or `<deslop-root>/docs/documentation.md`.
6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` first and stop.
7. Require acceptance criteria from current context or `<deslop-root>/docs/acceptance-criteria.md`.
8. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to run `$deslop-generate-acceptance-criteria` first and stop.
9. If the implementation worktree or proposal is unavailable, ask for the missing source before verifying.
10. If validation passes, read `references/body.md` and follow it.
