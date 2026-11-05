# Skills and Plugins in Claude

## Answer first
A **skill** is a folder of instructions that teaches Claude how to do one kind of task well. A **plugin** is an installable *package* that can bundle skills, slash commands, agents, hooks and MCP servers. Skills = *knowledge*. Plugins = *distribution*. MCP = *connection to external systems*.

## 1. Skills
- A folder containing a `SKILL.md` (name + description in frontmatter, then instructions), plus optional scripts and reference files.
- Claude reads the short description, and loads the full skill only when the task matches. This keeps context small.
- Good for: house writing style, how to build a specific file type (docx, xlsx, pptx), review checklists, team conventions.
- Where they live in Claude Code:
  - Project: `.claude/skills/` (commit to git, shared with the team)
  - Personal: `~/.claude/skills/` (available in all your projects)

Minimal example:
```
.claude/skills/pr-review/SKILL.md
```
```markdown
---
name: pr-review
description: Review a pull request against our team checklist. Use when asked to review a PR or diff.
---
1. Check tests exist for new logic.
2. Flag functions over 50 lines.
3. Summarize risks in 3 bullets.
```

## 2. Plugins
- A bundle you install in one step. It can contain:
  - skills
  - slash commands
  - subagents
  - hooks (shell commands that fire on events)
  - MCP server configs
- Good for: sharing one setup across many repos or a whole team.
- Typical install flow in Claude Code:
```
/plugin marketplace add anthropics/claude-plugins-official
/plugin install <plugin-name>@claude-plugins-official
/reload-plugins
```

## 3. Skills vs plugins vs MCP
| | Skill | Plugin | MCP server |
|---|---|---|---|
| What it is | Instructions | Package of extensions | Tool/data connection |
| Gives Claude | Know-how | A bundle of the others | Ability to reach GitHub, DBs, Slack, etc. |
| Runs code | Only if it ships scripts | Can (via hooks, MCP) | Yes, as a separate process |
| Rule of thumb | "Do it this way every time" | "Install my whole setup" | "Talk to that system" |

## 4. Decision guide
- Want Claude to follow a repeatable process → write a **skill**
- Want Claude to reach an outside system → add an **MCP server**
- Want to share or reuse the whole combination → package a **plugin**

## 5. Safety note
Treat third-party skills and plugins like any code you install: read them first, since they can include scripts and hooks that run on your machine.

> Verify current details against the official Claude docs; this area changes quickly.
