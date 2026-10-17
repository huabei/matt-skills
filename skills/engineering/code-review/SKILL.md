---
name: code-review
description: "Review uncommitted changes for implementation correctness and computational efficiency using parallel reviewers. Use when reviewing staged, unstaged, or new files, or before committing an implementation."
---

Review **uncommitted changes only**, along two axes: **Correctness** and **Efficiency**. Both check the execution plan where one is available. Report findings without modifying implementation code, staging files, or committing.

## Process

1. Establish the scope with `git status --short`, `git diff --cached`, `git diff`, and `git ls-files --others --exclude-standard`. Include staged and unstaged changes and read new files explicitly; `git diff HEAD` alone can hide changes that cancel between the index and working tree. Read the relevant surrounding code. If there are no changes, report that and stop. Respect a user-specified file scope and distinguish pre-existing changes when called from implementation.

2. Read the provided execution plan or the one clearly identified in the conversation, plus applicable repository instructions and coding standards. No issue tracker is required. Without a plan, review the code itself and state that plan compliance could not be fully checked; do not infer requirements from the implementation.

3. Run two reviewer subagents in parallel, giving both the same file scope, staged and unstaged diffs, new-file contents or paths, plan, and applicable standards. Both must examine the working-tree code and any distinct staged version. Give each the brief below and require it to review directly, without invoking this skill or spawning additional agents.

   - **Correctness:** check whether the changes implement the plan and preserve intended mathematics, gradients, data and evaluation behaviour, and compatibility. Identify missing requirements, unintended behaviour, and regressions. Apply repository standards, but report style or structure only when it has a concrete consequence.
   - **Efficiency:** check compute and memory costs at the intended workload size, including repeated work, intermediate tensors, synchronization, data movement, and distributed communication where relevant. Check the plan's resource constraints and whether optimizations preserve the intended semantics. Distinguish measured results from inspection-based risks; do not claim a speedup or regression without evidence.

   Each reviewer reports actionable findings with severity, file and line, the triggering conditions, concrete consequence, and supporting evidence. Cite the plan or repository rule when relevant. Label findings against an index-only version as staged. Reviewers may run bounded low-cost checks in isolation, without changing implementation files or experiment artifacts; no long training or full experiments.

4. Verify findings against the relevant code and evidence. Remove unsupported claims and duplicates, then report findings in severity order, labelled Correctness or Efficiency. Include the location, consequence, and a concise suggested fix. Separate uncertain risks and validation gaps from confirmed defects. If no actionable findings remain, say so and state material limits of the review; do not invent improvements to fill the report.
