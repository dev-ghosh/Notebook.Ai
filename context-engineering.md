# Context Engineering

> **Answer:** Context engineering is the discipline of deciding **what information the model sees at each step, in what order, and what it never sees**. A prompt is just one piece. In 2026 most agent reliability problems are context problems, not model problems. The practical toolkit is four moves: **write, select, compress, isolate**, plus measurement.

---

## 1. What it is (and how it differs from prompt engineering)

- **Prompt engineering:** crafting the instruction text.
- **Context engineering:** managing the whole information environment: instructions, tools, retrieved data, memory, conversation state, and the token budget. The term was popularized by Andrej Karpathy.
- Why the shift: as tasks get longer and agents call tools, the prompt is a small fraction of what fills the window.

---

## 2. What goes into the context window (six inputs)

| Input | Examples | Key question |
|---|---|---|
| Instructions | System prompt, rules, output format | Is it short, specific, and non-contradictory? |
| Tools | Function schemas, MCP tool descriptions | Does the model need all of these right now? |
| Retrieved knowledge | RAG chunks, documents, search results | Is it relevant and fresh? |
| Memory | Facts from past sessions | Is it still true and needed for this task? |
| State / history | Prior turns, scratchpad, tool outputs | Can older parts be summarized? |
| Budget | Tokens and cost per step | What is the cost per task? |

---

## 3. The four moves

### Write (store context outside the window)
Save notes, plans, and intermediate results to a scratchpad or file so the window stays small. Use long-term memory for facts that should survive across sessions.

### Select (pull in only what is relevant)
Retrieve the right chunks (hybrid search + reranking), load only the tools needed for this step, and fetch memories that match the current task. Sometimes a well-structured document in the prompt beats a RAG pipeline.

### Compress (shrink what stays)
Summarize old conversation turns, trim verbose tool outputs, and drop redundant text. Compaction keeps long tasks inside the budget.

### Isolate (separate concerns)
Give sub-agents their own clean context for sub-tasks and return only a short result. Keep noisy tool output out of the main thread.

---

## 4. Failure modes to watch for

- **Poisoning:** a wrong fact or hallucination enters the context and gets reused as truth.
- **Distraction:** too much history makes the model fixate on the past instead of the task.
- **Confusion:** irrelevant tools or documents lead the model to use the wrong one.
- **Clash:** two parts of the context contradict each other.
- **Overflow / cost:** the window fills, quality drops, and spend rises.

(These names are commonly used in the community; they describe patterns rather than a formal standard.)

---

## 5. Context is not memory

A bigger window does not solve forgetting. Practitioners at AI Engineer Melbourne 2026 described memory as still unsolved: agents need an explicit memory architecture (what to store, when to retrieve, when to expire), not just more tokens.

---

## 6. Practical checklist

1. Write down what the model must know to do this one step. Nothing more.
2. Put stable instructions first and volatile data last.
3. Load tools lazily; do not expose 50 tools for a 2-tool task.
4. Cap tool output size; summarize before it re-enters the window.
5. Add a compaction step for long-running agents.
6. Log the exact context sent on every call (see `observability-vs-tracing.md`).
7. Run evals when you change retrieval, prompts, or memory. Do not trust vibes.

---

## 7. Example: support-ticket agent

**Before (messy):** full ticket history + entire knowledge base + all 30 tools + a 2,000-word system prompt on every call.

**After (engineered):**
- System prompt: 150 words, role plus output schema.
- Select: top 3 relevant KB chunks plus the last 3 customer messages.
- Tools: only `lookup_order` and `create_refund` for this intent.
- Compress: earlier turns summarized into 5 bullets.
- Result: lower cost, lower latency, fewer wrong tool calls.

---

## 8. How it connects to other topics

- **MCP** standardizes how tools and data reach the context.
- **Small models** need tighter context than large ones (see `small-llm-vs-llm.md`).
- **Observability** is how you see what context the model actually received.

---

## Sources
- [7 AI Development Trends Shipping Right Now (context engineering supersedes prompt engineering)](https://www.gilricardo.com/blog/ai-development-trends-shipping-early-2026)
- [Context Engineering: The Next Evolution of AI (Omdena)](https://www.omdena.com/blog/context-engineering-next-evolution-of-ai)
- [AI Engineer Melbourne 2026 field dispatch (context is not memory)](https://fieldreports.webdirections.org/ai-engineer-melbourne-2026/one-pager.html)

*Last updated: 2026-10-16*
