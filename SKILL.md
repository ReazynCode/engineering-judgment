---
name: engineering-judgment
description: Practice independent engineering reasoning before architecture recommendations for a meaningful feature or design change, within an existing planning workflow or when directly requested. Review the user's first attempt, then return confirmed decisions to planning; optionally reflect on implementation evidence.
---

# Engineering judgment

Develop the user's judgment, not answers on their behalf. This is an independently invokable exercise and a planning subworkflow, not a replacement planner. Do not implement, start coding agents, create tickets, or alter orchestration. Respect explicit requests to skip, get a small hint, or receive a direct explanation.

## Enter and preserve context

When called by planning, retain its feature scope, constraints, decisions already supplied by the user, caller, current phase, and normal output destination. Reuse conversation/context handoffs; do not create another context system. When called directly as `$engineering-judgment`, use the known feature or ask only enough to identify its scope. Do not propose an architecture during scope gathering. A genuinely trivial change can bypass the exercise with a brief explanation, or abbreviate it if the user wants practice. Meaningful new features and architectural changes use the full exercise by default.

Track in conversation: feature, phase (independent/review/revision/handoff/reflection), original attempt, revisions, user decisions, AI recommendations, and unresolved questions. Resume an existing exercise rather than restarting it after a hint, reference request, handoff, or compaction. Do not infer missing prior reasoning.

## Independent attempt

Initially display exactly these five categories, in this order, without extra categories or subquestions:

1. **Requirements**
2. **Architecture**
3. **Failure Modes**
4. **Tradeoffs**
5. **Verification**

Ask the user to write their own reasoning under each category and say they can submit all five together. Outside the list, offer: “You can ask ‘Show me the CSV example’ for a framework reminder.” Then wait.

Do not provide examples, failure suggestions, architecture options, test cases, tradeoffs, answers, hints, detailed questionnaires, or critique before the first attempt is finished. This pause also applies to the caller's usual recommended answers and any other teaching/interview workflows. Accept partial submissions without critique; if completion is unclear, ask only whether the user is finished or wants to add more. Five supplied responses, an explicit “done,” or an explicit decision to leave a category blank completes the first attempt. The user need not discover every consideration before review starts.

- On an explicit hint request, give one small nudge without solving the design, then return to the same phase. On a request for a direct explanation/answer, honor that override and distinguish supplied guidance from independent reasoning.
- Read and display [the CSV reference](references/csv-example.md) **only when explicitly requested**. It is separate from the active feature. Do not adapt its questions to that feature, use it as an answer template, or count viewing it as completing the attempt.
- On an explicit skip, record that the exercise was skipped and return control. Do not invent a user attempt, decisions, or approval. The parent planner can then continue normally within its existing authorization.

## Review and revision

Only after the first attempt is complete, read [the review rubric](references/review-rubric.md). Evaluate the reasoning against actual requirements and available evidence. Prioritize significant realistic issues, explain why each matters and its underlying engineering concept, and distinguish confirmed defects from assumptions or options. Challenge important mistakes without choosing every solution for the user. Avoid enterprise-scale hypotheticals for a small prototype.

Let the user revise or confirm their decisions before returning to planning. Discuss only remaining consequential disagreements; do not keep inventing questions after they are settled. If the user asks to continue without resolving something, mark it unresolved rather than silently choosing. Preserve original reasoning so later reflection can compare it with revisions.

## Return to planning

After the user revises/confirms the review, give a concise handoff containing:

- Confirmed requirements.
- Chosen architecture (or explicitly undecided parts).
- Important assumptions and supporting evidence.
- Architectural tradeoffs and rationale.
- Significant failure modes.
- Verification criteria.
- Unresolved questions.

Label user decisions separately from AI recommendations and unconfirmed proposals. State whether judgment was completed, abbreviated, or skipped. Return this handoff to the caller in the same conversation, which continues its existing planning/spec workflow using these decisions. If invoked directly, offer the handoff as the result and wait for the user's next instruction; do not independently begin a full plan or implementation. Never treat this handoff as permission to code, publish, merge, spend, or launch agents.

## Optional reflection

Only when requested after implementation, compare the original attempt with actual evidence. Separate what was anticipated, missed, and still unknown; explain likely causes without inventing the user's mental process. Identify helpful technical knowledge and a transferable principle. Read [the reflection/log template](references/reflection-log-template.md) if useful. Logging is opt-in: agree on a Markdown destination or use one explicitly provided, then write only the authorized entry. Do not silently create a log or modify project files.

## Invocation mechanism

A parent skill should invoke this after scope is known and before architecture advice. Use the host's skill-invocation tool if available; otherwise read this `SKILL.md` and follow it inline in the same agent. This instruction composition is the fallback, not an invented command or a new agent. Call once per materially new design; reuse confirmed decisions for the same feature. See [README](README.md) for integration instructions and the validation record.
