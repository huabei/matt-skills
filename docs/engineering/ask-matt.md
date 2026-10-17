## What it does

`ask-matt` recommends a skill from the 17 retained skills in this research fork. It reads the target skill before describing its behaviour and stops after the recommendation so you can choose what to invoke.

## When to reach for it

You invoke this by typing `/ask-matt`; the agent does not reach for it on its own. Use it when you know the task but are unsure which retained skill fits.

## Current boundaries

The spec and ticket orchestration flow has been removed. Some retained skills still carry their original engineering assumptions and will be adapted separately. The router points out those constraints rather than promising experiment execution or analysis that the skills do not yet provide.

## Common questions

**Does it run the recommended skill?**

No. It recommends the next step and leaves invocation to you.

**Does it include other skills installed on my machine?**

No. It maps this repository's retained set.

## It's working if

- It names a retained skill and explains why it fits your situation.
- It reads that skill before describing what it does.
- It explains any current prerequisites that affect your task.

## Where it fits

`ask-matt` is the standalone router over this set. Common destinations include [grill-with-docs](https://aihero.dev/skills-grill-with-docs), [research](https://aihero.dev/skills-research), and [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs).
