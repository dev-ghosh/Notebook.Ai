# tmux: important commands (cheat sheet)

> **Answer first:** Learn these eight and you can use tmux productively: `tmux new -s <name>`, `Ctrl+b d` (detach), `tmux attach -t <name>`, `Ctrl+b c` (new window), `Ctrl+b %` and `Ctrl+b "` (split), `Ctrl+b arrows` (move between panes), `Ctrl+b z` (zoom), `Ctrl+b [` (scroll).

**Prefix key = `Ctrl+b`.** Press it, release, then press the command key. In the tables, "Prefix + d" means `Ctrl+b`, then `d`.

---

## 1. Sessions (run in your shell)

| Command | Purpose |
|---|---|
| `tmux` | Start a new unnamed session |
| `tmux new -s <name>` | Start a named session |
| `tmux new -A -s <name>` | Attach if it exists, otherwise create it |
| `tmux ls` | List sessions |
| `tmux attach -t <name>` (or `tmux a -t <name>`) | Reattach to a session |
| `tmux rename-session -t <old> <new>` | Rename a session |
| `tmux kill-session -t <name>` | Kill one session |
| `tmux kill-server` | Kill everything |

**Inside tmux:**

| Keys | Purpose |
|---|---|
| Prefix + `d` | **Detach** (leave everything running) |
| Prefix + `s` | Pick a session from a list |
| Prefix + `$` | Rename current session |
| Prefix + `(` / `)` | Previous / next session |

## 2. Windows (tabs)

| Keys | Purpose |
|---|---|
| Prefix + `c` | New window |
| Prefix + `,` | Rename window |
| Prefix + `n` / `p` | Next / previous window |
| Prefix + `0`-`9` | Jump to window number |
| Prefix + `w` | Pick from a window/session list |
| Prefix + `&` | Kill window (asks to confirm) |

## 3. Panes (splits)

| Keys | Purpose |
|---|---|
| Prefix + `%` | Split left/right (vertical divider) |
| Prefix + `"` | Split top/bottom (horizontal divider) |
| Prefix + arrow keys | Move to the pane in that direction |
| Prefix + `o` | Cycle to the next pane |
| Prefix + `z` | **Zoom** the pane full-screen (press again to restore) |
| Prefix + `x` | Kill pane (asks to confirm) |
| Prefix + `Space` | Cycle through preset layouts |
| Prefix + `{` / `}` | Swap pane with previous / next |
| Prefix + `!` | Break pane out into its own window |
| Prefix + `q` | Show pane numbers briefly |
| Hold Prefix, then `Ctrl+arrow` | Resize pane |

## 4. Scrolling, copy and command mode

| Keys | Purpose |
|---|---|
| Prefix + `[` | Enter **copy mode** (scroll with arrows or PgUp/PgDn) |
| `q` | Leave copy mode |
| Prefix + `]` | Paste the tmux buffer |
| Prefix + `:` | Open the tmux command prompt (e.g. `resize-pane -D 5`) |
| Prefix + `?` | List all key bindings |

## 5. Handy config (`~/.tmux.conf`)

```tmux
set -g mouse on                # click panes, drag borders, scroll with the wheel
set -g history-limit 50000     # bigger scrollback
set -g base-index 1            # number windows from 1
setw -g mode-keys vi           # vi keys in copy mode
set -s escape-time 10          # snappier Esc (helps in vim)
```

Apply changes without restarting: `tmux source-file ~/.tmux.conf`. You can also bind a reload key: `bind r source-file ~/.tmux.conf`.

## 6. A typical workflow

```bash
tmux new -s api            # 1. create a named session
# Prefix + %               # 2. split: code on the left, server on the right
# Prefix + "               # 3. split the right side: logs below the server
# Prefix + d               # 4. detach when you leave
tmux attach -t api         # 5. next day: pick up where you left off
```

## 7. Common gotchas

- **Mouse scroll does nothing:** enable `set -g mouse on` or use Prefix + `[`.
- **Nested tmux (tmux inside SSH inside tmux):** the outer tmux eats the prefix. Press the prefix twice to send it to the inner one.
- **Sessions vanish after a reboot:** tmux doesn't persist across restarts by default (plugins like tmux-resurrect can restore layouts).

---

## Sources
- [tmux manual page](https://man7.org/linux/man-pages/man1/tmux.1.html)
- [tmux wiki: Getting started](https://github.com/tmux/tmux/wiki/Getting-Started)
