# Deslop

Deslop is a simple Spec-Driven Development workflow for turning unclear software work into documented, acceptance-driven, plannable, and verifiable decisions.

Most SDD workflows start from a reasonable intention: covering the whole development cycle. They try to help you define specifications, plan work, generate tasks, implement, validate, document, and maintain consistency. The problem is that, in trying to become complete systems, they also become prescriptive systems. They do not only give you tools; they tell you how to think, how to structure the problem, which steps to follow, which artifacts to produce, and in what order to work.

Deslop starts from a different premise: the system should not be the protagonist. The software engineer should be.

## Why Deslop Exists

In many SDD workflows, the technology tries to take the center. The system presents itself as an almost perfect machine for transforming intent into software. The more complete the system is, the more it seems to promise that the correct process will solve the problem.

But in practice, real software problems are not solved by a workflow alone. They are solved with judgment: understanding context, making decisions, accepting tradeoffs, choosing tools, discarding paths, adapting to constraints, and knowing when to skip steps.

Deslop does not try to replace that judgment. It tries to support it.

That is why Deslop exists: to make work clearer before implementation, without turning that clarity into a heavy system that forces the user to work in only one way. The workflow helps transform a vague idea into reviewable documentation, acceptance criteria, proposals, plans, and verification. But control over the decisions stays with the user.

## Philosophy

Deslop is intentionally simple. It does not try to impose a single way to build software. It does not require a specific technology, implementation style, architecture, planning format, or problem-solving approach.

That simplicity is what makes it versatile. A smaller workflow is easier to understand, easier to modify, and easier to apply to different kinds of problems, different working styles, and different sizes of implementation. It can be used for a small bug, a behavior change, an architecture decision, a refactor, or a multi-PR plan without forcing all of those cases into a large process.

Deslop also does not try to be the most technologically complete workflow possible, because that kind of completeness often reduces versatility. The more a system tries to cover, the more it starts requiring you to work inside its own assumptions.

The distinction matters:

Other workflows say: "this is the system; work inside it."

Deslop says: "these are tools; use them to think better."

## What Deslop Tries To Solve

Deslop tries to solve the point where agents usually fail the most: the gap between loosely structured human intent and an implementation that actually satisfies what was expected.

To do that, it does not try to capture the entire development process. It focuses on the contract that matters most before implementation starts: what must be true when the work is finished.

The center of Deslop is acceptance criteria. First, it reads the user's input and background material. Then it generates draft documentation that makes the problem, constraints, concepts, and expected behavior explicit. From that documentation, it generates acceptance criteria. Those criteria do not dictate how to implement, but they do clarify what must be satisfied.

From there, Deslop can help propose, plan, and verify. But not because the workflow owns the process. It can help because the engineer has already defined what it means for the work to be done well.

Everything outside that core can be complemented with whatever technology, skill, agent, or external process the user considers necessary. You can pair Deslop with a separate implementation skill, a documentation refinement skill, a code review agent, a testing tool, a team-specific workflow, or any project-specific system.

Deslop does not compete with those tools or require them to fit into a closed ecosystem. It works as a lightweight acceptance-driven backbone, and lets the engineer decide what to connect around it.

## Workflow

Each Deslop run lives in a Deslop root. That folder is the unit of work, and it can be any folder the user chooses for that run.

```txt
<deslop-root>/
  <background>/
  docs/
  proposals/
  plan/
  issue/
  verification/
```

The main process is intentionally short:

1. `$deslop-understand` reads the user's input and the material in a user-specified `<background>` folder, treats that folder's parent as `<deslop-root>`, then generates `docs/documentation.md` as draft documentation.
2. The user reviews `docs/documentation.md` and decides whether it represents the problem correctly.
3. `$deslop-generate-acceptance-criteria` uses that documentation to generate `docs/acceptance-criteria.md`.
4. The user reviews the acceptance criteria and decides whether they are the right contract.
5. `$deslop-brainstorm-proposals` or `$deslop-propose` uses the documentation and acceptance criteria to explore or choose a solution direction.
6. `$deslop-plan-prs` turns an accepted proposal into a PR-by-PR implementation plan. Alternatively, `$deslop-plan-issue` turns the same proposal into a single self-contained, commit-by-commit issue draft that a simpler implementing agent can execute on its own.
7. `$deslop-verify-implementation` compares the completed implementation against the proposal, documentation, and acceptance criteria.

The important boundary is that acceptance criteria become the downstream contract. Once they exist, planning and verification should be judged against them, not against a loose memory of the original request.

That is the philosophy: less system, more judgment. Less technological perfection, more user control. Deslop does not try to be the best universal process for building software. It tries to be a set of simple tools that help engineers keep clarity, make decisions, and verify results without losing freedom.

## Skill Design

Deslop skills follow the same philosophy as the workflow: they should be small, readable, validation-first, and easy to adapt. See [SKILL-DESIGN.md](SKILL-DESIGN.md) for the style decisions behind the skills.

