# AI Assistant vs AI Agent

## TL;DR
- **AI assistant:** waits for you, answers your question, and **you** do the next step.
- **AI agent:** you give it a **goal**, and it plans, uses tools, takes actions, and checks results on its own across many steps.

Short version: *an assistant helps you do the work; an agent does the work for you.*

---

## Example 1: Booking a trip
**Assistant**
> You: "Suggest flights from Delhi to Goa next Friday."
> Assistant: lists a few options.
> You: compare them, open the airline website, book, add it to your calendar.

**Agent**
> You: "Book me the cheapest morning flight to Goa next Friday and add it to my calendar."
> Agent: searches flights, compares prices, picks one, (asks your approval before paying), books it, adds it to your calendar, and tells you when it is done.

## Example 2: Coding
**Assistant (e.g. code chat or autocomplete):** you paste an error, it explains the problem and suggests a fix. You apply it.

**Agent (e.g. Claude Code, Google's Jules):** you say "Fix the login bug." It reads your code, finds the cause, edits the files, runs the tests, and opens a pull request for you to review.

## Example 3: Email
**Assistant:** drafts a reply when you ask.
**Agent:** monitors your inbox, sorts messages, replies to routine ones, and flags only the important ones for you.

## Comparison
| | AI assistant | AI agent |
|---|---|---|
| Starts when | You ask something | You give it a goal |
| Steps | Usually one reply at a time | Many steps, planned by itself |
| Tools | Little or none | Uses tools (search, files, apps, code) |
| Acts in the world? | Mostly just talks | Takes real actions |
| Your role | Do the follow-up yourself | Review, approve, step in if needed |
| Speed to finish | Depends on you | Faster for multi-step jobs |
| Risk | Low | Higher: mistakes can have real effects |

## Important notes
- It is a **spectrum**, not a strict line. Many products start as assistants and gain agent features (like running tools or doing multi-step tasks).
- Agents work best with **clear goals, limited permissions, and a human approval step** for risky actions (payments, deleting files, sending messages).
- Agents are built on the same AI "brain" as assistants. The difference is the **loop**: plan -> act -> check -> repeat.

## Quick recap
- Assistant = answers.
- Agent = achieves goals.
- Pick an assistant for quick help and an agent for multi-step tasks you would rather hand off.
