---
name: deslop-propose
description: Create one decision-ready proposal from an explicit flow folder after deslop-understand has produced documentation. Use only when explicitly invoked as $deslop-propose with a flow folder; honor user proposal direction when provided.
---

# Deslop Propose

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit flow folder path before working:

```txt
<flow-folder>
```

2. Capture any extra user directive from the invocation as proposal direction.
3. If the user gives no proposal direction, do not ask for one; choose the best solution direction during analysis.
4. Treat the flow folder as any folder the user chooses for this Deslop run.
5. Require documentation from current context or this file:

```txt
<flow-folder>/docs/documentation.md
```

6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` for the flow folder first and stop.
7. Require acceptance criteria from current context or this file:

```txt
<flow-folder>/docs/acceptance-criteria.md
```

8. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to review `documentation.md`, run `$deslop-generate-acceptance-criteria`, and stop.
9. If validation passes, read `references/body.md` and follow it.
