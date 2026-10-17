## What it does

`teach` explains a concept through the current code or development task. Teaching happens in the conversation, without a course, HTML lessons, or persistent learning records.

It adjusts the explanation to your questions and responses, defines necessary terms, and connects the idea to a small concrete example. Explanations of code behaviour are grounded in the relevant implementation, with source code or official documentation consulted when verification is needed.

## When to reach for it

You invoke this by typing `/teach`; the agent will not reach for it on its own. Use it when understanding a concept will help you follow or perform the current task.

| What you need | Reach for |
| --- | --- |
| Understand why or how a piece of code works | `teach` |
| Have the previous message explained more clearly | [wait-what](https://aihero.dev/skills-wait-what) |
| Investigate code and save cited findings | [research](https://aihero.dev/skills-research) |

## Focused explanation and feedback

A small example ties the concept to the implementation. A short exercise or a request to explain the idea back can help check understanding when useful. The skill responds to your answer and stops when the current question is answered, rather than starting another lesson.

## Common questions

**Does it create a teaching workspace or learning files?**

No. It teaches directly in the conversation and does not create a long-term curriculum.

**Will it change the code while teaching?**

Only if you request implementation changes. Reading and explaining code does not itself authorize modifying it.

## It's working if

- The explanation addresses the question that arose in your current task.
- Necessary terms are explained and examples connect to the code.
- Assumptions are distinguished from verified behaviour.
- No teaching workspace or unrelated lesson is created.

## Where it fits

`teach` is a standalone aid during development. [research](https://aihero.dev/skills-research) investigates code and documents findings; [implement](https://aihero.dev/skills-implement) executes planned changes. See [ask-matt](https://aihero.dev/skills-ask-matt) for the map.
