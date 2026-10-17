## What it does

`tdd` builds a feature or fixes a bug test-first: one failing test, then just enough code to pass it, then the next behaviour. It carries the standards that make that loop produce tests worth keeping: what a good test is, where tests go, what mocks are for, and the three anti-patterns that make a suite worthless.

It uses the test seams and checks in the execution plan, or a relevant existing interface when no seam is specified. It asks only when a material ambiguity affects what behaviour is verified. Tests stay low-cost; full training and research-metric improvements are not red-green signals.

## When to reach for it

Type `/tdd`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it automatically when a task fits: building a feature or fixing a bug test-first, or when you say "red-green-refactor".

Reach for it when there is a concrete behaviour to build, with an input and an observable output, and you want tests that survive a refactor.

| Your situation | Where to go |
| --- | --- |
| A behaviour with defined inputs and outputs (business logic, a request/response contract, a transformation, validation) | `tdd` |
| The behaviour isn't pinned down yet | [grill-with-docs](https://aihero.dev/skills-grill-with-docs) to clarify it, then [to-plan](https://aihero.dev/skills-to-plan) to record the steps and checks |
| The question is really the shape of the interface, not the tests | [codebase-design](https://aihero.dev/skills-codebase-design) |
| You have an execution plan and want it implemented | [implement](https://aihero.dev/skills-implement) |
| Config, wiring, glue, type annotations, straight CRUD delegation | Nothing here fits well; see the open gap below |

That last row is a real gap. The skill decides *where* the seams go, but nothing in it decides *whether* a change is worth the loop at all. If you run it on a change with no independent source of truth to assert against, you get a test that restates the implementation. That is the tautological anti-pattern the skill warns about, reached from the other direction. It is [issue #746](https://github.com/mattpocock/skills/issues/746), and it is open. Until it closes, you make that call yourself, or write the rule into your `CLAUDE.md`.

## Prerequisites

[codebase-design](https://aihero.dev/skills-codebase-design) needs to be installed. `tdd` used to carry its own deep-module and interface-design notes; v1.0 deleted them in favour of the shared skill, and `tdd` now uses its interface-design vocabulary. Nothing else; the skill is [stateless](https://www.aihero.dev/ai-coding-dictionary/stateless) and writes no files of its own.

## The loop, and the seam it runs at

The skill rests on three terms.

**Red-green.** Write the failing test, then only enough code to pass it. Do not write code for the test after next. Once green, make small necessary refactors and rerun the affected tests. [code-review](https://aihero.dev/skills-code-review) reports findings rather than performing refactoring.

**Vertical slice.** Write one test at one seam, then the minimal implementation, then repeat. The first cycle is a **tracer bullet** that proves a single path end to end. The opposite is horizontal slicing: all the tests first, then all the code. Tests written in bulk verify *imagined* behaviour. They check the shape of things rather than what a user does, and they commit you to a test structure before you understand the implementation.

**Seam.** A seam is the public boundary you observe behaviour at without reaching inside. Prefer the seams and checks captured by [to-plan](https://aihero.dev/skills-to-plan). When the plan is silent, choose a relevant existing interface and ask only if the choice has a material ambiguity.

The three anti-patterns it is written to prevent:

| Anti-pattern | The tell |
| --- | --- |
| Implementation-coupled | The test breaks when you rename an internal function, though behaviour did not change. Mocked internal collaborators, asserted call counts, database queries used to verify instead of the interface. |
| Tautological | The expected value is computed the way the code computes it, so the test passes by construction. Expected values have to come from somewhere else: a known-good literal, a worked example, the spec. |
| Horizontal slicing | A batch of tests landed before any implementation. |

Mocks are for system boundaries only: external APIs, time, randomness, sometimes the filesystem or the database. Never mock your own modules.

## Common questions

**Must I approve every test seam?**

No. A seam already covered by the execution plan needs no repeated confirmation. If a choice is needed, the agent explains what each option catches and misses and asks only when the ambiguity matters.

**Can it refactor after a test passes?**

Yes, when needed. Keep the change small and rerun the affected tests. Review remains a separate reporting step.

**It wrote the implementation before the test, even though the skill says red first.**

It happens. One user pushed the [model](https://www.aihero.dev/ai-coding-dictionary/model) on it and got an unusually honest answer: "I knew the skill said 'one test at a time, watch it fail for the right reason'. I read it. I just defaulted to my normal habit." The skill accepts this. No instruction makes an agent comply 100% of the time, and stricter wording restricts the agent's creativity for little gain. The loop is worth running even when the agent does not follow it strictly, because the results are still better overall. If strict adherence matters for a particular slice, watch the run rather than trusting the skill to enforce it.

**Should it write browser or end-to-end tests first?**

Usually not, and the skill will not stop it. A user reported the agent writing a Playwright test first, then spending a long loop re-running it and concluding the *test* was broken for a feature that did not exist yet. Browser tests are slow enough that the red-green feedback loop stops paying for itself. State in your repo's `CLAUDE.md` that browser tests come after the behaviour works.

**Does `/tdd` replace `/implement`, or the course's `/do-work`?**

No. `/tdd` documents the methodology; `/implement` follows an execution plan, performs low-cost checks, and calls code review. The course's single `/do-work` step is now split across `/implement`, `/tdd` and `/code-review`. Use `/implement` to execute a plan and `/tdd` for test-first development.

**Where did the deep-modules and interface-design guidance go?**

Into [codebase-design](https://aihero.dev/skills-codebase-design) in v1.0, generalised so several skills share one vocabulary. Small necessary refactors now happen after green; [code-review](https://aihero.dev/skills-code-review) reports correctness and efficiency findings.

## It's working if

- Tests follow the execution plan or a relevant existing interface, without repeated confirmation of settled choices.
- One test appears, goes red, gets just enough code to pass, and only then does the next test appear, not a batch of tests followed by a batch of code.
- Test names read as capabilities ("user can checkout with valid cart"), not as internals ("checkout calls paymentService.process").
- Expected values in assertions are literals you can trace to the spec, not values recomputed the way the code computes them.
- Renaming an internal function breaks nothing in the suite.
- Mocks appear only at external boundaries (the payment API, the clock) and never around your own modules.

## Where it fits

`tdd` supplies test-first development for deterministic behaviour. [to-plan](https://aihero.dev/skills-to-plan) records the execution steps and low-cost checks; [implement](https://aihero.dev/skills-implement) carries out the plan and calls [code-review](https://aihero.dev/skills-code-review). [codebase-design](https://aihero.dev/skills-codebase-design) supplies the shared interface vocabulary. See [ask-matt](https://aihero.dev/skills-ask-matt) when unsure which skill fits.
