---
name: deslop-generate-acceptance-criteria
disable-model-invocation: true
description: Generate acceptance criteria from a deslop-understand documentation.md file. Use only when explicitly invoked as $deslop-generate-acceptance-criteria; resolve the Deslop root from the argument or active session context and do not implement or propose solutions.
argument-hint: "[../<deslop-root>]"
---

# Deslop Generate Acceptance Criteria

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy.

## Validation process

1. Resolve `<deslop-root>` from an explicit argument when provided, otherwise from `active_deslop_root`; explicit input overrides memory, and a missing, stale, or ambiguous root must be requested before continuing.
2. Remember the normalized root as `active_deslop_root` and clear `active_proposal` when it belongs to another root.
3. Require documentation from current context or this file:

```txt
<deslop-root>/docs/documentation.md
```

4. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the Deslop root first and stop.
5. If validation passes, read `references/body.md` and follow it.
