---
name: deslop-understand
disable-model-invocation: true
description: Build documented understanding from an explicit background folder, deriving the Deslop root from its parent. Use only when explicitly invoked as $deslop-understand with a background folder; do not propose, plan, or implement.
---

# Deslop Understand

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit background folder path before working:

```txt
<background>
```

2. Treat `<background>` as any folder the user chooses for source material.
3. Derive `<deslop-root>` as the parent folder of `<background>`.
4. Require background material from current context or this folder:

```txt
<background>/
```

5. If background material is not in context and `<background>/` is missing, tell the user and stop.
6. If validation passes, read `references/body.md` and follow it.
