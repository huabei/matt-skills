---
name: ask-matt
description: Ask which retained skill fits your situation. A router over the skills in this repo.
disable-model-invocation: true
---

# Ask Matt

Recommend a skill from the retained set below, explain why it fits, and stop so the user can choose. Read the target SKILL.md before describing its behaviour or prerequisites. User-invoked skills are recommendations for the human to invoke, never instructions to invoke them yourself.

## Choose by situation

| Situation | Skill |
| --- | --- |
| Clarify an idea while maintaining shared project understanding | `/grill-with-docs`, combining `/grilling` and `/domain-modeling` |
| Discuss an idea without maintaining project docs | `/grill-me`, the wrapper around `/grilling` |
| Investigate code, dependencies, or official documentation | `/research` |
| Turn settled discussion into an execution plan | `/to-plan` |
| Execute a plan with correctness, efficiency, and low-cost checks | `/implement` |
| Investigate a specific failure and apply a supported local fix | `/diagnosing-bugs` |
| Build deterministic behaviour test-first using low-cost checks | `/tdd` |
| Review uncommitted changes for correctness and efficiency | `/code-review` |
| Design a module's interface or structure using project terminology | `/codebase-design` |
| Clarify project terminology or distinguish current and intended behaviour | `/domain-modeling` |
| Suggest evidence-based improvements to the agent's environment after a session | `/retro` |
| Transfer context to another session or workspace | `/handoff` |
| Learn a concept with a stateful teaching workspace | `/teach` |
| Re-explain a message that did not land | `/wait-what` |
| Write skills or agent instructions | `/writing-for-agents` |
| Optionally configure shared docs and execution plan locations | `/setup-matt-pocock-skills` |

## Current boundaries

The former `/to-spec` has been restored as `/to-plan`, which writes a local plan without implementing it. The ticket, triage, architecture-survey, PR-writing, UI-prototyping, and wizard skills have been removed. Recommend only skills present in this repo.

The retained skills are being adapted separately. `/implement` follows that plan, records progress, and performs low-cost correctness and efficiency checks; it does not run long training jobs or full experiments, and commits only on user request. `/implement` calls `/code-review` on its uncommitted changes. That review uses parallel Correctness and Efficiency reviewers and checks the plan where available; it reports findings without modifying code. Setup optionally records shared-document and plan conventions; it does not configure issue tracking. Explain these current constraints when recommending them; do not claim that they already run or analyse deep learning experiments.

`/diagnosing-bugs` uses bounded reproductions or existing artifacts to investigate specific failures and can apply supported local fixes. It distinguishes code defects from disappointing research outcomes and does not run long training or full experiments.

`/grilling` clarifies the current goal and necessary decisions, retains experiment-dependent questions, and waits for confirmation of shared understanding.

`/research` investigates code, dependencies, and official documentation in one background agent without further delegation, and records cited findings. It is not an experiment runner or a dedicated literature-review workflow. `/teach` currently builds a teaching workspace across sessions.

## Context boundaries

Continue in the current session while its context is useful. Use `/handoff` when context must travel to another session, directory, or collaborator. Read [PHASE-BOUNDARIES.md](PHASE-BOUNDARIES.md) when choosing between continuing, clearing, compacting, handing off, or using a subagent. Run `/retro` before discarding the session being reviewed, or provide its log.
