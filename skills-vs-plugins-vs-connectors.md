# Skills vs Plugins vs Connectors in Claude

## TL;DR
- **Skill = *how* to do something.** Written instructions Claude follows (your report format, your review checklist).
- **Connector = *access* to something.** A live link between Claude and an outside app (your calendar, CRM, Google Drive, Slack).
- **Plugin = a *package*.** A bundle of skills, connectors, commands, and helpers that you install in one step.

Simple way to remember: **connector gives data, skill gives method, plugin gives the bundle.**

---

## Analogy: a new employee
- **Connector** = the keys and logins to the tools (email, CRM, drive).
- **Skill** = the training manual: "when you write the weekly report, do it like this."
- **Plugin** = the onboarding kit that hands over the keys *and* the manual together.

## Each one in detail

### Skills
- A folder with a `SKILL.md` file (plus optional scripts or templates) that teaches Claude a procedure.
- Claude loads a skill **only when your request matches it**, so it does not clutter every conversation.
- **Cannot reach live data by itself.** It only tells Claude how to work.
- **Examples:** "Write meeting notes in our company format", "Review code against our checklist", "Build a branded slide deck".
- In Claude Code, personal skills live in `~/.claude/skills/` and project skills in `.claude/skills/`.

### Connectors
- A live connection from Claude to an external service. Under the hood these use **MCP (Model Context Protocol)**, an open standard for linking AI to tools and data. In the apps they are called "connectors"; in developer docs you will see "MCP servers".
- Claude can read from and act in that service, within **your** permissions.
- **Examples:** Gmail, Google Drive, Slack, GitHub, a company CRM.
- **Cannot decide how to do the job.** It supplies access, not method.

### Plugins
- A **bundle** that can contain skills, connectors (MCP servers), slash commands, subagents, and hooks.
- Built so a team can **share and install** a whole setup at once.
- **Example:** a "Sales toolkit" plugin that includes a follow-up-email skill, a CRM connector, and a `/pipeline-review` command.

## Side-by-side
| | Skill | Connector | Plugin |
|---|---|---|---|
| Main job | Teach a procedure | Provide access to an app | Package things together |
| Contains | Instructions, templates, scripts | A link to a service | Skills, connectors, commands, subagents, hooks |
| Gives Claude | Know-how | Data and actions | A ready-made setup |
| Needs a login to an app? | No | Usually yes | Only if it includes a connector |
| Best for | Repeating the same way of working | Pulling live data or acting in a tool | Sharing a tested setup with a team |
| Example | Brand voice guide | Slack connector | "Marketing team" kit |

## How they work together (example)
Goal: *"Create this week's sales report."*
1. **Connector** pulls this week's deals from the CRM.
2. **Skill** tells Claude how to structure and word the report.
3. **Plugin** is how you hand both to a new teammate in one install.

## Which one should I use?
- Need live data or to act in another app? -> **Connector**
- Need the same format, tone, or steps every time? -> **Skill**
- Need to share a working setup with others? -> **Plugin**

**Tip:** start with the smallest piece that solves your problem. Build a skill or add a connector first. Package into a plugin once it works and more than one person needs it.

## Safety notes
- Connectors can read and change real data, so connect only what you need and check what each one is allowed to do.
- Only install skills and plugins from sources you trust, since they can contain instructions and scripts.

## Quick recap
- Skill = method. Connector = access. Plugin = bundle.
- A skill or connector works fine alone. A plugin is for sharing several together.
