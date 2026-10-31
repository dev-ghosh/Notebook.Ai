# Setting Up the Agent and Subagents Separately in Claude Code

## TL;DR
- The **agent** is your main Claude Code session. You configure it with `CLAUDE.md`, settings, and the model you pick.
- A **subagent** is a helper the main agent hands work to. Each is a Markdown file in `.claude/agents/` with its own instructions, tools, and model.
- You set them up **separately**: configure the main agent once, then add subagents one file at a time.

---

## Part 1: The main agent (your session)

This is Claude Code itself. Set it up with these pieces:

| What | How |
|---|---|
| Project instructions | Run `/init` to create a `CLAUDE.md`, then edit it with your rules (coding style, commands, folder layout) |
| Model | Use `/model` to pick one |
| Permissions and settings | `.claude/settings.json` (project) or `~/.claude/settings.json` (all projects) |
| External tools | Add MCP servers, for example `claude mcp add ...` |

### Optional: run the whole session AS a custom agent
You can make the main session behave like one of your agent files:

```bash
claude --agent code-reviewer
```

Or make it the default for a project in `.claude/settings.json`:

```json
{
  "agent": "code-reviewer"
}
```

---

## Part 2: A subagent

A subagent is a Markdown file with a small settings block (frontmatter) on top, and its instructions below.

### Where the file lives
| Location | Available in |
|---|---|
| `.claude/agents/` | This project only (commit it so your team shares it) |
| `~/.claude/agents/` | All your projects |

### Create one
**Easiest way:** just ask Claude.

```text
Create a project subagent called code-reviewer in .claude/agents/.
It should review code for bugs and security issues, be read-only, and use Sonnet.
```

Or write the file yourself: `.claude/agents/code-reviewer.md`

```markdown
---
name: code-reviewer
description: Reviews code for quality and security. Use proactively after code changes.
tools: Read, Grep, Glob
model: sonnet
---

You are a careful code reviewer. Look at the recent changes and give
specific, actionable feedback. Group it as: critical, warnings, suggestions.
```

### The settings (frontmatter) explained
| Field | Required? | Meaning |
|---|---|---|
| `name` | Yes | Unique name, e.g. `code-reviewer` |
| `description` | Yes | **When** Claude should use this subagent (very important) |
| `tools` | No | Which tools it may use. Leave out to allow all |
| `model` | No | `sonnet`, `opus`, `haiku`, `fable`, or `inherit` (same as main) |

There are more optional fields (like `skills`, `memory`, `permissionMode`), but these four are enough to start.

### Use it
Three ways, from loosest to strictest:
1. **Let Claude decide:** it reads each subagent's `description` and delegates automatically.
2. **Ask by name:** "Use the code-reviewer subagent to check my changes."
3. **@-mention:** type `@` and pick the subagent from the list to force it.

> If you create the `.claude/agents/` folder for the first time while Claude Code is already running, restart the session once so it notices the new folder.

---

## Part 3: Using both together

Example: a main agent that only coordinates, with two specialist subagents.

`.claude/agents/researcher.md`
```markdown
---
name: researcher
description: Searches the codebase and reports findings. Use for exploration.
tools: Read, Grep, Glob
model: haiku
---
You explore code and report a short summary of what you find. Do not edit files.
```

`.claude/agents/worker.md`
```markdown
---
name: worker
description: Makes code changes and runs tests once the plan is clear.
tools: Read, Edit, Write, Bash
model: sonnet
---
You implement the requested change, run the tests, and report what you changed.
```

`.claude/agents/coordinator.md`
```markdown
---
name: coordinator
description: Plans work and delegates to specialist agents.
tools: Agent(worker, researcher), Read, Bash
---
Break the task into steps. Send exploration to researcher and code changes to worker.
```

Start the session as the coordinator:

```bash
claude --agent coordinator
```

The coordinator can only hand work to `worker` and `researcher`, because of `Agent(worker, researcher)` in its `tools`.

## Quick test without creating files
Define subagents for one session only:

```bash
claude --agents '{
  "debugger": {
    "description": "Debugging specialist for errors and test failures.",
    "prompt": "You are an expert debugger. Find root causes and propose fixes."
  }
}'
```

---

## Good habits
- **One job per subagent.** "Reviewer" and "test-runner" beat a vague "helper".
- **Write a sharp `description`.** Claude uses it to decide when to delegate.
- **Give the fewest tools needed.** A reviewer should not be able to edit files.
- **Use a cheaper model for simple jobs** (for example `haiku` for searching).
- **Remember:** a subagent starts with a fresh context. It does not see your chat history, so give it the details it needs in the task.
- **Why use subagents at all?** They keep noisy work (long logs, big searches) out of your main conversation and return just a summary.

## Quick recap
1. Main agent = your session. Set up with `CLAUDE.md`, `/model`, settings, MCP.
2. Subagent = a `.md` file in `.claude/agents/` (project) or `~/.claude/agents/` (personal).
3. Use `--agent <name>` if you want the main session itself to act as a specific agent.
