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
| Investigate source code or technical primary sources | `/research` |
| Implement a concrete change | `/implement` |
| Diagnose a bug or performance regression | `/diagnosing-bugs` |
| Build a deterministic behaviour test-first | `/tdd` |
| Review changes against a fixed point | `/code-review` |
| Design a module's interface or structure | `/codebase-design` |
| Clarify terminology or record a decision | `/domain-modeling` |
| Improve the agent's environment after a coding session | `/retro` |
| Transfer context to another session or workspace | `/handoff` |
| Learn a concept with a stateful teaching workspace | `/teach` |
| Re-explain a message that did not land | `/wait-what` |
| Write skills or agent instructions | `/writing-for-agents` |
| Configure project conventions for the retained engineering skills | `/setup-matt-pocock-skills` |

## Current boundaries

The spec, ticket, triage, architecture-survey, PR-writing, UI-prototyping, and wizard skills have been removed. Recommend only skills present in this repo.

The retained skills are being adapted separately. At present, `/implement` still accepts a spec or tickets, invokes TDD where possible, reviews, and commits. `/code-review` still has Standards and Spec axes and expects an issue tracker. Setup still configures tracker and domain conventions. Explain these current constraints when recommending them; do not claim that they already run or analyse deep learning experiments.

`/research` investigates primary sources and records cited findings. It is not an experiment runner or a dedicated literature-review workflow. `/teach` currently builds a teaching workspace across sessions.

## Context boundaries

Continue in the current session while its context is useful. Use `/handoff` when context must travel to another session, directory, or collaborator. Read [PHASE-BOUNDARIES.md](PHASE-BOUNDARIES.md) when choosing between continuing, clearing, compacting, handing off, or using a subagent. Run `/retro` before discarding the session being reviewed, or provide its log.
