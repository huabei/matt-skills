## What it does

`setup-matt-pocock-skills` records where project terminology, decisions, and execution plans live and how agents use them. It preserves existing conventions and shows proposed changes for confirmation before writing.

Setup is optional. Other skills can follow existing instructions and their own defaults without running it first.

## When to reach for it

You invoke this by typing `/setup-matt-pocock-skills`; the agent will not reach for it on its own. Use it to establish shared document locations or update conventions in an existing repository.

## Prerequisites

Run it in the repository you want to configure. It updates `docs/agents/domain.md` and the appropriate existing `AGENTS.md` or `CLAUDE.md`, following shared-file and symlink arrangements. If the correct instruction file is unclear or neither exists, it asks which to use.

## Conventions, not scaffolding

Existing locations take precedence. Without an established convention, it proposes a root `GLOSSARY.md`, `docs/adr/`, and `plans/`. Glossary entries and ADRs are created only when there is something to record, rather than as empty files during setup.

The instruction file tells agents to read relevant terminology and decisions and records where execution plans belong. It describes the user-invoked planning and implementation steps without starting them. Existing documents and unrelated instructions are preserved.

## Common questions

**Must I run setup before the other skills?**

No. It makes conventions explicit but is not a prerequisite.

**Does it configure issues, labels, or experiment infrastructure?**

No. It only configures shared documents and execution plan conventions.

**What happens to documents from an older setup?**

They are not automatically deleted. You can review them separately if they no longer serve a purpose.

## It's working if

- Document locations match existing project conventions where they exist.
- You see and confirm the proposed changes before files are written.
- The instruction file used by your agent points to the relevant documentation and plan location.
- Existing user content and skill files remain intact.

## Where it fits

This is optional setup for [domain-modeling](https://aihero.dev/skills-domain-modeling) and the [to-plan](https://aihero.dev/skills-to-plan) to [implement](https://aihero.dev/skills-implement) workflow. See [ask-matt](https://aihero.dev/skills-ask-matt) for the map.
