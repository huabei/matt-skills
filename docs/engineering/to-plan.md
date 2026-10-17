## What it does

`to-plan` turns the discussion and codebase understanding you already have into a local **execution plan**. It synthesizes settled decisions without restarting the interview, and records unresolved questions without guessing their answers.

The plan connects ordered code changes to completion criteria and low-cost checks. It also accounts for computational efficiency and separates implementation correctness from scientific questions that need full experiments.

## When to reach for it

You invoke this by typing `/to-plan`; the agent will not reach for it on its own. Use it when you are ready to turn a discussion into work that [implement](https://aihero.dev/skills-implement) can execute, including across sessions.

| Your situation | Reach for |
| --- | --- |
| The approach is discussed and needs an execution plan | `/to-plan` |
| The goal or approach needs discussion | [grill-with-docs](https://aihero.dev/skills-grill-with-docs) |
| Understanding the current code requires investigation | [research](https://aihero.dev/skills-research) |
| A plan exists and you want its code changes made | [implement](https://aihero.dev/skills-implement) |

## Prerequisites

Run it in the codebase the plan concerns. It writes to your chosen path or the repository's existing plan location, falling back to `plans/<slug>.md`. No issue tracker is required.

## An executable handoff

Each step names a deliverable, a completion criterion, and a low-cost check. Dependencies make the execution order clear, while code paths ground the plan in the current repository. Compute and memory tradeoffs are considered at the intended workload size, even when validation uses small inputs.

Unresolved decisions are visible. A step that depends on one stays blocked; a scientific question that requires training is recorded separately and need not block implementing an already agreed method. Planning ends at the saved document, before implementation or experiment execution starts.

## Common questions

**Is this the old spec-and-issue workflow?**

It replaces the removed `to-spec` in this fork. The output is a local plan with implementation steps, rather than user stories, tracker issues, or labels.

**Does it implement the plan automatically?**

No. You invoke `/implement` with the saved plan when ready. That skill updates progress and validation evidence as it works.

**Does the plan include full experiments?**

It records questions requiring those experiments, but its executable steps cover code changes and low-cost validation. Full training and complete experiments remain outside this workflow.

## It's working if

- You receive a local plan that reflects the discussion and actual code paths.
- Every step has an observable completion criterion and a bounded check where execution is needed.
- Assumptions and blocked decisions are visible rather than presented as agreements.
- The plan addresses compute and memory costs without claiming unmeasured speedups.
- Planning stops after saving the document.

## Where it fits

`to-plan` is the planning step between [grill-with-docs](https://aihero.dev/skills-grill-with-docs), which maintains shared understanding, and [implement](https://aihero.dev/skills-implement), which executes the plan. Use [ask-matt](https://aihero.dev/skills-ask-matt) to choose the next skill.
