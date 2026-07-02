---
name: deslop-understand
description: Build documented understanding from an explicit flow folder for later Deslop proposal work. Use only when explicitly invoked as $deslop-understand with a flow folder; do not propose, plan, or implement.
---

# Deslop Understand

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
3. Require background material from current context or this folder:

```txt
<flow-folder>/background/
```

4. If background material is not in context and `background/` is missing, tell the user and stop.
5. If validation passes, read `references/body.md` and follow it.
