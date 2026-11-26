# AI inference vs training

> **Answer first:** **Training** is how a model *learns*: it processes huge amounts of data and repeatedly adjusts its weights. **Inference** is how a trained model *works*: weights are frozen, and it uses what it learned to answer a new input. Training is a huge, occasional cost that is throughput-bound. Inference is a smaller, constant per-request cost that is latency-bound, and it is what users and products actually run.

**Analogy:** training is a student studying for years. Inference is that student taking one exam question at a time.

---

## 1. Side-by-side comparison

| Dimension | Training | Inference |
|---|---|---|
| **Purpose** | Learn patterns: produce the weights | Apply the weights: produce outputs (text, image, prediction) |
| **What runs** | Forward pass, loss, **backward pass** (backpropagation), optimizer step | **Forward pass only** |
| **Weights** | Updated every step | Frozen (read-only) |
| **Data** | Massive datasets, many passes (epochs) | One request at a time (or small batches) |
| **Compute per unit** | About 6 × params × tokens FLOPs overall (rule of thumb) | About 2 × params FLOPs **per generated token** (rule of thumb) |
| **Memory** | Weights + gradients + optimizer states + activations, roughly **16 bytes/param** with Adam in mixed precision | Weights (2 bytes/param in FP16, ~0.5 in 4-bit) + **KV cache** that grows with context length |
| **Hardware** | Large GPU/TPU clusters with fast interconnect | Single GPUs up to clusters, plus specialized inference chips; edge devices for small models |
| **Cost shape** | Big one-time (or periodic) spend per model | Ongoing spend that scales with users and usage |
| **Key metric** | Loss, time-to-train, hardware utilization | Latency (time to first token), tokens/second, throughput, **cost per token** |
| **Optimized by** | Data/model/pipeline parallelism, mixed precision, better data | Quantization, batching, KV caching, speculative decoding, distillation, faster chips |
| **Who does it** | Model labs and teams fine-tuning | Everyone who calls or hosts a model |
| **Frequency** | Rare (weeks to months per model) | Constant (millions of requests per day) |

## 2. Two details worth knowing

1. **LLM inference has two phases.**
   - **Prefill:** read the whole prompt in parallel. This is compute-bound.
   - **Decode:** generate one token at a time. This is memory-bandwidth-bound, which is why chips with very fast memory help.
2. **Fine-tuning counts as training.** It updates weights, just on a smaller dataset and budget. Prompting, RAG and tool use are **inference-time** techniques: no weights change.

## 3. Why the distinction matters

- **Cost:** training gets the headlines, but inference is paid on every request, so it dominates spend once a product has users.
- **Hardware strategy:** training favors raw throughput; inference favors low latency and low cost per token. This is why inference-specialized chips and clouds exist (e.g., Groq; see `grok-vs-groq.md`).
- **Engineering:** inference work is serving: batching, caching, quantizing, autoscaling and monitoring latency. Training work is data pipelines, distributed jobs and checkpoints.

## 4. Quick examples

| Scenario | Phase |
|---|---|
| A lab runs thousands of GPUs for weeks to produce a new model | Training |
| Fine-tuning an open model on your company's support tickets | Training (fine-tuning) |
| You send a prompt to a chatbot and get a reply | Inference |
| A phone runs a small on-device model offline | Inference |
| Adding documents to a prompt via RAG | Inference (no weight changes) |

## 5. Memory aid

> **Train once, infer forever.** Training builds the brain; inference is the brain at work, and every user request pays for it.

---

## Sources
- [Axios: Nvidia deal shows why inference is AI's next battleground](https://www.axios.com/2025/12/29/nvidia-groq-inference-chips)
- [Tom's Hardware: Nvidia's Groq deal and the focus on inference](https://www.tomshardware.com/tech-industry/semiconductors/nvidia-confirms-20-billion-groq-deal-to-bolster-ai-inference-dominance)
- Rules of thumb (6ND training FLOPs, 2N inference FLOPs per token, ~16 bytes/param for Adam mixed precision) are standard figures from the scaling-laws and ZeRO literature. Treat them as estimates.
