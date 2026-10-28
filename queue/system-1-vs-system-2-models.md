# System 1 vs System 2 Models (How AI "Decides" How to Think)

## TL;DR
- **System 1 model = fast, instinctive.** It answers right away by recognising patterns.
- **System 2 model = slow, deliberate.** It thinks step by step before answering.

The idea comes from psychologist Daniel Kahneman's book *Thinking, Fast and Slow*. AI researchers borrowed it to describe two styles of AI.

---

## The human version first
| | System 1 | System 2 |
|---|---|---|
| Speed | Instant | Slow |
| Effort | Almost none | Needs focus |
| Example | Recognising a friend's face, 2 + 2 | Solving 17 x 24, planning a route |

## The AI version
### System 1 models (fast and intuitive)
They produce an answer in one quick pass, based on patterns learned in training. They do not stop to "think".

**Examples**
- Autocomplete on your phone keyboard
- A spam filter deciding "spam or not spam"
- An image classifier labelling a photo "cat"
- A chatbot giving a quick, casual reply
- Face unlock

**Good at:** speed, low cost, simple or familiar tasks.
**Weak at:** tricky multi-step problems, where it may sound confident but be wrong.

### System 2 models (slow and reasoning)
They spend extra time "thinking" before replying: breaking the problem into steps, trying approaches, checking their own work. These are often called **reasoning models** or "thinking mode".

**Examples**
- OpenAI's o-series and GPT "Thinking" modes
- Claude with extended thinking
- Gemini's thinking modes
- DeepSeek-R1

**Good at:** maths, hard coding bugs, logic puzzles, planning, science questions.
**Weak at:** slower and more expensive, and overkill for simple questions.

## Where do "decision models" fit in?
Decision-making in AI is about **choosing how much thinking a task needs**:
- Easy question ("What is the capital of France?") -> use the fast System 1 path.
- Hard question ("Find the bug in this 500-line program") -> use the slow System 2 path.

Many modern AI products do this automatically: a built-in "router" decides when to answer quickly and when to think longer.

## Side-by-side
| | System 1 model | System 2 model |
|---|---|---|
| Speed | Fast | Slower |
| Cost | Cheap | More expensive |
| How it works | Instant pattern matching | Step-by-step reasoning |
| Best for | Simple, everyday tasks | Hard, multi-step problems |
| Risk | Quick but sometimes wrong | Slow, can overthink easy things |

## Quick recap
- System 1 = fast gut feeling. System 2 = slow careful thinking.
- Use the fast kind for easy tasks, the reasoning kind for hard ones.
- The best AI tools mix both.

> Note: if you meant classic "decision models" from machine learning (like decision trees), that is a different topic. Ask and I will add a separate file.
