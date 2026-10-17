## What it does

`code-review` examines uncommitted changes for **Correctness** and **Efficiency**, using two parallel [subagents](https://www.aihero.dev/ai-coding-dictionary/subagent). Both check the execution plan when one is available. The review covers staged, unstaged, and new files, and reports findings without modifying implementation code.

It verifies the reviewers' claims before reporting them, merges duplicates, and orders findings by severity. Every actionable finding needs a location, triggering conditions, a concrete consequence, and evidence.

## When to reach for it

Type `/code-review`, or the agent reaches for it when reviewing uncommitted work. [implement](https://aihero.dev/skills-implement) calls it before handing back a completed change.

| Your situation | Behaviour |
| --- | --- |
| Staged, unstaged, or new files need review | Reviews those changes and the surrounding code |
| You provide a plan | Both reviewers check the applicable decisions and requirements |
| No plan is available | Reviews code and states the limit on checking plan compliance |
| Only committed changes exist | Reports that there are no uncommitted changes to review |

## Two independent perspectives

The Correctness reviewer checks implementation behaviour, including mathematics, gradients, data and evaluation logic, and compatibility. Repository standards apply, but style and structure findings need a concrete consequence rather than a named code smell.

The Efficiency reviewer considers compute and memory at the intended workload size, including synchronization and data movement. A potential bottleneck found by inspection is distinct from a measured regression. Numerical or algorithmic changes made for speed must still match the plan.

Both reviewers work directly, without recursively invoking the skill or delegating further. Low-cost checks must be bounded and isolated from implementation files and experiment artifacts. Long training and full experiments remain outside review.

## Common questions

**Must I commit before review?**

No. This skill reviews only uncommitted changes. It examines both the index and working tree, including staged edits that an unstaged reversal could hide in a combined diff. Findings about a distinct index version are labelled staged.

**Does it fix the findings?**

No. It reports them. When called by [implement](https://aihero.dev/skills-implement), that skill handles substantive fixes and repeats the affected checks.

**Does it need a spec or issue tracker?**

No. A local execution plan supplies intended behaviour when available. Missing requirements are not invented from the code being reviewed.

## It's working if

- The review covers staged, unstaged, and new files in the requested scope.
- Findings identify concrete consequences and code locations.
- Unsupported performance claims are excluded, and uncertain risks are labelled.
- The report prioritizes verified findings rather than reproducing raw reviewer output.
- Review leaves implementation files and Git staging unchanged.

## Where it fits

`code-review` follows [implement](https://aihero.dev/skills-implement), which invokes it with the plan produced by [to-plan](https://aihero.dev/skills-to-plan). It also works independently on uncommitted changes. Use [ask-matt](https://aihero.dev/skills-ask-matt) to choose among the retained skills.
