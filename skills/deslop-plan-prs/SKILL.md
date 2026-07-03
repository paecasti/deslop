---
name: deslop-plan-prs
disable-model-invocation: true
description: Create a PR-by-PR execution plan from a completed Deslop proposal, documentation, and acceptance criteria. Use only when explicitly invoked as $deslop-plan-prs with a Deslop root; write files under `<deslop-root>/plan`.
argument-hint: "../<deslop-root>/<propose>"
---

# Deslop Plan PRs

## Mid-tier model hierarchy

1. `codex-5.4`
2. `sonnet-4.6`

Use the first available model in the recommended mid-tier hierarchy, and define separate hierarchies for other tiers when available.

## Validation process

1. Require an explicit Deslop root path before working:

```txt
<deslop-root>
```

2. Treat the Deslop root as any folder the user chooses for this Deslop run.
3. Require a completed proposal from current context or an explicit proposal file under:

```txt
<deslop-root>/proposals/
```

4. If no completed proposal is in context and no explicit proposal file is provided, ask the user which proposal to plan and stop.
5. Require documentation from current context or this file:

```txt
<deslop-root>/docs/documentation.md
```

6. If documentation is not in context and `documentation.md` is missing, tell the user to run `$deslop-understand` first and stop.
7. Require acceptance criteria from current context or this file:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

8. If acceptance criteria are not in context and `acceptance-criteria.md` is missing, tell the user to run `$deslop-generate-acceptance-criteria` first and stop.
9. If validation passes, read `references/body.md` and follow it.
