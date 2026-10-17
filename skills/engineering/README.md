# Engineering

Skills I use daily for code work.

## User-invoked

Reachable only when you type them (Claude Code: `disable-model-invocation: true`; Codex: `policy.allow_implicit_invocation: false` in `agents/openai.yaml`).

- **[ask-matt](./ask-matt/SKILL.md)**: Ask which skill or flow fits your situation. A router over the user-invoked skills in this repo.
- **[grill-with-docs](./grill-with-docs/SKILL.md)**: Grilling session that also builds your project's domain model, sharpening terminology and updating `GLOSSARY.md` and ADRs inline.
- **[setup-matt-pocock-skills](./setup-matt-pocock-skills/SKILL.md)**: Configure this repo for the engineering skills (issue tracker, triage labels, domain doc layout). Run once per repo.
- **[to-plan](./to-plan/SKILL.md)**: Turn the current conversation into a local execution plan with ordered steps, completion criteria, and low-cost validation.
- **[implement](./implement/SKILL.md)**: Execute a plan with correctness, computational efficiency, and low-cost validation, without long-running or full experiments.
- **[retro](./retro/SKILL.md)**: Suggest improvements to the coding agent's environment (navigation, automated checks, coding standards, steering files, tooling) after a session, most severe first.

## Model-invoked

Model- or user-reachable (rich trigger phrasing so the model can reach for them).


- **[diagnosing-bugs](./diagnosing-bugs/SKILL.md)**: Diagnose specific failures with bounded reproductions and evidence, apply supported local fixes, and report validation gaps without running full experiments.
- **[research](./research/SKILL.md)**: Investigate code, dependencies, and official documentation in a background agent, saving cited findings as a Markdown file in the repo.
- **[tdd](./tdd/SKILL.md)**: Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.
- **[domain-modeling](./domain-modeling/SKILL.md)**: Actively build and sharpen a project's domain model by challenging terms, stress-testing with scenarios, and updating `GLOSSARY.md` and ADRs inline.
- **[codebase-design](./codebase-design/SKILL.md)**: Shared discipline and vocabulary for designing deep modules: small interfaces, clean seams, testable through the interface.
- **[code-review](./code-review/SKILL.md)**: Review uncommitted changes for correctness and computational efficiency with parallel reviewers, checking the execution plan where available.
