# Deslop Propose Body

## What this produces

One decision-ready proposal at `<flow-folder>/proposals/proposal-<idea>.md` derived from the flow documentation, acceptance criteria, and any user-provided direction.

## Analysis process

1. Use `documentation.md` content from context when already available; otherwise read the file.
2. Use acceptance criteria from context when already available; otherwise read the file:

```txt
<flow-folder>/docs/acceptance-criteria.md
```

3. If existing proposal ideas are not already known from context and `<flow-folder>/proposals/` contains proposals, read enough of them to identify their ideas.
4. Choose one proposal direction that follows the user's directive when provided.
5. If no user directive was provided, choose the best solution direction supported by the documentation and acceptance criteria.
6. Create one proposal, not a set of alternatives.
7. If prior proposals exist, make the new proposal idea distinct from each existing proposal.
8. Write the proposal to a short filesystem-safe idea filename:

```txt
<flow-folder>/proposals/proposal-<idea>.md
```

9. Include this metrics block near the top:

```md
## Metrics

| Metric         | Value        | Notes                                      |
|----------------|--------------|--------------------------------------------|
| effort         | low/mid/high | Implementation complexity for a developer  |
| design_clarity | low/mid/high | How clean and maintainable the design is   |
| estimated_time | e.g. 2-4 h   | Rough range based on what is already known |
```

10. Use `unknown` for a metric value only when it cannot be inferred, and explain why in the notes cell.
11. End by telling the user the proposal file created and that it is ready to accept, reject, revise, compare with another proposal, or plan.
12. Suggest running `$deslop-plan-prs` for the same flow folder after the proposal is accepted or chosen.

## Gotcha list

**Input:**
- Do not use the `background/` folder to create the proposal.
- Do not read `documentation.md`, `acceptance-criteria.md`, or existing proposal files when their contents are already available in current context.
- Do not continue when acceptance criteria are neither in context nor available in `acceptance-criteria.md`.
- Use `acceptance-criteria.md` as required decision input.
- Treat user-provided proposal direction as binding unless it conflicts with documented requirements.

**Proposal:**
- Create one clear direction, not multiple alternatives.
- Do not ignore the user's requested solution direction when it is compatible with the documentation.
- Do not ask for a proposal direction when the user simply invokes the skill.
- Do not reject the task because proposals already exist; create a distinct proposal idea.
- Do not create an execution plan, task breakdown, or implementation.
- Read source files only when the documented understanding is insufficient to avoid a flawed proposal.

**Metrics:**
- Set `effort` from implementation complexity, moving parts, side effects, and codebase familiarity.
- Set `design_clarity` from coupling, concepts added, and ease of explanation.
- Set `estimated_time` as a rough developer planning range in hours or days.

**Next step:**
- Point the user to `$deslop-plan-prs` after a proposal is accepted or chosen.
