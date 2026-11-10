# Engineering Judgment

**Practice thinking through code changes before AI gives you the answers.**

`engineering-judgment` is an AI skill that helps you make your own engineering decisions. You explain how you would build a feature. AI then reviews your reasoning and points out important things you missed.

The goal is to build the habit of asking useful questions before you change a codebase: What needs to happen? What could go wrong? Why choose this approach? How will I know it works?

With repeated practice, the aim is for you to notice these issues yourself. AI gives feedback after you try, so you keep practicing the thinking instead of handing every decision to AI.

Use **`$engineering-judgment`** on its own, or add it to your existing planning skill. Your planner still writes the plan. This skill does not write application code or start coding agents.

## How it works

Once the feature is clear, the assistant shows only these five categories:

1. **Requirements**
2. **Architecture**
3. **Failure Modes**
4. **Tradeoffs**
5. **Verification**

You write your own reasoning first. You can send all five answers together. The assistant waits until you finish before it gives questions, examples or advice, unless you ask for help.

AI then reviews your answers. It explains important gaps, risky assumptions and unnecessary complexity. You revise or confirm your choices before planning continues.

The assistant returns a short decision summary to your planner. The summary keeps your choices separate from AI suggestions and marks anything still undecided.

## Example: adding file uploads

Here is how the exercise could work when you add file uploads.

1. **You think first.** You explain what users can upload, how the upload should work, what might fail, which choices you made and how you would test it.
2. **AI reviews your attempt.** If you missed interrupted uploads or duplicate submissions, AI explains why those cases matter. AI does not assume every possible problem needs a complex solution.
3. **You make the next decision.** You revise your plan and explain how you will handle the problems that matter for your app.
4. **You can reflect after building.** Compare your original reasoning with what actually happened. What did you predict? What surprised you? What should you recognize next time?

The learning comes from making an attempt, receiving feedback and trying again. The goal is to help you recognize patterns such as partial work and repeated requests when planning a different feature later.

## Install in Codex

To install for your user account:

```sh
git clone https://github.com/ReazynCode/engineering-judgment.git ~/.agents/skills/engineering-judgment
```

If that directory already exists, inspect the existing installation before changing it; do not overwrite it blindly. You can alternatively clone elsewhere and link that checkout into a supported skill location. Keep one main copy so you know which files the assistant uses.

A Codex skill is a folder containing `SKILL.md` and any supporting files. Put a skill in `~/.agents/skills` to use it across projects, or in a project’s `.agents/skills` folder to keep it with that project. See the [official OpenAI skill documentation](https://learn.chatgpt.com/docs/build-skills) for the supported locations and ways to run skills. If a newly installed skill does not appear, restart Codex.

## Use directly

```text
$engineering-judgment
I want to reason through adding photo uploads to my app.
```

If you have already explained the feature, the assistant uses that context. Otherwise, it asks enough to understand the feature first. When you run this skill directly, it finishes with a decision summary and waits for your next instruction.

You control the exercise:

- **“Show me the CSV example”** displays the separate historical-stock-price CSV reference. It is never adapted into answers for the active feature automatically.
- **“Give me a small hint”** gives a small nudge.
- **“Explain it directly”** allows direct guidance, labeled as supplied rather than independent reasoning.
- **“Skip the exercise”** returns control to normal planning without inventing user decisions.

Small edits can skip or shorten the exercise. The planner reuses confirmed decisions for the same feature, so you do not have to repeat your answers at every step.

## Integrate with your existing planning skill

Add the instruction below to your planning skill. The planner should first understand the feature, then run this exercise before suggesting how to build it. The instructions tell the assistant when to pause and continue; they do not start a separate service.

```markdown
Once you understand the scope of a meaningful feature or design change,
run engineering-judgment before suggesting how to build it.

Use the available skill tool, or read the installed
engineering-judgment/SKILL.md and follow its instructions in this conversation.
Wait for the user's own reasoning before giving questions or advice.
After review, let the user revise or confirm their decisions.
Then continue normal planning using the decision summary.

Honor a request to skip. Shorten or skip the exercise for trivial changes.
Reuse confirmed decisions for the same feature.
Keep the existing planning process, agent roles and output location.
The summary alone does not give permission to implement or start coding agents.
```

Point the instruction at your installed `SKILL.md`. If both skills sit in the same parent folder, use `../engineering-judgment/SKILL.md`. Use the assistant’s skill tool when one is available. Otherwise, have the assistant read the file and follow it in the same conversation.

### Examples of integrations

| Your existing workflow | How to connect this skill |
| --- | --- |
| Feature interview or written specification | Run the exercise after the feature is clear, then continue writing the specification using your confirmed choices. |
| `grill-me` or another design interview | Pause its questions and recommended answers while you make your first attempt. Resume after review. |
| Architecture notes | Use the decision summary to record what you chose and why. Keep suggestions separate from decisions you accepted. |
| GitHub issues or task planning | Break the agreed plan into tasks. Keep open questions visible rather than treating them as settled. |
| Several coding agents | Give the agents your confirmed decisions through the existing coordinator. This skill does not start or authorize those agents. |
| Saved context or project notes | Keep your original attempt, revisions and decisions in your existing notes when you request it. The skill does not create another memory system. |

The first local integration used `interview` and `grill-me`, which calls the shared `grilling` skill. Those skills are not included in this repository. Add the instruction to your own planner without replacing its existing process. If several planners use the same underlying skill, adding the instruction there will affect all of them.

## Optional reflection

After implementation, ask to compare your original reasoning with actual outcomes. The assistant separates what you anticipated, missed and still cannot verify, then identifies a useful engineering principle to recognize next time.

A [Markdown log template](references/reflection-log-template.md) is included. Saving a log is optional: choose where it should go first. The skill does not create logs automatically or invent implementation results.

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | When to run, how the exercise works and how to return decisions to planning |
| [agents/openai.yaml](agents/openai.yaml) | The skill’s name, short description and suggested prompt in Codex |
| [CSV example](references/csv-example.md) | Optional reference, displayed only when requested |
| [Review rubric](references/review-rubric.md) | Guidance loaded after the first attempt |
| [Reflection template](references/reflection-log-template.md) | Optional log based on what actually happened |
| [Validation report](references/validation-report.md) | Checks performed and their limitations |
| [Forward-test transcripts](validation/forward-transcripts.md) | Simulated multi-turn behavior examples |

## Validation and limitations

The initial skill passed the Codex skill-creator format check. A separate reviewing agent also walked through simulated conversations covering the ten requested behaviors, direct use and reflection. These checks do not guarantee that every AI model will follow the instructions correctly. Read the [validation report](references/validation-report.md) for what was tested and what remains untested.

This skill is a set of instructions. It needs no extra API key, server or background process, though the AI tool you use may have its own cost. It does not change your application. Other AI tools may load skills differently; keep the same rule when adapting it: you think first, then AI reviews your attempt.
