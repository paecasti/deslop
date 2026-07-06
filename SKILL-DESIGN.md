# Deslop Skill Design

Deslop skills are small workflow tools. They are not a closed platform and are not tied to a specific agent runtime. Their job is to help a software engineer move from unclear input to acceptance-driven planning and verification.

The design goal is simple: keep each skill predictable, readable, and easy to modify.

## Style Principles

- **Validation first**: check required inputs before doing real work.
- **Sequential steps**: use ordered instructions instead of vague guidance.
- **Small surface**: keep each skill short enough to inspect and edit.
- **Clear stops**: stop on missing prerequisites instead of guessing.
- **Acceptance-driven**: proposal, planning, and verification depend on acceptance criteria.
- **Gotcha lists**: name common mistakes so the agent can stay inside the intended lane.
- **User control**: support the engineer's workflow instead of replacing it.

## Validation First

Each skill starts by checking whether it has enough context to run.

This prevents common failures: using the wrong folder, inventing missing information, skipping user review, or advancing the workflow too early.

Examples:

- understanding needs a background folder and derives the Deslop root from its parent;
- acceptance criteria need reviewed documentation;
- proposals need documentation and acceptance criteria;
- planning needs a selected or inferable proposal;
- verification needs implementation code, one proposal, documentation, and acceptance criteria.

Prefer a clear stop over a clever guess.

## Sequential Process

Each skill uses ordered steps so the workflow is easy to follow and easy to change.

The steps should answer:

- what to read;
- what to produce;
- when to stop;
- what the user should review next.

If a team wants a different proposal format, report shape, or planning style, it should be able to edit the relevant steps without redesigning the whole workflow.

## Gotcha Lists

Gotcha lists are part of the skill design.

They keep the instructions small without making them vague. They call out predictable failure modes such as:

- reading too much context;
- skipping validation;
- turning acceptance criteria into tasks;
- proposing before understanding;
- planning while still proposing;
- fixing code during verification.

## Narrow Responsibilities

Each skill has one main job:

- `$deslop-understand`: document the problem and context.
- `$deslop-generate-acceptance-criteria`: turn documentation into testable criteria.
- `$deslop-brainstorm-proposals`: explore solution directions.
- `$deslop-propose`: create one decision-ready proposal.
- `$deslop-plan-prs`: turn an accepted proposal into PR-sized work.
- `$deslop-plan-issue`: turn an accepted proposal into a single self-contained, commit-by-commit issue draft.
- `$deslop-verify-implementation`: check completed work against the proposal, documentation, and acceptance criteria.

The boundaries matter:

- understanding should not propose;
- acceptance criteria should not design implementation;
- proposal should not plan PRs;
- planning should not modify implementation code;
- issue planning should not create the issue or modify implementation code;
- verification should not fix failures unless the user asks.

## External Tools Are Expected

Deslop does not own the full development process.

Users can pair it with any implementation skill, refinement loop, testing tool, code review agent, team checklist, or project-specific workflow.

Deslop provides the acceptance-driven backbone. The engineer decides what to connect around it.

## Design Test

A skill is probably drifting if it:

- forces a full development methodology;
- hides important decisions inside agent behavior;
- becomes hard to modify;
- reads unrelated context just because it exists;
- treats the skill as the authority instead of the engineer;
- starts doing another skill's job.

A good Deslop skill should feel like a sharp tool: small, explicit, understandable, and useful alongside whatever else the engineer chooses to use.
