---
name: deslop-verify-implementation
description: Verify completed Deslop implementation against one proposal, documentation, and acceptance criteria from a flow folder. Use when explicitly invoked as $deslop-verify-implementation; create unit tests when the architecture supports them, otherwise inspect code.
---

# Deslop Verify Implementation

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation Process

Run these checks before verification:

1. Require an explicit flow folder path before working:

```txt
<project>/<flows-container>/<flow-name>
```

2. Treat the flow folder as the unit of work, not the project root.
3. Require this existing Deslop folder structure:

```txt
<flow-folder>/docs/
<flow-folder>/proposals/
```

4. If the required flow folder structure is missing, tell the user which folder is missing and stop.
5. Require access to the implementation code in the current worktree, whether its changes are committed, uncommitted, or both.
6. Require exactly one proposal from current context, an explicit proposal file, or `<flow-folder>/proposals/`.
7. If `<flow-folder>/proposals/` contains more than one proposal and the user did not specify which one to use, tell the user to specify the proposal and stop.
8. Require documentation from current context or `<flow-folder>/docs/documentation.md`.
9. Require acceptance criteria from current context or `<flow-folder>/docs/acceptance-criteria.md`.
10. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to run `$deslop-generate-acceptance-criteria` first and stop.
11. If the implementation worktree, proposal, documentation, or acceptance criteria are unavailable, ask for the missing source before verifying.
12. If validation passes, read `references/body.md` and follow it.
