---
name: deslop-verify-implementation
disable-model-invocation: true
description: Verify completed Deslop implementation against one proposal, documentation, and acceptance criteria from a Deslop root. Use when explicitly invoked as $deslop-verify-implementation with a proposal file path; reuse or create canonical unit tests when the architecture supports them, otherwise inspect code.
argument-hint: "../<deslop-root>/proposals/<idea>.md"
---

# Deslop Verify Implementation

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy.

## Validation process

1. Require an explicit `<deslop-root>/proposals/<idea>.md` path and treat the parent of `proposals/` as `<deslop-root>`.
2. Require the proposal content and implementation worktree; ask for either unavailable source and stop.
3. Require documentation from context or `<deslop-root>/docs/documentation.md`; if missing, tell the user to run `$deslop-understand` and stop.
4. Require acceptance criteria from context or `<deslop-root>/docs/acceptance-criteria.md`; if missing, tell the user to run `$deslop-generate-acceptance-criteria` and stop.
5. If validation passes, read `references/body.md` and follow it.
