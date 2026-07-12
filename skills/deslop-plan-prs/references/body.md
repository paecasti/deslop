# Deslop Plan PRs Body

## What this produces

A sequential PR execution plan under `<deslop-root>/plan/` with `PLAN.md`, one `context.md` per PR, and one executable `tasks.md` per PR.

## Planning process

1. Use the proposal content from context only when its recorded modification time matches the proposal file's current modification time; otherwise read the proposal file given at invocation and record its modification time.
2. Apply the same freshness check to `documentation.md`; read and record the file when context is not fresh.
3. Apply the same freshness check to `acceptance-criteria.md`; read and record the file when context is not fresh.
4. Read source project files only when needed to avoid an impossible or vague task breakdown.
5. Detect objectives, constraints, risks, dependencies, affected surfaces, and validation commands.
6. Split the work into small sequential PRs with low coupling.
7. Split each PR into atomic tasks that a simple agent can execute without broad design decisions.
8. Create the plan folder:

```txt
<deslop-root>/plan/
```

9. Write this minimum structure:

```txt
<deslop-root>/plan/
  PLAN.md
  pr-1-<slug>/
    context.md
    tasks.md
  pr-2-<slug>/
    context.md
    tasks.md
```

10. Include in `PLAN.md`:
- Overall objective.
- Reference to the source proposal this plan implements (file name under `proposals/`).
- Folder, filename, and numbering conventions.
- Ordered PR map with objective, related acceptance criteria IDs, risk, and relative complexity.

11. Include in each PR `context.md`:
- PR objective.
- Minimal background the implementing agent needs before executing tasks.
- Preconditions, when applicable.
- Frozen decisions, when applicable.
- Practical risks, when applicable.
- All execution boundaries the implementing agent must know for this PR, including any general boundaries from `PLAN.md` that affect execution.
- Human review guidance: expected final outcome, PR-level validation when available, and manual review focus.

12. Include in each PR `tasks.md`:
- Ordered atomic task sections.
- Files to read, create, and modify.
- Concrete sequential verifiable steps.
- `Check`: the concrete command, compile/build step, startup sanity check, or manual task-level check to run after the task.
- Task-specific `Do not`, only when narrower than the PR boundaries in `context.md`.

13. Review numbering, filenames, internal references, and PR order before ending.
14. Return a summary with the generated folder, number of PRs, total task count, and important assumptions.
15. Tell the user the plan is ready for implementation PR by PR.

## Gotcha list

**Input:**
- Do not browse other files under `proposals/`; the invocation always names the one proposal to plan.
- Do not use the original `<background>/` source folder to create the plan.

**Output:**
- Write real files under `<deslop-root>/plan/`; do not only answer in chat.
- Do not invent an additional parent folder under `plan/`.
- Use Markdown, kebab-case PR folder names, and lowercase `context.md` and `tasks.md` filenames.
- Do not create `README.md` files for PR context.
- Do not create one Markdown file per task.
- Do not add empty sections.

**Planning:**
- Do not modify or create implementation files in the target codebase; write only files under `<deslop-root>/plan/`.
- Preserve existing behavior unless the proposal explicitly asks for a bugfix or functional change.
- Make each PR folder executable from only its `context.md` and `tasks.md`.
- Document non-blocking assumptions briefly in the relevant plan file.
- Ask before writing files when an ambiguity blocks task decomposition.

**Tasks:**
- Keep acceptance criteria IDs in `PLAN.md`; do not repeat them in `context.md` or task sections.
- Keep `tasks.md` operational: files, steps, task-level check, and task-specific boundaries.
- Use short illustrative snippets in `tasks.md` only when they remove implementation ambiguity.
- Do not add `Done when`, `Done criterion`, or milestone sections to tasks.
- If no useful task-level check exists, write `Check: covered by PR final review`.
- Split a PR when `tasks.md` mixes unrelated responsibilities.
