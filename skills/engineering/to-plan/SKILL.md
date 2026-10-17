---
name: to-plan
description: "Turn the current conversation into a local execution plan: no interview, just synthesis of what you've already discussed."
disable-model-invocation: true
---

This skill takes the current conversation and codebase understanding and produces an **execution plan**. Synthesize what is already settled; do not reopen the design or invent decisions. Record unresolved implementation questions explicitly. Questions whose answers depend on full experiments do not block code changes that are already clear.

## Process

1. Explore the relevant code and configuration if you haven't already. Trace the current behaviour, data flow, and invariants. Use the project's glossary vocabulary and respect existing decisions.

2. Break the change into ordered steps, each with a concrete deliverable and completion criterion. Name dependencies when ordering alone is not enough. Ground the steps in actual code paths and existing helpers; include paths or short mathematical expressions where they make a decision precise.

3. Account for correctness and computational efficiency. Identify the affected numerical behaviour, gradients, interfaces, and compatibility constraints. Consider compute and memory at the intended workload size, including synchronization and data movement. Distinguish agreed choices from assumptions and unmeasured expectations.

4. Define low-cost checks for the changed paths, using the repo's existing tooling where possible. Bound execution by steps, input size, or duration. Separate implementation checks from questions requiring long training or full experiments.

5. Write the plan using the template below. Use the user's path or the repo's established plan location; otherwise save to `plans/<slug>.md`. Update an existing plan only when it is clearly the same effort, preserving its progress and evidence. Report the path and unresolved decisions, then stop. Planning does not modify implementation code or start experiments; the user invokes `/implement` when ready.

<plan-template>

## Goal

The requested behaviour and why it is needed.

## Current Implementation

Relevant code paths, existing mechanisms, and constraints. Reference existing research notes rather than copying them.

## Implementation Decisions

The agreed approach, mathematical meaning, interfaces, and compatibility requirements. Explain material compute and memory tradeoffs at the intended workload size. Label assumptions and decisions that remain open.

## Execution Steps

An ordered checklist. For each step, state:

- What changes and where, including dependencies if needed.
- The completion criterion.
- The low-cost check that verifies it, with an execution bound where applicable.

Mark a step blocked if an unresolved decision prevents implementation; do not present a guess as an agreed choice.

## Validation

Checks across the completed change, expected outcomes, and required hardware or data. A short performance comparison must state its workload and timing conditions; code inspection alone does not establish a speedup.

## Out of Scope

Work excluded from this change, including long-running training and full experiments.

## Open Questions

Separate unresolved implementation decisions from scientific questions that require later experiments. State what evidence would resolve each.

</plan-template>
