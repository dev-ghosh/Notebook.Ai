# Observability vs Tracing (for LLM apps)

> **Answer:** **Tracing is one technique; observability is the goal.** A trace records the path of a single request through your system as a tree of timed steps (spans). Observability is the broader ability to understand *why* the system behaved as it did, using traces **plus** metrics, logs/events, and (for LLM apps) evaluations. Tracing is necessary for agents, but not sufficient.

---

## 1. Definitions

| Term | What it is | Question it answers |
|---|---|---|
| **Observability** | A property of your system: you can infer its internal state from the data it emits | "Why did this happen, and what else is broken?" |
| **Tracing** | Recording one request's journey as spans with timing and attributes | "What exactly happened on this request?" |
| **Metrics** | Aggregated numbers over time (latency p95, tokens/min, error rate, cost) | "How is the system trending?" |
| **Logs / events** | Discrete records (errors, prompts, outputs) | "What was said or thrown at that moment?" |
| **Evals** | Scored quality checks on outputs | "Was the answer actually good?" |

Relationship: `tracing ⊂ observability`. Observability = traces + metrics + logs + evals, used together.

---

## 2. Why LLM apps need more than classic observability

- Outputs are non-deterministic: the same input can give different results.
- "Success" (HTTP 200) says nothing about answer quality. A hallucination is a successful request.
- Agents make multi-step decisions: model call -> tool call -> model call -> retrieval. You need the full tree to debug.
- Cost is per token, so cost is a first-class signal.
- Incidents rarely live only in the model layer; they often come from tools, retrieval, or context.

Observability does not replace evaluation. Traces show what happened; evals judge whether it was good.

---

## 3. What a good LLM trace contains (mutually exclusive layers)

1. **Request span:** user input, session/user ID, end-to-end latency.
2. **Model-call spans:** model name, parameters, input and output tokens, latency, finish reason.
3. **Retrieval spans:** query, documents returned, scores.
4. **Tool spans:** tool name, arguments, result, errors, duration.
5. **Agent spans:** each plan/step decision and loop iteration.
6. **Cost and quality tags:** cost per call, eval scores, user feedback.

---

## 4. The open standard: OpenTelemetry GenAI

OpenTelemetry (OTel) defines semantic conventions for GenAI: events, exceptions, metrics, model-operation spans, and agent-operation spans, with guidance for providers such as Anthropic, OpenAI, AWS Bedrock, Azure AI Inference, and for MCP.

Important caveat: these conventions are still marked **Development**, so attribute names and structure can change.

Typical attributes (verify against the current spec):

| Attribute | Meaning |
|---|---|
| `gen_ai.operation.name` | e.g. chat, embeddings |
| `gen_ai.request.model` | model requested |
| `gen_ai.usage.input_tokens` | prompt tokens |
| `gen_ai.usage.output_tokens` | completion tokens |

Why it matters: instrument once with OTel, then send traces to any backend (Langfuse, Datadog, Arize Phoenix, LangSmith) and avoid vendor lock-in. Vendor consolidation is real (for example, ClickHouse acquired Langfuse in January 2026, per one report), which is a good argument for staying vendor-neutral at the instrumentation layer.

---

## 5. Minimal manual tracing example (Python)

```python
from opentelemetry import trace

tracer = trace.get_tracer("my-agent")

def call_llm(prompt: str) -> str:
    with tracer.start_as_current_span("chat my-model") as span:
        span.set_attribute("gen_ai.operation.name", "chat")
        span.set_attribute("gen_ai.request.model", "my-model")

        response_text, in_tokens, out_tokens = my_model_client(prompt)  # your client

        span.set_attribute("gen_ai.usage.input_tokens", in_tokens)
        span.set_attribute("gen_ai.usage.output_tokens", out_tokens)
        return response_text
```

You also need an OTel SDK, a span processor, and an exporter configured once at app startup. Instrumentation libraries (OpenLLMetry, OpenLIT, or the OpenAI instrumentation package) can add these spans automatically.

---

## 6. Tool landscape (examples, not an endorsement)

- **Langfuse:** open-source LLM observability, OTel-based tracing, sessions, and agent graphs.
- **LangSmith:** LangChain's platform; supports native tracing and OTel.
- **Arize Phoenix / Arize AX:** ingest GenAI spans.
- **Datadog LLM Observability:** consumes OTel GenAI conventions.
- **OpenLLMetry / OpenLIT:** OTel instrumentation libraries for many frameworks.

---

## 7. Practical checklist

1. Trace every model call and tool call from day one.
2. Record token counts and compute cost per task.
3. Log the exact context sent (see `context-engineering.md`) with care for PII.
4. Add a feedback or eval score to traces so you can filter bad runs.
5. Alert on cost, latency, and error-rate metrics, not only on crashes.
6. Build a small golden dataset and run evals on every prompt or model change.
7. Prefer OTel-based instrumentation to stay portable.

---

## Sources
- [OpenTelemetry for GenAI Observability (Rubin Lake technology radar)](https://rubinlake.com/en/technology-radar/developer-ai-and-delivery/opentelemetry-genai-observability)
- [OpenTelemetry GenAI Semantic Conventions in 2026 (DEV Community)](https://dev.to/gabrielanhaia/opentelemetry-genai-semantic-conventions-your-llm-traces-should-look-like-this-in-2026-3ff6)
- [Langfuse: OpenTelemetry for LLM observability](https://langfuse.com/integrations/native/opentelemetry)

*Last updated: 2026-10-16*
