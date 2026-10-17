> **Customization note.** Links marked archived describe removed skills and their former workflows. They are historical context, not available steps in this fork. Retained skills will be adapted separately.

## What it does

`research` answers a question by reading the sources that own the answer, then leaves a cited Markdown file in the repo. It works only from **[primary sources](https://www.aihero.dev/ai-coding-dictionary/primary-source)**: the codebase, dependency source code, and official documentation. It follows every claim back to the source that owns it, so it will not repeat a blog post's account of an API when the API's own docs are reachable.

It does not answer you in the conversation. The output is a file, written where the repo already keeps such notes, with a link on each claim. You get a document you can react to, hand to another agent, or throw away, rather than an answer that is gone when the [session](https://www.aihero.dev/ai-coding-dictionary/session) ends.

## When to reach for it

Type `/research`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it automatically when a task turns into reading legwork.

Reach for it when the next step is *finding something out* about code or dependencies (how the current implementation works, how a library API behaves, whether a version claim holds), and you'd rather not stall your own thread doing the reading. What you need decides which skill:

| What you need | Reach for |
| --- | --- |
| A code or dependency fact a decision is waiting on | `research` |
| A decision made *with* you, by interview | [grilling](https://aihero.dev/skills-grilling) |
| A durable architecture decision, written into `GLOSSARY.md` and ADRs | [grill-with-docs](https://aihero.dev/skills-grill-with-docs) |
| To find out whether an approach works in your codebase | [prototype (archived)](https://aihero.dev/skills-prototype) |
| A plan too big to hold in one session | [wayfinder (archived)](https://aihero.dev/skills-wayfinder) |

The line between `research` and `grill-with-docs` is the **shelf life of what comes back**. Research produces short-lived facts, such as what this library's auth mechanism does as of this week. An ADR records a decision you keep. If what you are producing is a decision rather than a fact, you are [grilling](https://www.aihero.dev/ai-coding-dictionary/grilling), not researching.

## Delegated legwork

The reading runs as a **background agent**. You keep working while it follows each claim to its primary source, writes one Markdown file, and reports back. Research is legwork you delegate, not thinking you outsource. You get a document to grill, plan, or design against, and you still make the decision.

The background agent investigates directly without further delegation. If this skill is reached inside a subagent, that agent does the research itself.

The repo decides where the file goes, not the skill. It follows whatever convention already exists for notes. If there is none, it picks a sensible place and tells you where. It writes one file per run.

## Common questions

**Does the research agent delegate again?**

No. The caller starts one background agent with instructions to investigate directly. An agent already running as a subagent does the research itself.

**Where should the file live, and should I commit it?**

The skill puts the file where the repo already keeps notes and has no further opinion. The community view is mostly settled: keep ADRs, not research files. One Discord thread on this question put it most clearly: "ADRs yes. Everything else archive or delete after done. It otherwise becomes cruft of work and can poison future repo reads if you've drifted away from the spec/research." A research file records what was true on the day it was written, so a stale one is worse than none. On balance, these files don't belong in git, and there is no standard home for them. People use Obsidian, a separate knowledge repo, or the issue tracker instead.

**What counts as a "high-trust" primary source, and who decides?**

The [model](https://www.aihero.dev/ai-coding-dictionary/model) does. The skill names the *kinds* of source that qualify (official docs, source code, specs, first-party APIs), and there is no allowlist, no domain gate, and no verification pass. This was the loudest objection when the skill was first proposed, and nobody has answered it publicly: "Five research subagents pointed at junk just gives you five confident wrong answers faster. How are you gating what counts as high-trust sources?" Your only protection is the citation on each claim. Follow two or three of them. If they land on a summary of the thing rather than the thing, the run failed.

**Does a later session reuse what an earlier run found?**

No. Nothing loads a past research file automatically. The file stays in the repo until a human or a skill points at it. This was the strongest early challenge to the design: "the value's the markdown becoming context the agent re-reads later, not the fetch itself. A write-once dead file is just a fancy search." The shipped skill does not solve it. In practice, the file is useful only when you feed it into the next step yourself: attach it to a spec, quote it into a grilling session, point a [ticket](https://www.aihero.dev/ai-coding-dictionary/ticket) at it.

**Why not just ask the agent to go read the docs?**

You can, and a two-line prompt saying exactly that was the practice this skill replaced. The skill gives you two things the prompt does not. It runs in the background, so your session's [context](https://www.aihero.dev/ai-coding-dictionary/context) stays clean. And the primary-source constraint and the cited-file output are the same every time, rather than depending on how you phrased the prompt. Compared with a [harness](https://www.aihero.dev/ai-coding-dictionary/harness)'s own deep-research mode, the difference is the file and the primary-source rule, not the search. If a two-line prompt gets you what you need on a small question, use the two-line prompt.

**When does it stop reading?**

The skill has no stopping criterion. This shows up as two complaints that look opposite but have the same cause: agents that go far too deep, and agents that cover a topic broadly but miss the one detail that mattered. One practitioner put it as "deep-research skills are a bit too deep sometimes. And telling an agent to research usually results in missing crucial details." You have to set the scope. A narrow, answerable question (one API, one behaviour, one version claim) comes back far better than "research X".

## It's working if

- Your own session keeps going. If you are sitting watching it read, the delegation didn't happen.
- The caller starts one background task; a subagent performs the research directly without nesting.
- One new Markdown file shows up, in the folder the repo already uses for notes, and the agent tells you the path.
- Every claim in it carries a link, and following two at random lands you on official documentation or the source file itself, not on someone's write-up of it.
- You can make the decision you were stuck on from the file alone, without going back to the sources yourself.

## Where it fits

`research` is a reach-for-it-anytime standalone. Its cited findings inform [grill-with-docs](https://aihero.dev/skills-grill-with-docs) and [to-plan](https://aihero.dev/skills-to-plan). It investigates code and technical documentation; dedicated literature research belongs to other skills. See [ask-matt](https://aihero.dev/skills-ask-matt) for the map.
