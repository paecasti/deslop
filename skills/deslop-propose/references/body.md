# Deslop Propose Body

## What this produces

One decision-ready proposal at `<deslop-root>/proposals/proposal-<idea>.md` derived from the Deslop documentation, acceptance criteria, and any user-provided direction.

## Analysis process

1. Use `documentation.md` content from context only when its recorded modification time matches the file's current modification time; otherwise read the file and record its modification time.
2. Apply the same freshness check to the acceptance criteria; read and record the file when context is not fresh:

```txt
<deslop-root>/docs/acceptance-criteria.md
```

3. If `<deslop-root>/proposals/` contains proposals, apply the same freshness check to them: reuse their ideas from context only when the recorded modification times match; otherwise read enough of them to identify their ideas and record their modification times.
4. Read source project files only when the documented understanding is insufficient to avoid a flawed proposal.
5. Choose one proposal direction that follows the user's directive when provided.
6. If no user directive was provided, choose the best solution direction supported by the documentation and acceptance criteria.
7. Create one proposal, not a set of alternatives.
8. If prior proposals exist, make the new proposal idea distinct from each existing proposal.
9. Write the proposal to a short filesystem-safe idea filename:

```txt
<deslop-root>/proposals/proposal-<idea>.md
```

10. Include this metrics block near the top:

```md
## Metrics

| Metric         | Value        | Notes                                      |
|----------------|--------------|--------------------------------------------|
| effort         | low/mid/high | Implementation complexity for a developer  |
| design_clarity | low/mid/high | How clean and maintainable the design is   |
| architectural_fit | low/mid/high | How naturally it fits existing architecture and conventions |
| estimated_time | e.g. 2-4 h   | Rough range based on what is already known |
```

11. Use `unknown` for a metric value only when it cannot be inferred, and explain why in the notes cell.
12. Record the modification time of the written proposal file so later Deslop skills in the same session can detect user edits.
13. End by telling the user the proposal file created and that it is ready to accept, reject, revise, compare with another proposal, or plan.
14. Suggest running `$deslop-plan-prs` for the same Deslop root after the proposal is accepted or chosen.

## Gotcha list

**Input:**
- Do not use the original `<background>/` source folder to create the proposal.
- Treat user-provided proposal direction as binding unless it conflicts with documented requirements.

**Proposal:**
- Do not reject the task because proposals already exist; create a distinct proposal idea.
- Do not create an execution plan, task breakdown, or implementation.
