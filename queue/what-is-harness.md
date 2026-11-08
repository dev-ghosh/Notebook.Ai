# What is a Harness (in AI)?

## TL;DR
**A harness is everything built around an AI model that lets it do real work instead of just producing text.** The model is the brain. The harness is the body: the hands (tools), the memory, the rules, and the loop that keeps it working until the job is done.

Claude Code is a harness. So are Cursor's agent mode, GitHub Copilot's agent mode, and OpenAI's Codex CLI. Different harnesses can use the same model and still behave very differently.

---

## Simple analogy
A strong horse is powerful, but it goes nowhere useful without a **harness**: the straps and reins that let a person steer it and attach a cart.

An AI model is the same. It is very capable at reasoning and writing, but on its own it can only take text in and give text out. The harness connects that power to the real world and keeps it under control.

Another way to see it: **model = engine, harness = the rest of the car** (steering, brakes, dashboard, fuel line).

## What is inside a harness?
| Part | What it does | Example |
|---|---|---|
| **Instructions (system prompt)** | Tells the model its role, rules, and style | "You are a coding assistant. Never delete files without asking." |
| **Tools** | Lets the model act: read files, search the web, run code, call APIs | Read, Edit, Bash, web search |
| **The loop** | Repeats: think -> use a tool -> look at the result -> think again, until done | Fix a bug, run tests, see failure, fix again |
| **Context and memory** | Decides what the model can "see" and remember, and trims it when it gets too long | `CLAUDE.md` project notes, conversation summaries |
| **Permissions and safety** | Asks before risky actions and blocks forbidden ones | "Allow this command?" prompts |
| **Orchestration** | Hands work to helpers and combines results | Subagents |

## How it works (one request, step by step)
```text
You: "Fix the failing login test."
 1. Harness sends your request + instructions + tool list to the model.
 2. Model replies: "Let me read the test file."  (a tool request)
 3. Harness runs the tool, checks permissions, returns the file contents.
 4. Model reads it, decides to edit code.  -> harness applies the edit.
 5. Model asks to run the tests.           -> harness runs them, returns output.
 6. Repeat until tests pass, then the model reports back.
```
The model never touches your computer directly. **The harness does the touching** and reports back.

## Why does it matter?
- **Same model, different results.** A bare model and the same model inside a good harness are very different experiences.
- **Reliability.** The harness handles retries, mistakes, and long tasks that would otherwise fall apart.
- **Safety.** Permission checks and limits live in the harness, not in the model.
- **Cost and speed.** How the harness manages context and tool calls affects both.

## Other names you may hear
People use these loosely and they overlap: **agent harness**, **scaffold**, **agent framework**, **runtime**. There is no single official definition, but they all point to the same idea: the software around the model.

## Quick recap
- Harness = the software that wraps a model: tools + loop + memory + rules.
- Model thinks; harness acts.
- Claude Code, Cursor, Codex CLI and similar tools are harnesses.
