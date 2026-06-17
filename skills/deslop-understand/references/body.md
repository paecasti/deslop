# Deslop Understand Body

## What this produces

A concise understanding dossier in `<flow-folder>/docs/` derived from user-provided material in `<flow-folder>/background/`.

## Investigation process

1. Use background material from current context when already available; otherwise read it from `background/`.
2. If the background contains contradictions or conceptual inconsistencies, report them and stop before investigating further.
3. Write concise understanding notes to:

```txt
<flow-folder>/docs/documentation.md
```

4. When explicit information is missing and an assumption is needed, record it immediately in:

```txt
<flow-folder>/docs/assumptions.md
```

5. Return a completion summary to the user that lists the documents created or updated.
6. If the user wants to refine the documented understanding, suggest running `$refine` with `documentation.md`.
7. Tell the user to review `documentation.md` first and run `$deslop-generate-acceptance-criteria` for the same flow folder only after they consider the documentation correct.

## Gotcha list

**Scope:**
- Do not infer the flow folder from the repository root when the user omits it.
- Do not continue when background material is neither in context nor available in `background/`.
- Do not read background files when their contents are already available in current context.
- Do not read background material before the validation process passes.
- Do not inspect implementation files before reading the background material.

**Behavior:**
- Do not propose, plan, implement, refactor, or select a solution.
- Stop on contradictions in background material instead of reconciling them silently.
- Update `assumptions.md` as assumptions appear during investigation, not only at the end.
- Do not request clarification during understanding; use `$refine` only when the user explicitly wants optional refinement.

**Output:**
- Keep `documentation.md` useful for a later proposal without repeating the same investigation.
- Always return a short summary of created or updated files before ending.
- Point the user to review `documentation.md` before running `$deslop-generate-acceptance-criteria`.
