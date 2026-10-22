# n8n vs LangGraph

> **Answer:** They solve different problems. Use **n8n** when the job is wiring apps and triggers together with some AI in the middle. Use **LangGraph** when the agent's control flow, state, and recovery *are* the product. Many teams use both: n8n as the trigger and integration layer, LangGraph as the agent brain behind an HTTP call.

---

## 1. What each one is

| | n8n | LangGraph | 
|---|---|---|
| Category | Workflow automation platform (visual + code) | Agent orchestration framework (library) |
| You build with | A canvas of nodes | Code: state, nodes, edges |
| License | Fair-code: Sustainable Use License + Enterprise License. Source is visible and self-hostable, but it is **not** OSI open source | MIT (open source) |
| AI angle | AI agent nodes built on LangChain; model-flexible (OpenAI, Anthropic, Google, open-weight) | Stateful, durable agents; LangChain 1.0 agents are built on top of it |
| Where it runs | Self-host or n8n Cloud | Wherever your Python/JS code runs |

LangGraph 1.0 went GA in October 2025. The one notable change was that `langgraph.prebuilt` was deprecated in favour of `langchain.agents`.

---

## 2. How to choose (five independent dimensions)

### A. Build experience
- **n8n:** fastest path from idea to a running automation. Non-engineers can read and edit the canvas. Code nodes (JavaScript/Python) cover the gaps.
- **LangGraph:** you model the agent as a graph in code. Slower to start, but everything is explicit and version-controlled.

### B. Control and reliability
- **n8n:** good for linear or lightly branching flows. Complex loops, retries with state, and long-lived agent memory get awkward on a canvas (practitioner experience, not a hard limit).
- **LangGraph:** built for this. Checkpointing saves state at each step, so a run can be paused and resumed exactly where it stopped, even days later. Human-in-the-loop interrupts are first-class: pause for review, edit, or approval, then continue.

### C. Ecosystem and integrations
- **n8n:** 400+ integrations and 900+ templates out of the box. This is its biggest strength.
- **LangGraph:** you bring your own integrations (tools, MCP servers, APIs). Maximum flexibility, more work.

### D. Operations (testing, observability, deployment)
- **n8n:** execution logs per workflow run; enterprise tier adds RBAC and audit trails.
- **LangGraph:** it is just code, so it fits normal CI, unit tests, evals, and tracing (see `observability-vs-tracing.md`). Streaming of tokens, tool calls, and state updates is built in.

### E. Licensing and cost
- **n8n:** read the Sustainable Use License before commercial use. Free self-hosting has limits on how you may use it.
- **LangGraph:** MIT, no restrictions beyond the usual.

---

## 3. Decision rule

```
Is the main value "connect system A to system B on a trigger"?
  yes -> n8n
  no  -> Does the agent need durable state, branching loops,
         or human approval mid-run?
           yes -> LangGraph
           no  -> either; start with whichever your team can maintain
```

---

## 4. The hybrid pattern (often the best answer)

```
[Email / webhook / schedule]
        |
      n8n  --- fetch data, clean it, handle auth
        |
   HTTP call
        |
   LangGraph agent service  --- plan, call tools, pause for approval
        |
      n8n  --- send Slack message / write to sheet / create ticket
```

n8n owns the edges (triggers and integrations). LangGraph owns the reasoning core.

---

## 5. Minimal LangGraph example

```python
from typing import TypedDict
from langgraph.graph import StateGraph, START, END
from langgraph.checkpoint.memory import InMemorySaver

class State(TypedDict):
    question: str
    answer: str

def answer_node(state: State) -> dict:
    return {"answer": f"Echo: {state['question']}"}

builder = StateGraph(State)
builder.add_node("answer", answer_node)
builder.add_edge(START, "answer")
builder.add_edge("answer", END)

graph = builder.compile(checkpointer=InMemorySaver())
result = graph.invoke(
    {"question": "hello"},
    config={"configurable": {"thread_id": "demo-1"}},
)
print(result["answer"])
```

`InMemorySaver` is for learning. Use a persistent checkpointer in production.

---

## 6. Pitfalls

- **LangGraph durable execution needs discipline.** Make steps deterministic and idempotent, and wrap side effects (API calls, file writes) inside tasks or nodes so a resume does not repeat them.
- **Checkpointing has a cost.** Higher durability modes add storage and latency overhead.
- **Human-in-the-loop needs a policy.** Decide who approves, how long a run may wait, and what happens on timeout.
- **n8n "open source" label.** It is source-available. Do not call it open source in your docs.

---

## Sources
- [LangGraph 1.0 announcement (LangChain changelog)](https://changelog.langchain.com/announcements/ann_lxOZRCoFw2Qn9)
- [LangGraph durable execution docs](https://docs.langchain.com/oss/python/langgraph/durable-execution/index.html)
- [n8n on GitHub (license, integrations, AI nodes)](https://github.com/n8n-io/n8n)

*Last updated: 2026-10-16*
