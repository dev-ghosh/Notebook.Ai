# Jules by Google

## TL;DR
**Jules is Google's AI coding agent that works in the background.** You give it a coding task (fix a bug, add a feature, write tests, update a dependency). It copies your project into a secure cloud computer, makes the changes, runs the tests, and comes back with a pull request for you to review.

It is **asynchronous**: you do not have to sit and watch. You hand off the job and carry on with other work.

---

## Quick facts
| | |
|---|---|
| Made by | Google (started in Google Labs) |
| Type | Autonomous / asynchronous coding agent |
| Announced | December 2024 (Google Labs preview) |
| Public beta | Google I/O, May 2025 |
| Out of beta | August 2025 |
| Powered by | Google's Gemini models (it launched on Gemini 2.5 Pro) |
| Works with | GitHub repositories |
| Interfaces | Web app, command-line tool (Jules Tools), GitHub integration |
| Pricing | Included in Google's AI plans (Pro and Ultra get higher limits) |
| Website | jules.google |

> Plans, limits, and the model under the hood change over time. Check jules.google for the latest.

## How Jules works (step by step)
1. **Connect GitHub** and choose a repository.
2. **Describe the task**, for example "Fix the crash when the cart is empty" (or assign it from a GitHub issue).
3. Jules **copies your repo into a private cloud virtual machine**. Each task gets its own isolated machine.
4. It **reads your code and writes a plan**. You can see the plan and its reasoning before it starts changing things.
5. It **edits the code and runs your tests**.
6. It **opens a pull request** with the changes. You review and merge, or ask for tweaks.

## What you can use it for
- Fixing bugs
- Adding small or medium features
- Writing or improving tests
- Updating dependencies and version bumps
- Cleaning up code or writing docs

## Jules vs. other coding tools
| | Jules | Autocomplete / chat in your editor (e.g. Gemini Code Assist, Copilot) |
|---|---|---|
| Style | Asynchronous: hand off and come back later | Synchronous: works with you live while you type |
| Scope | A whole task, start to finish | Lines, functions, or quick questions |
| Where it runs | Google Cloud VM | Inside your editor |
| Output | A pull request | Suggestions in your code |

They are **complementary**: use editor tools for live coding and Jules for background tasks.

## Things to keep in mind
- **Always review the pull request.** Treat it like code from a new teammate.
- It works best on **clear, well-scoped tasks**. Vague tasks give vague results.
- Tasks run **independently**; Jules is not a team of agents talking to each other.
- Usage limits depend on your Google AI plan.

## Quick recap
- Jules = Google's "hand it off and review the PR" coding agent.
- Runs in the cloud, uses Gemini, integrates with GitHub.
- Great for background chores so you can focus on harder work.
