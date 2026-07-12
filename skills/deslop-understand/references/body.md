# Deslop Understand Body

## What this produces

A concise understanding dossier in `<deslop-root>/docs/` derived from user-provided material in `<background>/`, where `<deslop-root>` is the parent folder of `<background>`.

## Investigation process

1. Use background material from current context when already available; otherwise read it from `<background>/`.
2. If the background contains contradictions or conceptual inconsistencies, report them and stop before investigating further.
3. Write concise understanding notes to:

```txt
<deslop-root>/docs/documentation.md
```

4. When explicit information is missing and an assumption is needed, record it immediately in an `## Assumptions` section of `documentation.md`.
5. Record the modification time of the final `documentation.md` so later Deslop skills in the same session can detect user edits.
6. Return a completion summary to the user that lists the documents created or updated.
7. Tell the user to review `documentation.md` first and run `$deslop-generate-acceptance-criteria` for the same Deslop root only after they consider the documentation correct.

## Gotcha list

**Scope:**
- Do not inspect implementation files before reading the background material.

**Behavior:**
- Do not propose, plan, implement, refactor, or select a solution.
- Stop on contradictions in background material instead of reconciling them silently.

**Output:**
- Keep `documentation.md` useful for a later proposal without repeating the same investigation.
