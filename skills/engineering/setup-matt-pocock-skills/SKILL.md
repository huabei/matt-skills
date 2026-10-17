---
name: setup-matt-pocock-skills
description: "Configure where project terminology, decisions, and execution plans live and how agents use them."
disable-model-invocation: true
---

Configure this repo's document conventions. Setup is optional; the other skills can use existing conventions without it. Explore, present the proposed changes, confirm with the user, then write.

## Process

1. Read existing `AGENTS.md` / `CLAUDE.md`, `GLOSSARY.md` / `GLOSSARY-MAP.md`, relevant ADRs, `docs/agents/`, and execution plans. Preserve established locations and instructions. If no convention exists, use a root `GLOSSARY.md`, `docs/adr/`, and `plans/`. Keep existing multi-context layouts; do not introduce one without a demonstrated need.

2. Propose the document locations and the instruction-file changes. Prefer the instruction file used by the current agent; follow existing shared-file or symlink arrangements without duplicating instructions. If the appropriate file is unclear or neither exists, ask which to edit or create. Show the draft and obtain confirmation before writing.

3. Write `docs/agents/domain.md`, adapting [domain.md](domain.md) to the agreed glossary and ADR locations. Record the execution plan location and these usage rules in the chosen instruction file's `## Agent skills` section:

   - Read relevant glossary definitions and ADRs when exploring code; missing documents do not block work.
   - Use `to-plan` to capture settled discussion in the agreed plan location. Use `implement` to execute the selected plan and record progress and validation there. These are user-invoked steps, not automatic calls.

   Update existing instructions in place, preserving unrelated user content. Create glossary entries and ADRs lazily through `domain-modeling`, not as empty scaffolding. Do not delete existing documents from an earlier setup merely because this version no longer configures them.

4. Report the files changed and the agreed conventions. The user can edit them directly; rerun setup only when the conventions need to change. Do not modify the skills themselves.
