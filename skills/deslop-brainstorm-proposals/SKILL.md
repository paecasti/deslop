---
name: deslop-brainstorm-proposals
disable-model-invocation: true
description: Brainstorm brief solution proposal ideas from a Deslop root. Use only when explicitly invoked as $deslop-brainstorm-proposals; resolve the root from the argument or active session context and default to 5 ideas unless the user specifies a count.
argument-hint: "[../<deslop-root>] [count]"
---

# Deslop Brainstorm Proposals

## Validation process

1. Resolve `<deslop-root>` from an explicit folder argument when provided, otherwise from `active_deslop_root`; an explicit folder overrides memory, and a missing, stale, or ambiguous root must be requested before continuing.
2. Remember the normalized root as `active_deslop_root` and clear `active_proposal` when it belongs to another root.
3. Capture any user-specified proposal count from the invocation; use 5 when omitted.
4. Require documentation from current context or this file:

```txt
<deslop-root>/docs/documentation.md
```

5. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the Deslop root first and stop.
6. Require acceptance criteria from current context or this file:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

7. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to run `$deslop-generate-acceptance-criteria` first and stop.
8. If validation passes, read `references/body.md` and follow it.
