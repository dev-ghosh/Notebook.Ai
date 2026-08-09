# AI Agents: Normal Agents, AI Agents, and Deep Agents

## What is an AI Agent?

An **AI Agent** is a system that uses an AI model to understand a goal,
decide what actions are needed, use tools when necessary, and produce a
result.

``` text
Goal
 ↓
AI Model
 ↓
Reason / Decide
 ↓
Use Tools
 ↓
Observe Results
 ↓
Take More Actions if Needed
 ↓
Final Result
```

An agent is therefore more than an LLM simply answering a question: it
can **take actions and interact with its environment**.

------------------------------------------------------------------------

## LLM vs AI Agent

A normal LLM application:

``` text
User → LLM → Answer
```

An agent can:

``` text
User → Agent → Decide → Tool → Observe → Answer
```

**LLM = primarily generates**

**Agent = decides + acts + generates**

------------------------------------------------------------------------

## What is a Normal / Simple Agent?

A simple agent is designed to accomplish a relatively straightforward
task using an LLM and one or a few tools.

Example:

``` text
Question
 ↓
Agent
 ↓
Search Tool
 ↓
Result
 ↓
LLM
 ↓
Answer
```

------------------------------------------------------------------------

## What is an AI Agent?

AI Agent is the broader term for systems where an AI model can:

-   Understand a goal
-   Make decisions
-   Select tools
-   Perform actions
-   Observe results
-   Adapt its next action

A simple agent is therefore a type of AI agent.

------------------------------------------------------------------------

## What is a Deep Agent?

A **Deep Agent** is an advanced agent designed for complex, multi-step
tasks.

It may:

-   Break a large goal into smaller tasks
-   Plan its work
-   Use multiple tools
-   Maintain state or memory
-   Manage large amounts of context
-   Iterate and check results
-   Delegate work to sub-agents

Example:

``` text
Large Goal
    ↓
Create Plan
    ↓
Task 1 → Research
    ↓
Task 2 → Collect Data
    ↓
Task 3 → Compare
    ↓
Task 4 → Analyze
    ↓
Review
    ↓
Final Result
```

There is no single universally accepted definition of exactly when an
agent becomes a "deep agent"; it is best understood as a more capable
architecture for complex work.

------------------------------------------------------------------------

# Types of Agents

## Reactive Agents

React directly to the current input.

``` text
Input → Action
```

They generally perform little or no long-term planning.

## Tool-Using Agents

Use external tools such as:

-   Web search
-   APIs
-   Databases
-   Code execution

``` text
Question
 ↓
Agent
 ↓
Tool
 ↓
Result
```

## Planning Agents

Create a plan before performing actions.

``` text
Goal
 ↓
Plan
 ↓
Task 1 → Task 2 → Task 3
 ↓
Result
```

## Reflection / Reflexion Agents

Evaluate their own work and attempt to improve it.

``` text
Generate
 ↓
Critique
 ↓
Improve
```

A Reflexion-style system can also retain useful feedback or experience
for future attempts.

## Multi-Agent Systems

Multiple specialized agents collaborate.

``` text
Manager Agent
      │
 ┌────┼─────┐
 ↓    ↓     ↓
Research Coding Writing
Agent    Agent   Agent
```

## Deep Agents

Designed for sophisticated, multi-step, often long-running tasks and may
combine:

-   Planning
-   Tool use
-   Memory/state
-   Context management
-   Iteration
-   Sub-agents

------------------------------------------------------------------------

# Comparison

  Feature              Simple Agent   AI Agent        Deep Agent
  -------------------- -------------- --------------- ---------------
  Uses an LLM          Yes            Yes             Yes
  Tool usage           Sometimes      Usually         Extensive
  Planning             Limited        Possible        Strong
  Multi-step tasks     Limited        Yes             Yes
  Memory / State       Optional       Optional        Common
  Iteration            Basic          Possible        Extensive
  Multiple tools       Few            Several         Many
  Sub-agents           Rare           Possible        Common
  Context management   Basic          Moderate        Advanced
  Best for             Simple tasks   General tasks   Complex tasks

------------------------------------------------------------------------

# Example: Research Task

User asks:

> "Research the latest RAG techniques and create a detailed report."

### Simple Agent

``` text
Question → Search → Answer
```

### AI Agent

``` text
Question
 ↓
Search
 ↓
Read Results
 ↓
Search Again if Needed
 ↓
Answer
```

### Deep Agent

``` text
Goal
 ↓
Create Research Plan
 ↓
├── Research RAG Techniques
├── Research Recent Papers
├── Compare Approaches
├── Collect Sources
└── Analyze Findings
 ↓
Review Results
 ↓
Fill Missing Information
 ↓
Write Report
 ↓
Review Report
 ↓
Final Report
```

------------------------------------------------------------------------

# Where Does LangGraph Fit?

**LangGraph** is a framework for building stateful, controllable agent
workflows.

For example:

``` text
User
 ↓
LangGraph
 ├── Research Node
 ├── Retrieval Node
 ├── Grading Node
 ├── Web Search Node
 └── Generation Node
```

LangGraph itself is **not an agent**. It is a framework that can be used
to build agentic systems and workflows.

------------------------------------------------------------------------

# Simple Mental Model

``` text
LLM
 │
 │ generates text
 ▼
Tool-Using Agent
 │
 │ takes actions
 ▼
Planning Agent
 │
 │ breaks down tasks
 ▼
Deep Agent
 │
 │ manages complex work
 ▼
Multi-Agent System
```

This is a simplified mental model, not a strict industry classification.

------------------------------------------------------------------------

# Key Takeaways

-   An **LLM** primarily generates responses.
-   An **AI Agent** can use an LLM to make decisions and take actions.
-   A **simple/normal agent** usually handles straightforward tasks with
    a small number of tools.
-   **Planning agents** break complex goals into smaller tasks.
-   **Reflection/Reflexion agents** evaluate and improve their work.
-   **Multi-agent systems** use multiple specialized agents.
-   A **Deep Agent** is designed for complex, multi-step, long-running
    tasks and may combine planning, tools, memory, context management,
    iteration, and sub-agents.
-   **LangGraph** is a framework for building stateful agent workflows;
    it is not itself an agent.
