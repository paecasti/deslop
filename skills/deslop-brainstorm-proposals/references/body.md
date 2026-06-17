# Deslop Brainstorm Proposals Body

## What this produces

A lightweight proposal brainstorm at `<flow-folder>/proposals/brainstorm-proposals.md` with multiple brief solution ideas grounded in documentation, acceptance criteria, and metrics.

## Analysis process

1. Use `documentation.md` content from context when already available; otherwise read the file.
2. Use acceptance criteria from context when already available; otherwise read the file:

```txt
<flow-folder>/docs/acceptance-criteria.md
```

3. Read source project files only when needed to avoid irrelevant or impossible ideas.
4. Generate the requested number of distinct solution ideas.
5. Keep each idea brief; do not deepen it into a full proposal.
6. Write the brainstorm to:

```txt
<flow-folder>/proposals/brainstorm-proposals.md
```

7. Use this structure:

```md
# Proposal Brainstorm

## Context

## Ideas

### Idea 1: <short idea name>

<Brief explanation>

| Metric         | Value        | Notes |
|----------------|--------------|-------|
| effort         | low/mid/high |       |
| design_clarity | low/mid/high |       |
| estimated_time | e.g. 2-4 h   |       |
```

8. Set `effort`, `design_clarity`, and `estimated_time` for each idea.
9. End by telling the user the brainstorm file created and that any idea can be turned into a full proposal with `$deslop-propose`.
10. Suggest running `$deslop-propose` with the chosen brainstorm idea as the proposal direction.

## Gotcha list

**Input:**
- Do not use the `background/` folder to brainstorm proposals.
- Do not continue when documentation is neither in context nor available in `documentation.md`.
- Do not continue when acceptance criteria are neither in context nor available in `acceptance-criteria.md`.
- Do not read `documentation.md` before the validation process passes.
- Do not read `documentation.md` or `acceptance-criteria.md` when their contents are already available in current context.
- Use `acceptance-criteria.md` as required decision input.

**Brainstorm:**
- Do not create full proposal files for each idea.
- Do not create an execution plan, task breakdown, or implementation.
- Do not make the ideas variations of the same solution.
- Do not invent requirements that are not supported by `documentation.md` or `acceptance-criteria.md`.
- Read source files only when the documented understanding is insufficient to avoid weak ideas.

**Count:**
- Default to 5 ideas when the user does not specify a count.
- Honor the user's requested count when it is a concrete number.
- Ask one concise clarification only when the requested count is ambiguous or impossible.

**Metrics:**
- Set `effort` from implementation complexity, moving parts, side effects, and codebase familiarity.
- Set `design_clarity` from coupling, concepts added, and ease of explanation.
- Set `estimated_time` as a rough developer planning range in hours or days.

**Next step:**
- Point the user to `$deslop-propose` after the brainstorm is complete.
