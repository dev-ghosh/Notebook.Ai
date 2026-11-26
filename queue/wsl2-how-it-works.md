# WSL2: what it is and how it works

> **Answer first:** WSL2 (Windows Subsystem for Linux 2) lets you run a real Linux environment on Windows without dual-booting. It runs a genuine Linux kernel inside a lightweight virtual machine that Windows manages for you. Linux tools, shells, Docker and dev servers behave like a normal Linux box, while Windows files, VS Code and the terminal stay one command away.

---

## 1. What it is

- A Windows feature that runs Linux distributions (Ubuntu, Debian, etc.) alongside Windows.
- WSL2 is the current default when you install a distro; WSL1 is the older architecture.
- The Linux kernel is open source and serviced through Windows updates (`wsl --update`), so you don't manage it yourself.

## 2. How it works (architecture)

| Piece | What happens |
|---|---|
| **Real Linux kernel** | A Microsoft-built Linux kernel runs inside a lightweight utility VM (built on Hyper-V technology). Linux system calls are handled natively, not translated. |
| **One VM, many distros** | All your distros run as isolated containers inside the same managed VM. Windows starts the VM on demand and shuts it down when idle. |
| **Virtual disk** | Each distro's root filesystem is a real **ext4** filesystem stored in a `.vhdx` file on your Windows drive. |
| **Windows drives in Linux** | Mounted at `/mnt/c`, `/mnt/d`, etc. (via a network-style file protocol). Convenient, but slower than Linux's own filesystem. |
| **Linux files in Windows** | Open `\\wsl$\<Distro>` or `\\wsl.localhost\<Distro>` in File Explorer. |
| **Networking** | By default the VM sits behind NAT with its own virtual IP, and `localhost` ports are forwarded to Windows. Windows 11 also offers "mirrored" networking mode (set in `.wslconfig`). |
| **Resources** | The VM takes a share of host CPU and RAM (configurable in `%UserProfile%\.wslconfig`). |
| **Extras** | Systemd support (`/etc/wsl.conf` → `[boot] systemd=true`), GPU compute (CUDA), and Linux GUI apps through WSLg. |
| **Interop** | Run Windows programs from Linux (`explorer.exe .`, `code .`) and Linux commands from Windows (`wsl ls`). |

```
Windows host
 ├─ Windows apps, VS Code, Terminal
 └─ Lightweight utility VM  (managed by Windows)
      ├─ Linux kernel
      ├─ Distro A (ext4 in .vhdx)
      └─ Distro B (ext4 in .vhdx)
```

## 3. WSL1 vs WSL2

| | WSL1 | WSL2 |
|---|---|---|
| Design | Translates Linux syscalls to Windows (no kernel) | Real Linux kernel in a VM |
| Syscall compatibility | Partial | Full |
| Speed inside Linux filesystem | Slower | Much faster |
| Speed on `/mnt/c` files | Faster | Slower |
| Networking | Shares the Windows network | Own virtual network (NAT by default) |
| Docker / systemd | Poor | Works well |

## 4. Essential commands (run in PowerShell or CMD)

| Command | Purpose |
|---|---|
| `wsl --install` | Install WSL and a default distro (Ubuntu) |
| `wsl -l -v` | List distros with state and WSL version |
| `wsl --set-default-version 2` | Make new distros use WSL2 |
| `wsl --set-version <Distro> 2` | Convert an existing distro to WSL2 |
| `wsl -d <Distro>` | Start a specific distro |
| `wsl --terminate <Distro>` | Stop one distro |
| `wsl --shutdown` | Stop all distros and the VM (also kills tmux sessions) |
| `wsl --update` | Update the WSL kernel and components |
| `wsl --export <Distro> backup.tar` / `wsl --import ...` | Back up or move a distro |

## 5. Gotchas and good practice

1. **Keep project files inside Linux** (`~/projects`), not under `/mnt/c`. Cross-OS file access is the main performance trap.
2. **The virtual disk grows but doesn't shrink on its own.** Newer WSL versions support sparse VHDs (`wsl --manage <Distro> --set-sparse true`), or compact the disk manually.
3. **Cap resources** in `.wslconfig` if WSL eats too much RAM:
   ```ini
   [wsl2]
   memory=8GB
   processors=4
   ```
4. **Running processes die when the VM stops** (`wsl --shutdown`, reboot, or Windows restart). Use tmux or a service for long jobs, and expect them to end if WSL shuts down.
5. **Virtualization must be enabled** in BIOS, and some third-party hypervisors can conflict.

## 6. When to use it

- **Good fit:** web and backend development, Docker, Node/Python/Go toolchains, CLI-heavy workflows, running Linux-only tools or AI/agent tooling on a Windows laptop.
- **Less ideal:** workloads needing a full Linux desktop or kernel modules, or strict hardware access beyond what WSL exposes. Use a full VM or dual boot there.

---

## Sources
- [Microsoft Learn: About WSL 2](https://learn.microsoft.com/windows/wsl/wsl2-about)
- [Microsoft Learn: Compare WSL versions](https://learn.microsoft.com/windows/wsl/compare-versions)
- [Microsoft Learn: WSL 2 index](https://learn.microsoft.com/en-us/windows/wsl/wsl2-index)
- [Announcing WSL 2 (Microsoft devblog)](https://devblogs.microsoft.com/commandline/announcing-wsl-2)
