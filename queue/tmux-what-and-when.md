# tmux: what it is and when it's used

> **Answer first:** tmux is a **terminal multiplexer**. It runs a background server that keeps your terminal sessions alive, and lets you split one terminal window into many panes and tabs. The key payoff is that you can **detach and come back later**: close the window, lose your SSH connection, and your processes keep running.

---

## 1. What it is

- A program that sits between you and your shell. Your shells run inside tmux, not inside the terminal window itself.
- Client-server design: the tmux **server** lives in the background, and terminal windows are just **clients** that attach to it.
- Free, runs on Linux, macOS and WSL, and is configured with `~/.tmux.conf`.

## 2. Core concepts (hierarchy)

| Level | What it is | Analogy |
|---|---|---|
| **Server** | Background process that owns everything | The app's engine |
| **Session** | A named workspace, e.g. `api` or `frontend` | A project |
| **Window** | A full-screen "tab" inside a session | Browser tab |
| **Pane** | A split region inside a window, each running its own shell | Split view |

Everything is controlled with a **prefix key** (default `Ctrl+b`) followed by a command key. See `tmux-commands.md`.

## 3. When it's used (use cases)

1. **Remote work over SSH.** Start a long job on a server, detach, log out, and reattach later. A dropped connection no longer kills the job.
2. **Long-running local tasks.** Training runs, builds, migrations, scrapers and AI agents, without tying up a terminal window.
3. **One-screen multitasking.** Editor in one pane, dev server in another, logs in a third.
4. **Several projects at once.** One named session per project, switched in a keystroke.
5. **Parallel agent or CLI sessions.** For example, a coding agent in one pane and a reviewer, tests or a log tail in another.
6. **Pair programming and shared debugging.** Two people can attach to the same session.
7. **Repeatable layouts.** Script your workspace so one command rebuilds it.

## 4. When you don't need it

- Short, one-off commands in a single terminal.
- If your terminal app already gives you tabs and splits and you never work remotely.
- A heavy GUI-only workflow.
- Alternatives: GNU `screen` (older, simpler), Zellij (newer, friendlier defaults).

## 5. WSL note

tmux sessions survive closing a terminal window, but not WSL itself stopping. `wsl --shutdown`, a reboot or a Windows restart ends the VM and the tmux server with it.

## 6. 30-second start

```bash
tmux new -s work      # start a named session
# ...do stuff...
# press Ctrl+b, then d   → detach (everything keeps running)
tmux ls               # list sessions
tmux attach -t work   # come back
```

---

## Sources
- [tmux wiki (GitHub)](https://github.com/tmux/tmux/wiki)
- [tmux manual page](https://man7.org/linux/man-pages/man1/tmux.1.html)
