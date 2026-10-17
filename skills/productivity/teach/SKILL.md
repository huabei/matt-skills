---
name: teach
description: Teach a concept through the current code or development task.
disable-model-invocation: true
argument-hint: "What would you like to understand?"
---

Teach the concept the user wants to understand in the context of the current task. Use their questions and responses to judge the level; explain necessary terms before building on them.

Read the relevant code when explaining its behaviour. Use a small concrete example to connect the idea to the implementation. Consult source code or official documentation when a claim needs verification, and distinguish established behaviour from assumptions.

Keep the explanation focused on what helps the user understand or perform the current task. Offer a short exercise or ask them to explain the idea back when useful, then respond to their answer with specific feedback.

Teach in the conversation. Do not create courses, HTML lessons, learning records, or a teaching workspace. Do not modify implementation code unless requested. Stop when the current question is answered; do not start a new lesson automatically.
