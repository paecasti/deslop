---
name: deslop-generate-acceptance-criteria
description: Generate acceptance criteria from a deslop-understand documentation.md file. Use only when explicitly invoked as $deslop-generate-acceptance-criteria with a flow folder; do not implement or propose solutions.
---

# Deslop Generate Acceptance Criteria

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit flow folder path before working:

```txt
<flow-folder>
```

2. Treat the flow folder as any folder the user chooses for this Deslop run.
3. Require documentation from current context or this file:

```txt
<flow-folder>/docs/documentation.md
```

4. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the flow folder first and stop.
5. If validation passes, read `references/body.md` and follow it.
