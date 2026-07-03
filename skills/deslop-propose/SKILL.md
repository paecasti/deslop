---
name: deslop-propose
disable-model-invocation: true
description: Create one decision-ready proposal from an explicit Deslop root after deslop-understand has produced documentation. Use only when explicitly invoked as $deslop-propose with a Deslop root; honor user proposal direction when provided.
argument-hint: "../<deslop-root> (optional)<idea>"
---

# Deslop Propose

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit Deslop root path before working:

```txt
<deslop-root>
```

2. Capture any extra user directive from the invocation as proposal direction.
3. If the user gives no proposal direction, do not ask for one; choose the best solution direction during analysis.
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
