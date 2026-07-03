---
name: deslop-brainstorm-proposals
disable-model-invocation: true
description: Brainstorm brief solution proposal ideas from an explicit Deslop root. Use only when explicitly invoked as $deslop-brainstorm-proposals with a Deslop root; default to 5 ideas unless the user specifies a count.
argument-hint: "../<deslop-root>"
---

# Deslop Brainstorm Proposals

## Mid-tier model hierarchy

1. `sonnet-4.6`
2. `codex-5.4`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit Deslop root path before working:

```txt
<deslop-root>
```

2. Capture any user-specified proposal count from the invocation.
3. If no count is specified, use 5 proposal ideas.
4. Treat the Deslop root as any folder the user chooses for this Deslop run.
5. Require documentation from current context or this file:

```txt
<deslop-root>/docs/documentation.md
```

6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the Deslop root first and stop.
7. Require acceptance criteria from current context or this file:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

8. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to review `documentation.md`, run `$deslop-generate-acceptance-criteria`, and stop.
9. If validation passes, read `references/body.md` and follow it.
