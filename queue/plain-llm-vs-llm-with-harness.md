# Plain LLM vs LLM with a Harness

## TL;DR
- **Plain LLM:** you send text, it sends text back. It can only *talk*.
- **LLM with a harness:** the same model, but wrapped in tools, memory, and a loop, so it can *do*: read files, run code, search, check its own work, and keep going until the task is finished.

Short version: *a plain LLM gives advice; an LLM with a harness does the work.*

---

## Example: "Fix the failing test"

**Plain LLM**
> You paste the error and the code into a chat.
> LLM: "Try changing line 42 to ..."
> You: copy the change, run the tests yourself, paste the new error back, repeat.

**LLM with a harness (e.g. Claude Code)**
> You: "Fix the failing test."
> It finds the test file, reads the code, edits it, runs the tests, sees one still failing, fixes that too, and reports "all tests pass."

The model is the same in both cases. What changed is the harness around it.

## Side-by-side
| | Plain LLM | LLM with harness |
|---|---|---|
| Input / output | Text in, text out | Text plus tools, files, apps |
| Can act in the world? | No | Yes (edit files, run code, search, send requests) |
| Sees your files? | Only what you paste | Can open and search them itself |
| Steps | One reply at a time | Many steps in a loop |
| Checks its own work? | No, unless you check | Yes: runs tests, reads results, retries |
| Memory | Only this chat | Project notes, saved context, summaries |
| Up-to-date info | Limited to its training | Can search the web or call live data |
| Who does the follow-up? | You | The harness |
| Risk | Wrong text | Wrong *actions* (so permissions matter) |
| Cost | Lower | Higher (many steps use more tokens) |

## What a harness adds
1. **Tools:** hands to read, write, run, and search.
2. **A loop:** keeps working until done instead of stopping after one reply.
3. **Context management:** feeds the model the right information at the right time.
4. **Memory:** remembers rules and progress across steps or sessions.
5. **Guardrails:** asks permission before risky actions.

## Where you meet each one
- **Plain LLM:** calling a model through an API with just a prompt and nothing else.
- **LLM with harness:** coding agents (Claude Code, Cursor, Codex CLI, Jules), and chat apps with search, file upload, or code running turned on. It is a **spectrum**: even a chat app adds a little harness (web search, file upload).

## When is plain enough?
- Quick questions, brainstorming, rewriting a paragraph, explaining a concept.

## When do you want the harness?
- Multi-step tasks, anything touching files or apps, work that needs checking, or jobs you want to hand off.

## Things to watch
- **Quality varies.** A weak harness can make a strong model look bad.
- **More power, more risk.** An agent can change real files, so use permission prompts and review the results.
- **It costs more.** Loops and tool calls add up.

## Quick recap
- Plain LLM = a smart brain with no hands.
- Harness = hands, memory, rules, and a loop.
- Same model, very different capability.
