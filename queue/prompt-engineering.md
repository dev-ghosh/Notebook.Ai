# What is Prompt Engineering?

## TL;DR
**Prompt engineering is the skill of writing clear instructions (prompts) so an AI gives you the answer you actually want.** A *prompt* is whatever you type to the AI. Better prompt = better result.

Think of it like giving directions to a very capable new colleague who knows a lot, but knows nothing about *your* situation unless you tell them.

---

## Bad prompt vs. good prompt
**Bad:**
> Write about dogs.

**Good:**
> Write a 150-word beginner-friendly paragraph about why dogs make good pets for families with young children. Use a warm, simple tone and end with one practical tip.

The second one says **what** to write, **who** it is for, **how long**, **what tone**, and **how it should end**.

## The 6 building blocks
| Block | What to include | Example |
|---|---|---|
| **Task** | What exactly you want | "Summarise this article" |
| **Context** | Background the AI cannot guess | "I'm a student with no maths background" |
| **Role** (optional) | Who the AI should act as | "Act as a friendly career coach" |
| **Format** | How the answer should look | "Use 5 bullet points" / "Give a table" |
| **Constraints** | Length, tone, what to avoid | "Under 100 words, no jargon" |
| **Examples** | Show what good looks like | "Here is a sample answer: ..." |

## Useful techniques
1. **Be specific.** Vague in, vague out.
2. **Give context.** Say who the audience is and what the goal is.
3. **Show an example (few-shot prompting).** Give 1 to 3 samples of the style or format you want, and the AI will copy the pattern.
4. **Break big tasks into steps.** Ask for an outline first, then each section.
5. **Ask for a format.** Table, bullets, JSON, email, steps.
6. **Say what to do, not only what to avoid.** "Write in short plain sentences" works better than "don't be complicated".
7. **Iterate.** If the first answer is off, reply with what to change ("shorter", "more formal", "add an example").
8. **Ask it to think step by step** on tricky problems. (Newer "reasoning" models already do this on their own.)

## A reusable template
```text
Role: You are a [role].
Task: [what you want done].
Context: [background, audience, goal].
Format: [bullets / table / paragraph / length].
Rules: [tone, things to avoid].
Example (optional): [a sample of good output].
```

## Quick example
**Prompt:**
> You are a friendly teacher. Explain what an API is to a 12-year-old using a restaurant analogy. Keep it under 120 words.

**Why it works:** it gives a role, topic, audience, a style (analogy), and a length.

## Common mistakes
- Being too short or too vague
- Asking for many unrelated things in one prompt
- Not stating the audience or the format
- Not checking the answer (AI can still be wrong, so verify important facts)
- Giving up after one try instead of refining

## Does it still matter as AI gets smarter?
Yes, but the "magic tricks" matter less. Modern models understand plain language well, so the best prompt is usually **clear, specific, and complete**, like a good brief to a colleague.

## Quick recap
- Prompt engineering = writing clear instructions for AI.
- Include task, context, format, constraints, and examples.
- Start simple, then refine based on the answer.
