# Loop (Engineering) vs Prompt Engineering

> **Assumption:** I read "loop" as *loop engineering*, the idea of designing the cycle that keeps an AI agent working and checking itself. This also covers the `/loop` command in Claude Code. If you meant something else, tell me and I will redo this file.

## TL;DR
- **Prompt engineering** = writing **one good instruction** so the AI gives a good answer.
- **Loop engineering** = building a **cycle** around the agent: do the work, **check the result**, decide the next step, repeat until done. You stop being the person who prompts every turn.

Short version: *prompt engineering improves a single message; loop engineering improves the whole process.*

---

## Simple analogy
- **Prompt engineering** = giving a very clear task to a new colleague.
- **Loop engineering** = setting up a system where that colleague works, **tests their own work**, fixes issues, and only comes back to you when it is genuinely done (or stuck).

## What each one focuses on
| | Prompt engineering | Loop engineering |
|---|---|---|
| Unit of work | One message | A repeating cycle |
| Main question | "How do I phrase this so it works?" | "How does this run, check itself, and stop?" |
| You do | Write the instruction | Design the goal, check, memory, and limits |
| Who decides the next step? | You, after reading each reply | The loop |
| Verification | You read the answer | A test, command, or checker confirms it |
| Good for | Single answers, writing, analysis | Long or repeating tasks, code that must pass tests |
| Main risk | Vague or wrong answer | Runaway cost, fake "done", unsafe actions |

## The parts of a good loop
1. **Goal with a checkable finish line.** "All tests pass" (a command can confirm it) beats "make the code better".
2. **Verification.** Judge "done" using evidence (test output, exit codes), not the AI's own claim.
3. **Memory outside the chat.** Keep progress in a file (e.g. `PROGRESS.md`) or git history so work survives across rounds.
4. **Limits.** A maximum number of attempts, then hand back to a human.

## Example: "Make all tests pass"

**Prompt engineering approach**
> You write: "Fix the failing tests. Do not change the tests. Explain each fix."
> You read the answer, run the tests, and send the next prompt if something fails.

**Loop approach**
```text
Goal: all tests pass.
Repeat (max 10 rounds):
  1. Run the test command.
  2. If everything passes -> stop and report.
  3. If not -> read the failures, fix the code, note progress in PROGRESS.md.
If still failing after 10 rounds -> stop and ask a human.
```
You are no longer in the middle. The loop supplies the "run it, see what failed, try again" step.

## The `/loop` command in Claude Code
`/loop` re-runs a prompt on a repeating schedule while a session is open. For example:

```text
/loop 5m check my pull request, address review comments, and fix any failing CI
```
- It decides **when** to run, not whether the goal was achieved.
- On its own it has **no built-in "done" check**. Pair it with real verification (tests, a goal condition) so it knows when to stop.
- It runs locally, so it stops if your computer shuts down or the session closes.

## Risks and how to handle them
| Risk | What it looks like | Fix |
|---|---|---|
| **Cost** | Repeated runs use many tokens | Cap iterations, use cheaper models for simple checks |
| **Gaming the check** | The AI edits the tests to make them pass | Forbid editing tests, review the diff |
| **Prompt injection** | A web page or issue contains hidden instructions | Limit permissions, ask before irreversible actions |
| **Unverifiable goals** | Vague goal, so the loop says "done" without proof | Use a measurable finish line |
| **No oversight** | Mistakes pile up while you are away | Review the results, keep a human approval step |

## Do you still need prompt engineering?
**Yes.** Each round of a loop still runs on a prompt. Loop engineering sits **on top of** prompt engineering (and the harness around the model); it does not replace it. A weak prompt in a loop just fails repeatedly and costs more.

## When to use which
- **Prompt engineering:** one-off tasks, writing, questions, brainstorming.
- **Loop engineering:** tasks you can verify automatically, work that repeats, long jobs you want to hand off.

## Quick recap
- Prompt engineering = a good instruction.
- Loop engineering = a good *process*: act, check, repeat, stop.
- A loop needs a measurable goal, real verification, saved progress, and limits.
- You need both.
