# Claude Code vs Claude Desktop

## Answer first
**Claude Desktop** is the general-purpose Claude app on your computer (chat, files, research, documents). **Claude Code** is the agentic coding tool that reads your codebase, edits files, runs commands and works with git. Desktop is for *conversations and knowledge work*; Code is for *building software*. They overlap: Code is also reachable from the desktop app, web and mobile.

## 1. What each one is
| | Claude Desktop | Claude Code |
|---|---|---|
| Purpose | Everyday assistant, writing, analysis, research, longer tasks | Software engineering agent |
| Main surface | Desktop app (also web and mobile as "Claude") | Terminal (CLI), IDE extensions, web, desktop, mobile |
| Typical user | Anyone | Developers |

## 2. What each can do
- **Claude Desktop:** chat, upload files, produce documents/spreadsheets/decks, web search, connectors to apps (Gmail, Drive), memory, projects, scheduled tasks, computer use on your machine.
- **Claude Code:** reads the whole repo, edits multiple files, runs tests and shell commands, uses git/GitHub (commits, PRs), supports MCP servers, skills, plugins, hooks, subagents, and a project memory file (`CLAUDE.md`).

## 3. Where they run
- Desktop app: your machine for the UI; cloud sessions can be linked to your computer's folders.
- Claude Code CLI: runs in your terminal against local files, so it needs your machine on.
- Claude Code on the web / cloud sessions: runs in Anthropic's cloud against a repo you attach, so your laptop can be off.

## 4. How to choose
- Writing, research, summarizing, planning, documents → **Desktop**
- Fixing bugs, refactoring, building features, running tests, git workflows → **Code**
- Daily automated work with the laptop off → **cloud session / scheduled task** (either product can start one)

## 5. Quick start for Code
```
npm install -g @anthropic-ai/claude-code   # or follow the official installer
cd your-project
claude
```
Inside a session: `/help` lists commands, `!` runs a shell command directly, `/install-github-app` connects GitHub.

> Product details change often. Verify against the official docs at https://docs.claude.com.
