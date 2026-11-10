# Engineering Judgment

**Build your engineering instincts before AI supplies the architecture.**

`engineering-judgment` is a reusable AI skill that adds an independent-thinking exercise to an existing feature-planning workflow. It also works directly as **`$engineering-judgment`**. It does not replace your planner, write implementation code, or launch coding agents.

## How it works

Once the feature scope is clear, the assistant shows five lenses:

1. **Requirements**
2. **Architecture**
3. **Failure Modes**
4. **Tradeoffs**
5. **Verification**

You write your own reasoning first—all five answers can be submitted together. The assistant waits rather than supplying subquestions, architectures or failure examples. After your first attempt, it reviews important gaps, weak assumptions and overengineering, explains why they matter, and lets you revise or confirm your choices.

The result is a handoff to your original planner containing confirmed requirements, architecture, assumptions, tradeoffs and rationale, failure modes, verification criteria and unresolved questions. Your decisions remain distinct from AI recommendations.

## Install in Codex

For a fresh user-level installation:

```sh
git clone https://github.com/ReazynCode/engineering-judgment.git ~/.agents/skills/engineering-judgment
```

If that directory already exists, inspect the existing installation before changing it; do not overwrite it blindly. You can alternatively clone elsewhere and link that checkout into a supported skill location. Keep one canonical copy to avoid editing a different installation from the one your host loads.

Codex skills use a directory with `SKILL.md` and optional supporting files. User-level skills can be discovered under `~/.agents/skills`; repository-scoped skills can live under `.agents/skills`. See the [official OpenAI skill documentation](https://learn.chatgpt.com/docs/build-skills) for current discovery and invocation conventions. If a newly installed skill does not appear, restart the host as the documented fallback.

## Use directly

```text
$engineering-judgment
I want to reason through adding photo uploads to my app.
```

Known scope is reused. If the feature is unclear, the assistant gathers enough scope before starting. Direct invocation returns a decision handoff and waits for your next instruction; it does not automatically start an implementation plan.

You control the exercise:

- **“Show me the CSV example”** displays the separate historical-stock-price CSV reference. It is never adapted into answers for the active feature automatically.
- **“Give me a small hint”** gives a small nudge.
- **“Explain it directly”** allows direct guidance, labeled as supplied rather than independent reasoning.
- **“Skip the exercise”** returns control to normal planning without inventing user decisions.

Trivial edits can skip or abbreviate the exercise. Confirmed decisions for the same feature are reused instead of repeating the exercise at every planning step.

## Integrate with your existing planning skill

Add a short instruction block to your planner after scope gathering and before architectural recommendations. This is instruction composition, not an executable callback or a server integration.

```markdown
After establishing scope for a meaningful new feature or architectural change,
invoke engineering-judgment before detailed design questions, recommended
answers, architecture proposals or an implementation plan.

If the host has no skill-invocation tool, read the installed
engineering-judgment/SKILL.md and follow it inline in the same agent.
Pause normal recommendations while the user makes their independent attempt,
then review and allow revision or confirmation. Resume this planning workflow
using the resulting decision handoff. Honor explicit skips and trivial-change
bypasses. Reuse a completed handoff for the same feature.

Keep the existing scope, context, orchestration and output destination.
Do not treat the handoff as authorization to implement or launch coding agents.
```

Resolve the file reference to your actual installation. For sibling installed skills, a relative link such as `../engineering-judgment/SKILL.md` is sufficient. On a host with native skill invocation, invoke it through that mechanism; do not invent a `Skill` tool if none exists.

### Examples of integrations

| Existing workflow | Where judgment fits | What remains unchanged |
| --- | --- | --- |
| Feature interview / PRD or spec authoring | After scope, before detailed design advice | Original interview, document destination and spec format |
| `grill-me` or a design-review planner | Before its recommended answers or architecture critique | Existing routing and later decision-tree process |
| Architecture decision records | Use the confirmed handoff as input after the exercise | ADR format and approval process; AI recommendations stay labeled |
| Ticket breakdown | Feed the agreed spec and handoff into ticket planning | Ticket tooling and acceptance-criteria workflow; unresolved decisions remain visible |
| Multi-agent implementation | Give an already-authorized orchestrator the confirmed decisions downstream | Existing worker roles, branches, reviews and authorization boundaries |
| Context handoffs or notes | Preserve the current phase, original attempt and confirmed decisions | Existing context system; no duplicate memory or silent project-file writes |

The initial local integration was tested with `interview` and `grill-me` via its existing `grilling` engine. Those third-party skills are **not bundled or replaced** by this repository. Put the hook in the shared engine if that is the appropriate entry point; document that other callers of the engine inherit it too.

## Optional reflection

After implementation, ask to compare your original reasoning with actual outcomes. The assistant separates what you anticipated, missed and still cannot verify, then identifies a useful engineering principle to recognize next time.

A [Markdown log template](references/reflection-log-template.md) is included. Logging is opt-in: provide or agree on a destination first. The skill does not create logs automatically or invent implementation results.

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Activation, exercise, review, handoff and user controls |
| [agents/openai.yaml](agents/openai.yaml) | Codex-facing display metadata; implicit invocation uses the default policy |
| [CSV example](references/csv-example.md) | Optional reference, displayed only when requested |
| [Review rubric](references/review-rubric.md) | Guidance loaded after the first attempt |
| [Reflection template](references/reflection-log-template.md) | Optional evidence-based learning log |
| [Validation report](references/validation-report.md) | Checks performed and their limitations |
| [Forward-test transcripts](validation/forward-transcripts.md) | Simulated multi-turn behavior examples |

## Validation and limitations

The initial skill passed the Codex skill-creator format validator and an independent simulated walkthrough covering the ten requested behaviors, plus direct use and reflection. This was not an end-to-end test of every host or future model response. Read the [validation report](references/validation-report.md) for the precise evidence and limits.

No API key, MCP server, paid provider, background service or implementation-agent framework is required by this instruction-only skill. It does not change your application's runtime. Other AI hosts may interpret skill discovery and invocation differently; adapt only the loading mechanism while retaining the independent-attempt boundary.
