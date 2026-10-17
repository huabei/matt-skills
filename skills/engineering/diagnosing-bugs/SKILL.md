---
name: diagnosing-bugs
description: "Diagnose hard bugs, training anomalies, and performance regressions. Use when the user asks to debug or diagnose a specific failure that needs investigation."
---

Diagnose the reported symptom using evidence, then apply a supported local fix. A disappointing research metric alone is not proof of a code defect. Keep investigation and validation low-cost; do not launch long training jobs or full experiments.

## Process

1. Read the report, relevant code and configuration, existing logs, and project terminology. Identify the exact symptom, expected behaviour, and known-good comparison where available. Reuse prior investigation. Redact secrets and sensitive data from commands, outputs, and captured artifacts before sharing them.

2. Build a **tight feedback loop** that detects the actual symptom. Prefer a focused test, small batch, saved input or checkpoint, or bounded comparison with a trusted implementation. Pin relevant seeds and record software and hardware conditions; seeds alone do not guarantee deterministic GPU execution. Bound retries by steps, input size, or duration and report reproduction frequency for intermittent failures.

   If reproduction requires unavailable hardware or expensive execution, investigate the code and existing artifacts instead. State what could not be reproduced and distinguish observed facts from hypotheses. Request only the missing evidence needed to distinguish causes; do not invent a substitute failure and claim it reproduces the report.

3. Reduce the reproduction enough to distinguish plausible causes, preserving the reported failure. Form evidence-supported, falsifiable hypotheses and state what observation would distinguish them. Do not force a fixed number of hypotheses or minimize beyond what helps the investigation.

4. Test the hypotheses with targeted probes, changing one variable at a time. Tag temporary instrumentation so it can be removed. For numerical failures, inspect the affected values and gradient path. For performance regressions, measure a comparable baseline before attributing a cause: match workload, device, and dtype, account for warmup and asynchronous accelerator execution, and check relevant memory costs. Keep inspection-based risks separate from measured regressions.

5. Apply a local fix when evidence supports the cause. Preserve intended mathematics and experimental semantics. Discuss changes to the algorithm, mathematical meaning, compatibility, material resource tradeoffs, or broad structure before proceeding; update an existing execution plan or recommend that the user run `/to-plan` where a new plan is needed.

   Turn the reproduction into a failing regression test before the fix when a meaningful low-cost test is available, then check that it passes after the fix. Otherwise record the verification gap without assuming it is an architecture defect. Rerun the bounded reproduction and relevant checks; an unreproduced original failure must not be reported as a verified fix.

6. Remove only the temporary instrumentation and artifacts introduced for this investigation, preserving user files and experiment outputs. Report the cause or remaining hypotheses, evidence, changes, checks, and unresolved validation. If the original full-scale scenario was not rerun, say so. Update an existing plan when relevant. Commit or push only on user request.
