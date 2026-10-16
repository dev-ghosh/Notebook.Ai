# Small LLM vs Large LLM

> **Answer:** Default to a **small model** for narrow, high-volume, well-defined tasks (classification, extraction, routing, summarization, structured output). Reserve a **large frontier model** for open-ended reasoning and hard, ambiguous work. The winning production pattern is a two-tier stack with a router, and the choice should be made by **evals on your task**, not by brand or size.

---

## 1. Definitions (they are fuzzy)

- **Small language model (SLM):** commonly sub-10B parameters. Runs on a laptop, phone, or a single modest GPU.
- **Large / frontier LLM:** tens to hundreds of billions of parameters, usually called through an API.
- Example of a small model: SmolLM3 (3B, Apache 2.0) supports 128K context and built-in tool calling.

The line moves every few months. Judge by capability per cost on your task, not by the parameter count alone.

---

## 2. When each one wins (mutually exclusive buckets)

### Small model wins when
- The task is narrow and repeatable: classify, extract fields, rewrite, detect intent, route.
- Volume is high, so cost per call dominates.
- Latency matters (interactive UX, on-device).
- Data must stay local (privacy, offline, regulated settings).
- You can fine-tune or distill for the one job.

### Large model wins when
- The task is open-ended: multi-step reasoning, planning, ambiguous instructions.
- It needs broad world knowledge or long, messy context.
- Failure is expensive and you cannot afford a weaker model's error rate.
- You have no labelled data to tune a small model.

---

## 3. Cost and memory math

Weights memory is roughly `parameters x bytes per parameter`. Add the KV cache (grows with context length) and runtime overhead on top.

| Model size | FP16 (2 bytes) | 4-bit (~0.5 bytes) |
|---|---|---|
| 3B | ~6 GB | ~1.5 GB |
| 7B | ~14 GB | ~3.5 GB |
| 70B | ~140 GB | ~35 GB |

These are rough weight-only figures. Real usage is higher.

Reported industry numbers (treat as indicative): task-tuned small models are often about an order of magnitude cheaper per million tokens than frontier tiers, and API prices overall fell sharply between 2024 and 2026.

---

## 4. Patterns for using both

1. **Router:** a small model (or rules) classifies each request and sends easy ones to a small model, hard ones to a large model.
2. **Cascade:** try the small model first; escalate to the large model if confidence is low or validation fails.
3. **Speculative decoding:** a small "draft" model proposes tokens and the large model verifies them, which speeds up large-model serving.
4. **Distillation / fine-tuning:** use a large model to generate training data, then tune a small model for one task.
5. **Specialist split:** small models for routing, classification, rephrasing, and intent detection; the frontier model only for hard reasoning.

---

## 5. Decision checklist

1. Can I define the task in one sentence with a clear right answer? -> try small first.
2. Do I have 50-200 realistic examples to build an eval set? If not, build that before choosing.
3. What is my target latency and cost per task?
4. Does the data need to stay on-device or on-prem?
5. Run both models on the eval set. Compare quality, cost per task, and failure rate.
6. Only then decide. Re-run when a new model ships.

---

## 6. Common mistakes

- Upgrading everything to the newest large model by default. Practitioners call this lazy model selection and it can cost many times more for no gain.
- Choosing a small model without measuring failure cases.
- Ignoring the harness. Routing, context, and validation often matter more than the base model.
- Forgetting that a small model needs tighter prompts, cleaner context, and structured output constraints (see `context-engineering.md`).

---

## Sources
- [7 AI Development Trends Shipping Right Now (early 2026)](https://www.gilricardo.com/blog/ai-development-trends-shipping-early-2026)
- [Generative AI Trends 2026 (two-tier stack, small task-tuned models)](https://futureagi.com/blogs/generative-ai-trends-2026)
- [AI Engineer Melbourne 2026 field dispatch (harness over model, model selection as engineering)](https://fieldreports.webdirections.org/ai-engineer-melbourne-2026/one-pager.html)

*Last updated: 2026-10-16*
