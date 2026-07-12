# Deslop Understand Body

## What this produces

A concise understanding document at `<deslop-root>/docs/documentation.md` derived from user-provided material in `<background>/`, where `<deslop-root>` is the parent folder of `<background>`.

## Investigation process

1. Read the background material from `<background>/`, complementing it with any background material already in context.
2. If the background contains contradictions or conceptual inconsistencies, report them and stop before investigating further.
3. Inspect the implementation files relevant to the problem, including those referenced by the background material, to ground the documentation in the actual project.
4. Write concise understanding notes to:

```txt
<deslop-root>/docs/documentation.md
```

5. When explicit information is missing and an assumption is needed, record it immediately in an `## Assumptions` section of `documentation.md`.
6. Record the modification time of the final `documentation.md` so later Deslop skills in the same session can detect user edits.
7. Return a completion summary that names `<deslop-root>/docs/documentation.md`.
8. Tell the user to review `documentation.md` first and run `$deslop-generate-acceptance-criteria` for the same Deslop root only after they consider the documentation correct.

## Gotcha list

**Scope:**
- Do not inspect implementation files before reading the background material.

**Behavior:**
- Do not propose, plan, implement, refactor, or select a solution.
- Stop on contradictions in background material instead of reconciling them silently.

**Output:**
- Keep `documentation.md` useful for a later proposal without repeating the same investigation.
