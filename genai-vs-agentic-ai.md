# Generative AI vs Agentic AI

## TL;DR
- **Generative AI (Gen AI)** *creates content* (text, images, code, audio) when you prompt it.
- **Agentic AI** *pursues a goal*: it plans, uses tools, takes actions, checks the results, and keeps going until the job is done.

Agentic AI usually uses Gen AI as its "brain", then adds planning, tools, memory, and the ability to act.

---

## Simple analogy
- **Gen AI** = a talented writer. You ask for something, and it hands you a draft.
- **Agentic AI** = a project manager. You give it a goal, and it gets people (tools) to do the steps and reports back when finished.

## Example 1: Customer support
**Gen AI:** you paste a customer complaint, and it writes a polite reply draft. You send it yourself.

**Agentic AI:** it reads the ticket, checks the order in the company system, sees the package is late, issues a refund (within the rules it was given), sends the reply, and closes the ticket. If the case is unusual, it hands it to a human.

## Example 2: Marketing launch
**Gen AI:** writes the launch email, social posts, and a banner image when you ask for each one.

**Agentic AI:** researches the audience, drafts the content, schedules the posts, watches how they perform, and adjusts the plan based on results.

## Example 3: Software
**Gen AI:** you ask for a function, and it writes the code in the chat.

**Agentic AI** (like Claude Code or Google's Jules): you say "add dark mode." It explores the codebase, edits several files, runs the tests, fixes failures, and opens a pull request.

## Comparison
| | Generative AI | Agentic AI |
|---|---|---|
| Main job | Create content | Achieve a goal |
| Input | A prompt | A goal |
| Steps | Usually one response | Many steps in a loop |
| Tools and actions | Usually none | Uses tools, apps, and APIs |
| Memory and planning | Limited | Plans and remembers progress |
| Human involvement | You guide each step | You supervise and approve key actions |
| Output | Text, image, code, audio | A finished outcome (task done) |
| Main risk | Wrong or made-up content | Wrong *actions*, and errors that pile up across steps |

## How they relate
```text
Agentic AI = Gen AI (the brain)
           + Planning (what to do next)
           + Tools (search, files, apps, code)
           + Memory (what's done so far)
           + A loop: plan -> act -> check -> repeat
```

So agentic AI does **not replace** Gen AI. It is built on top of it.

## When to use which
- **Gen AI:** drafting, brainstorming, summarising, quick answers, one-off creative work.
- **Agentic AI:** multi-step, repeatable tasks where the AI has to look things up and act (support workflows, research, coding tasks, data clean-up).

## Good practice with agents
- Give clear goals and limits.
- Give only the permissions needed.
- Keep a human approval step for risky actions (payments, deleting data, sending messages).
- Review the results, especially early on.

## Quick recap
- Gen AI = creates.
- Agentic AI = acts toward a goal.
- Agentic AI is Gen AI plus planning, tools, and autonomy.
