---
name: research
description: Investigate a question against high-trust primary sources and capture the findings as a Markdown file in the repo. Use when the user wants code, dependencies, or official documentation investigated.
---

Spin up one **background agent** to do the research, so you keep working while it reads. Tell it to investigate directly without further delegation. If you are already a subagent, do the research yourself.

Its job:

1. Investigate the question against **primary sources** (the codebase, dependency source code, and official documentation), not a secondary write-up of them. Follow every claim back to the source that owns it.
2. Write the findings to a single Markdown file, citing each claim's source.
3. Save it where the repo already keeps such notes; match the existing convention, and if there is none, put it somewhere sensible and say where.
