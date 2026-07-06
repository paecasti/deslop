---
name: deslop-help
disable-model-invocation: true
description: Explain how to use the Deslop workflow in a clear fixed user-facing response. Use only when explicitly invoked as $deslop-help or when the user asks for help understanding the Deslop workflow.
---

# Deslop Help

When invoked, reply with the fixed text below. Do not inspect files, create folders, run commands, or modify the workspace.

````md
Deslop is a workflow for turning an unclear idea into an implementable and verifiable proposal, with each stage saved inside a Deslop root.

A Deslop root can be any folder you choose for one Deslop run.

Recommended structure:

```txt
<deslop-root>/
  <background>/
  docs/
  proposals/
  plan/
  issue/
  verification/
```

Example:

```txt
checkout/
  priordata/
```

Here, `checkout/priordata` is the background folder and `checkout` is the Deslop root.

Skill summary:

- `$deslop-understand`: Reads a user-specified `<background>` folder and produces `docs/documentation.md` in its parent Deslop root.
- `$deslop-generate-acceptance-criteria`: Turns the documentation into concrete acceptance criteria.
- `$deslop-brainstorm-proposals`: Generates several brief solution directions for comparison.
- `$deslop-propose`: Creates one decision-ready proposal under `proposals/`.
- `$deslop-plan-prs`: Converts a proposal into a PR-by-PR execution plan.
- `$deslop-plan-issue`: Converts a proposal into a single self-contained, commit-by-commit implementation issue draft.
- `$deslop-verify-implementation`: Checks a completed implementation against the proposal, documentation, and acceptance criteria.

Workflow diagram:

```mermaid
flowchart TD
    A["Choose any Deslop root"]
    B["Add context<br/><background>/"]
    C["$deslop-understand"]
    D["Refine<br/>docs/documentation.md"]
    E["$deslop-generate-acceptance-criteria"]
    F["Refine<br/>docs/acceptance-criteria.md"]
    G{"Need multiple<br/>solution ideas?"}
    H["$deslop-brainstorm-proposals"]
    I["$deslop-propose<br/>'idea'"]
    J["$deslop-plan-prs<br/>'proposal'"]
    M["$deslop-plan-issue<br/>'proposal'"]
    K["Implement plan"]
    L["$deslop-verify-implementation"]

    A --> B --> C --> D --> E --> F --> G
    G -- "Yes" --> H --> I
    G -- "No" --> I
    I --> J --> K
    I --> M --> K
    K --> L
```

Typical usage:

1. Create or choose any Deslop root, for example `improve-onboarding/` or `deslop/improve-onboarding/`.
2. Put the initial context in any background folder inside it, for example `priordata/`, `context/`, or `background/`.
3. Run `$deslop-understand checkout/priordata` to generate `checkout/docs/documentation.md`.
4. Review the documentation. If decisions are missing or ambiguities remain, resolve them before moving forward.
5. Run `$deslop-generate-acceptance-criteria checkout` to create `checkout/docs/acceptance-criteria.md`.
6. Optionally run `$deslop-brainstorm-proposals <deslop-root>` if you want to compare several solution ideas.
7. Run `$deslop-propose <deslop-root>` to create a concrete proposal in `proposals/`.
8. Run `$deslop-plan-prs <deslop-root>` once you have chosen a proposal and want to split the implementation into PRs. Alternatively, run `$deslop-plan-issue <deslop-root> <target-branch>` to produce a single self-contained commit-by-commit issue draft that a simpler implementing agent can execute on the branch you specify.
9. Implement by following the generated plan; no specific skill is required for this stage.
10. Use `$deslop-verify-implementation <deslop-root>` to verify a completed implementation against the proposal, documentation, and acceptance criteria.


````
