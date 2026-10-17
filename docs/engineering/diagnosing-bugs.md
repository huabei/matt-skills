## What it does

`diagnosing-bugs` investigates a specific failure through a **tight feedback loop**, falsifiable hypotheses, and targeted probes. It can apply an evidence-supported local fix, while keeping execution and validation low-cost.

When the original failure needs unavailable hardware or expensive training, it investigates code and existing artifacts and states the evidence boundary. It does not require a fabricated reproduction before reasoning can begin, and it does not call an unverified fix proven.

## When to reach for it

Type `/diagnosing-bugs`, or the agent reaches for it when a specific hard failure needs investigation.

| Your situation | Reach for |
| --- | --- |
| NaNs, broken gradients, incorrect metrics, or another training anomaly | This skill |
| A specific slowdown or memory regression | This skill, with a comparable baseline |
| Research results fall short without evidence of a defect | First distinguish a code failure from a scientific outcome |
| A planned code change is already clear | [implement](https://aihero.dev/skills-implement) |
| You want a simple explanation rather than an investigation | Ask directly; a full diagnosis is unnecessary |

## Tight enough to distinguish causes

A useful loop catches the reported symptom, rather than just checking that code runs. Small inputs, saved batches, checkpoints, and comparisons with a trusted implementation can reduce the cost. Minimization stops when the remaining reproduction is sufficient to distinguish plausible causes.

Intermittent failures receive bounded retries and a reported reproduction frequency. Seeds and execution conditions are recorded, but deterministic GPU behaviour is not assumed. Performance comparisons account for warmup, accelerator synchronization, and relevant memory costs before attributing a regression.

## Common questions

**Must it reproduce the failure before investigating?**

Reproduction is preferred. When it is unavailable or too expensive, code, logs, and existing artifacts can support an investigation. The report separates observations, hypotheses, and unverified properties.

**Can it write a fix without a separate plan?**

Yes, for an evidence-supported local fix. Changes to the algorithm, mathematical meaning, compatibility, material resource tradeoffs, or broad structure return to discussion before affected work proceeds. [to-plan](https://aihero.dev/skills-to-plan) can capture a larger agreed change.

**Does verification rerun my full training job?**

No. It uses bounded reproductions and relevant low-cost checks. If the original full-scale scenario has not been rerun, the report states that limitation.

**Does a missing regression test imply bad architecture?**

No. Hardware access, nondeterminism, and cost can prevent a meaningful low-cost test. The skill records the gap rather than adding a shallow test or assuming its cause.

## It's working if

- Evidence concerns the failure you reported, not a substitute symptom.
- Each hypothesis has a prediction that a targeted observation can distinguish.
- Retries and validation stay bounded, without starting full experiments.
- A fix is supported by evidence and its remaining verification gaps are visible.
- Temporary instrumentation is removed without disturbing your data or experiment outputs.

## Where it fits

`diagnosing-bugs` is a standalone investigation and local repair skill. Larger changes can pass through [to-plan](https://aihero.dev/skills-to-plan) and [implement](https://aihero.dev/skills-implement). After a difficult session, [retro](https://aihero.dev/skills-retro) can suggest improvements to the agent's environment. Use [ask-matt](https://aihero.dev/skills-ask-matt) to choose the next skill.
