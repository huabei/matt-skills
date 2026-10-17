## What it does

`implement` changes the codebase according to your execution plan, checking both implementation correctness and computational efficiency. It finishes with **low-cost validation**, without running long training jobs or complete experiments.

A passing smoke check shows that the changed path executes under the checked conditions. It does not show that a method converges or improves research results.

## When to reach for it

You invoke this by typing `/implement`; the agent will not reach for it on its own. Provide the plan path or identify the plan in the conversation. If no plan exists, run [to-plan](https://aihero.dev/skills-to-plan) first. No spec or issue tracker is required.

| Your situation | Reach for |
| --- | --- |
| A plan exists and you want its code changes made | `/implement` |
| Discussion is settled and needs an execution plan | [to-plan](https://aihero.dev/skills-to-plan) |
| The goal needs clarification and shared project understanding | [grill-with-docs](https://aihero.dev/skills-grill-with-docs) |
| You need to understand an existing implementation first | [research](https://aihero.dev/skills-research) |
| A bug needs diagnosis before a fix can be chosen | [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs) |

## Following the plan

The plan carries scope, implementation decisions, and completion criteria. The skill follows dependency order and records progress, validation evidence, and routine deviations in that document. Discoveries that change the goal, mathematical meaning, compatibility, or material resource tradeoffs return to discussion before affected work proceeds.

## Correctness and computational cost

The intended mathematics matters alongside execution. Shapes, masks, reductions, gradients, precision, and training behaviour must match the request. An optimization that changes those properties needs an explicit decision, rather than being slipped into an implementation.

Efficiency includes compute, memory, synchronization, and data movement at the intended workload size. Replacing a loop with a large intermediate tensor can make a small check faster while making the real workload run out of memory. The skill considers that scaling and uses existing optimized framework operations where appropriate.

## Low-cost validation

Checks follow the changed path: focused tests, small numerical examples, and bounded execution through the relevant forward and backward code. A short performance measurement is useful when feasible, with its device, dtype, input size, and timing conditions reported. The skill distinguishes measured performance from expectations based on inspection.

## Common questions

**Does this run full training or evaluation?**

No. A few bounded steps can check execution and gradients. Full training, complete experiments, and scientific outcome analysis remain separate work.

**Must every change use TDD?**

No. Verification follows the changed behaviour and available tooling. Use [tdd](https://aihero.dev/skills-tdd) when test-first development is appropriate; implementation otherwise follows the checks in the plan.

**Does faster-looking code count as an optimization result?**

No. A performance claim needs a measurement under stated conditions. When suitable hardware is unavailable, the report identifies the unmeasured property.

**Does it commit automatically?**

No. Changes remain available for inspection. Committing or pushing requires a user request.

## It's working if

- The plan shows completed steps, validation evidence, and any deviations.
- The requested behaviour changes without requiring a spec or tracker setup.
- Relevant low-cost checks run, and the report states what they establish.
- Efficiency is considered at the intended workload size, including memory cost.
- No long training job or full experiment starts as part of validation.
- Missing hardware or full-scale evidence is reported without claiming scientific success.

## Where it fits

`implement` is the code-change step after [to-plan](https://aihero.dev/skills-to-plan) has captured the agreed execution plan. [tdd](https://aihero.dev/skills-tdd) supplies test-first development when requested; It calls [code-review](https://aihero.dev/skills-code-review) on the task's uncommitted changes with the execution plan, then fixes substantive findings and reruns affected checks. Use [ask-matt](https://aihero.dev/skills-ask-matt) to choose among the retained skills.
