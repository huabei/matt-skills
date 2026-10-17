---
name: implement
description: "Execute a plan with correctness, computational efficiency, and low-cost validation."
disable-model-invocation: true
---

Implement the execution plan provided by the user. If no plan is identifiable, ask which plan to follow; the user can run `/to-plan` to create one.

Read the relevant code and follow the plan's dependency order. Resume from recorded progress after checking it against the current code. Discuss changes to the goal, mathematical meaning, compatibility, or material resource tradeoffs before proceeding with affected work; record routine implementation adjustments in the plan.

Preserve the intended mathematics and gradient behaviour. Consider compute, memory, synchronization, and data movement at the intended workload size. Prefer suitable existing framework operations; do not silently change precision or the algorithm for speed.

Run the plan's low-cost checks, bounded by steps, input size, or duration. Do not run long training jobs or full experiments. Distinguish correctness checks and measured performance from unverified expectations; report missing hardware, data, or other validation gaps.

Review the actual task diff, including staged, unstaged, and new files, without disturbing pre-existing user changes. Fix substantive correctness and efficiency issues and rerun affected checks.

Update the plan with progress, validation evidence, and deviations. Mark steps complete only when their completion criteria and required checks are satisfied. Report the changes and remaining limitations. Commit or push only when the user has requested it.
