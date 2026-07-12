# Deslop Brainstorm Proposals Body

## What this produces

A lightweight proposal brainstorm at `<deslop-root>/proposals/brainstorm-proposals.md` with multiple brief solution ideas grounded in documentation, acceptance criteria, and metrics.

## Analysis process

1. Use `documentation.md` content from context only when its recorded modification time matches the file's current modification time; otherwise read the file and record its modification time.
2. Apply the same freshness check to the acceptance criteria; read and record the file when context is not fresh:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

3. Read source project files only when needed to avoid irrelevant or impossible ideas.
4. Generate the requested number of distinct solution ideas.
5. Keep each idea brief; do not deepen it into a full proposal.
6. Write the brainstorm to:

```txt
<deslop-root>/proposals/brainstorm-proposals.md
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
| architectural_fit | low/mid/high |       |
| estimated_time | e.g. 2-4 h   |       |
```

8. Set `effort`, `design_clarity`, `architectural_fit`, and `estimated_time` for each idea.
9. Record the modification time of the written `brainstorm-proposals.md` so later Deslop skills in the same session can detect user edits.
10. End by telling the user the brainstorm file created and that any idea can be turned into a full proposal with `$deslop-propose`.
11. Suggest running `$deslop-propose` with the chosen brainstorm idea as the proposal direction.

## Gotcha list

**Input:**
- Do not use the original `<background>/` source folder to brainstorm proposals.
- Do not continue when documentation is neither in context nor available in `documentation.md`.
- Do not continue when acceptance criteria are neither in context nor available in `acceptance-criteria.md`.
- Do not read `documentation.md` before the validation process passes.
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

**Next step:**
- Point the user to `$deslop-propose` after the brainstorm is complete.
