# Deslop Plan Issue Body

## What this produces

A single self-contained draft issue at `<deslop-root>/issue/ISSUE.md` that divides the implementation into ordered commits, embedding everything a separate simpler implementing agent needs to execute it without opening the Deslop files.

## Planning process

1. Use the proposal content from context when already available; otherwise read the proposal file given at invocation.
2. Use `documentation.md` content from context when already available; otherwise read the file.
3. Use `acceptance-criteria.md` content from context when already available; otherwise read the file.
4. Read source project files only when needed to avoid an impossible or vague commit breakdown.
5. Detect objectives, constraints, risks, dependencies, affected surfaces, and validation commands.
6. Split the work into the fewest ordered commits that keep the plan coherent; each commit is one logical, independently reviewable change, not one commit per file or per trivial step.
7. Prefer merging closely related work into a single commit over adding more commits; only split when a commit would mix unrelated responsibilities or force a design decision on the executor.
8. Keep each commit's steps concise: give the executor enough to act without ambiguity, and trust its judgment for routine mechanical details instead of scripting every line.
9. Create the issue folder:

```txt
<deslop-root>/issue/
```

10. Write a single `ISSUE.md` with this content:
- **Title**: imperative and concise.
- **Objective / summary**: self-contained, from the proposal.
- **Target branch**: the predefined branch the user specified at invocation; state clearly that the implementing agent must do all the work and all commits on this branch and must not commit to any other branch.
- **Context for the implementer**: the minimal background, frozen decisions, and constraints needed to implement without opening the Deslop files. Embed the information inline; do not reference it by file path or ID.
- **Global execution boundaries**: the `Do not` rules that apply to every commit, including working only on the target branch.
- **Commit plan**: an ordered list of commit sections. Each commit section contains:
  - Suggested commit message/title.
  - Goal of the commit.
  - Files to read, create, and modify.
  - Concrete sequential steps.
  - `Check`: the concrete command, build step, startup sanity check.
  - Commit-specific `Do not`, only when narrower than the global execution boundaries.
- **Assumptions**: a dedicated list of the non-blocking assumptions made while planning, so the user can review and confirm or correct them before creating the issue. Omit the section only when no assumptions were made.
- **Final review guidance**: expected end state and what a human should focus on when reviewing.

11. Review commit order, filenames, and internal references before ending.
12. Return a summary with the generated issue file path, number of commits, total step count, and important assumptions.
13. Tell the user to review the draft before creating it, calling out the assumptions in particular so they can confirm or correct them.
14. Tell the user that, once reviewed, they can create the issue themselves with `gh issue create --title "<title>" --body-file <deslop-root>/issue/ISSUE.md`.

## Gotcha list

**Input:**
- Do not use the original `<background>/` source folder to create the issue.


**Planning:**
- Do not run `gh`, `git`, or any command that creates the issue or commits; the output is a draft only.
- Do not modify or create implementation files in the target codebase; write only the file under `<deslop-root>/issue/`.
- Preserve existing behavior unless the proposal explicitly asks for a bugfix or functional change.
- Record non-blocking assumptions in the issue's **Assumptions** section so the user can review them.
- Ask before writing the file when an ambiguity blocks commit decomposition.

**Commits:**
- Bias toward the fewest coherent commits; do not over-split into one commit per file or per trivial step.
- Do not over-specify steps; keep them concise and leave routine mechanical details to the executor's judgment.
- Do not create broad commits that require design decisions from the executor.
- Split a commit only when it mixes unrelated responsibilities or forces a design decision on the executor.
- Keep each commit section operational: message, goal, files, steps, check, and commit-specific boundaries.
- Use short illustrative snippets only when they remove implementation ambiguity.
- Do not add `Done when`, `Done criterion`, or milestone sections to individual commits; each commit's `Check` and the final review guidance are enough.
