---
name: deslop-generate-acceptance-criteria
disable-model-invocation: true
description: Generate acceptance criteria from a deslop-understand documentation.md file. Use only when explicitly invoked as $deslop-generate-acceptance-criteria with a Deslop root; do not implement or propose solutions.
argument-hint: "../<deslop-root>"
---

# Deslop Generate Acceptance Criteria

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy.

## Validation process

1. Require an explicit Deslop root path before working:

```txt
<deslop-root>
```

2. Treat the Deslop root as any folder the user chooses for this Deslop run.
3. Require documentation from current context or this file:

```txt
<deslop-root>/docs/documentation.md
```

4. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the Deslop root first and stop.
5. If validation passes, read `references/body.md` and follow it.
