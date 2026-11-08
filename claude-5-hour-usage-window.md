# How Claude's 5-Hour Usage Window Works

## TL;DR
- Your Claude allowance for a short burst of work comes in a **5-hour block**.
- The block **starts when you send your first message** and **resets in full 5 hours later**.
- If you use it all early, you wait for the reset (or use paid extra credits).
- **Unused allowance does not roll over.** Each new window starts fresh.
- A separate **weekly limit** also applies. Resetting the 5-hour window does not refill the weekly one.

---

## How the window works
1. You send your first message. **The 5-hour clock starts now.**
2. Everything you do in the next 5 hours draws from the same allowance.
3. At the 5-hour mark, the allowance **resets in full**.
4. The next window starts when you send your next message after that.

### Example timeline
| Time | What happens |
|---|---|
| 9:00 AM | You send your first message. Window starts. Resets at 2:00 PM. |
| 10:30 AM, 12:00 PM | More messages, all inside the same window. |
| 12:30 PM | You hit 100%. Claude pauses. |
| 2:00 PM | Window resets to full. |
| 3:30 PM | Your next message starts a **new** window, which ends at 8:30 PM. |

If you only used half your allowance by 2:00 PM, the other half is **not saved**. That is why people sometimes say "rollover" about this window, but nothing actually rolls over.

## What counts toward it
Usage is measured by **how much work Claude does**, not by number of messages. A short question costs little. A long conversation or a big output costs a lot.

**It is one shared pool.** Claude on the web, Claude Desktop, and Claude Code all draw from the same limit.

**Things that use it up faster:**
- Long conversations (Claude re-reads the history each time)
- Bigger, more powerful models
- Higher effort or extended thinking
- Connectors and tools, which add a lot of text
- Subagents and background loops, which run extra work in parallel

## The weekly limit (a second, separate cap)
- Weekly limits also apply, across all models. Some plans also have a separate weekly limit for certain models.
- The weekly limit has its own fixed reset time for your account.
- **Both limits apply at once.** You can have room in the 5-hour window and still be blocked because your week is used up.

## What happens when you hit a limit
You can:
1. **Wait** for the reset (the message shows when).
2. **Use usage credits**, if you have turned them on, so work continues instead of stopping.
3. **Upgrade your plan.** New limits apply immediately.

## How to check where you stand
Look under **Settings > Usage**. The "Current session" bar shows how much of the 5-hour window you have used and the time left.

## Tips to stretch your allowance
- Start a **new chat** for a new topic instead of one giant conversation.
- Use a **smaller model** for easy tasks.
- Turn off tools and connectors you are not using.
- Be specific, so Claude does not need many tries.
- Plan big tasks to start when you will have time to use the window well, since the clock starts at your first message.

## Good to know
- Anthropic does not publish exact token counts per window, and says it may adjust limits to manage capacity. Treat the details as subject to change.
- Some third-party guides call this a "rolling" window. Anthropic's own help page describes it as starting at your first message and resetting five hours later. If something looks different on your screen, trust Settings > Usage.
- On some business or government plans, the dashboard may show reset times rounded to the top of the hour.

## Quick recap
- Window starts at your first message, resets 5 hours later.
- Nothing carries over.
- Weekly limit runs separately.
- Long chats, big models, and tools use it fastest.
