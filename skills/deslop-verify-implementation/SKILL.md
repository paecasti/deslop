---
name: deslop-verify-implementation
disable-model-invocation: true
description: Verify completed Deslop implementation against one proposal, documentation, and acceptance criteria. Use when explicitly invoked as $deslop-verify-implementation; resolve the proposal from the argument or active session context, then reuse or create canonical unit tests when supported, otherwise inspect code.
argument-hint: "[../<deslop-root>/proposals/<idea>.md]"
---

# Deslop Verify Implementation

## Validation process

1. Resolve the proposal path from an explicit argument when provided, otherwise from `active_proposal`; explicit input overrides memory, and a missing, stale, or ambiguous proposal must be requested before continuing.
2. Require `<deslop-root>/proposals/<idea>.md`, derive its root, and remember both normalized paths as `active_proposal` and `active_deslop_root`.
3. Require the proposal content and implementation worktree; ask for either unavailable source and stop.
4. Require documentation from context or `<deslop-root>/docs/documentation.md`; if missing, tell the user to run `$deslop-understand` and stop.
5. Require acceptance criteria from context or `<deslop-root>/docs/acceptance-criteria.md`; if missing, tell the user to run `$deslop-generate-acceptance-criteria` and stop.
6. If validation passes, read `references/body.md` and follow it.
