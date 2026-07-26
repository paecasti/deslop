---
name: deslop-propose
disable-model-invocation: true
description: Create one decision-ready proposal after deslop-understand has produced documentation. Use only when explicitly invoked as $deslop-propose; resolve the Deslop root from the argument or active session context and honor user proposal direction when provided.
argument-hint: "[../<deslop-root>] [idea]"
---

# Deslop Propose

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy.

## Validation process

1. Resolve `<deslop-root>` from an explicit folder argument when provided, otherwise from `active_deslop_root`; an explicit folder overrides memory, and a missing, stale, or ambiguous root must be requested before continuing.
2. Remember the normalized root as `active_deslop_root` and clear `active_proposal` when it belongs to another root.
3. Capture any extra user directive as proposal direction; if omitted, choose the best direction during analysis without asking.
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
