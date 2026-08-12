# LangChain vs LangGraph vs LangSmith

## Introduction

LangChain, LangGraph, and LangSmith are related tools in the LangChain
ecosystem, but they solve different problems.

``` text
LangChain  → Build AI application components
LangGraph  → Build and control complex AI workflows/agents
LangSmith  → Test, trace, evaluate, and monitor AI applications
```

## 1. What is LangChain?

**LangChain** is a framework for building applications powered by Large
Language Models (LLMs).

It provides reusable components for: - LLMs and chat models - Prompts -
Embeddings - Vector stores - Retrievers - Tools - Agents - Output
parsers - Document loaders

Example:

``` python
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_template(
    "Explain {topic} in simple terms."
)
```

Think of LangChain as a collection of **building blocks** for LLM
applications.

## 2. What is LangGraph?

**LangGraph** is a framework for building **stateful, multi-step, and
controllable AI workflows and agents**.

It is useful when an application needs: - Multiple steps - Conditional
logic - Loops - State - Tool usage - Human-in-the-loop workflows -
Agentic behavior

Example:

``` text
START
  ↓
Retrieve
  ↓
Grade Documents
  ↓
Relevant?
 ↙       ↘
Yes       No
 ↓         ↓
Generate  Web Search
 ↓         ↓
Answer ←───┘
```

LangGraph is especially useful for Adaptive RAG, Corrective RAG,
Self-RAG, reflection agents, and multi-agent systems.

## 3. What is LangSmith?

**LangSmith** is a platform for **observability, debugging, testing, and
evaluation of LLM applications**.

It can help developers inspect: - LLM calls - Prompts - Outputs - Tool
calls - Retrieval results - Latency - Token usage - Errors - Agent
execution steps

For example, if a RAG system gives a poor answer, LangSmith can help
identify whether the problem came from retrieval, context, the LLM, or
the workflow.

## Main Difference

  -----------------------------------------------------------------------
  Tool        Main Purpose                 Simple Meaning
  ----------- ---------------------------- ------------------------------
  LangChain   Build LLM application        Building blocks
              components                   

  LangGraph   Build complex AI             Workflow engine
              workflows/agents             

  LangSmith   Debug, evaluate, and monitor Observability platform
              AI apps                      
  -----------------------------------------------------------------------

## How They Work Together

``` text
                 AI Application
                       │
            ┌──────────┴──────────┐
            │                     │
        LangChain             LangGraph
            │                     │
     Components            Agent / Workflow
            │                     │
            └──────────┬──────────┘
                       ↓
                  LangSmith
                       │
              Trace / Evaluate /
              Debug / Monitor
```

## Example: Advanced RAG

### LangChain

You can use LangChain for: - Document loaders - Text splitting -
Embeddings - Retrievers - Prompts - LLM calls

``` text
Documents
   ↓
Text Splitter
   ↓
Embeddings
   ↓
Qdrant
   ↓
Retriever
```

### LangGraph

You can use LangGraph to control the workflow:

``` text
Question
   ↓
Route Question
   ↓
Retrieve
   ↓
Grade Documents
   ↓
Relevant?
 ↙       ↘
Yes      No
 ↓        ↓
Generate  Web Search
 ↓        ↓
Answer ←──┘
```

### LangSmith

You can use LangSmith to inspect and evaluate the execution of the
application.

## LangChain vs LangGraph

**LangChain** focuses on components and integrations:

``` text
Prompt + LLM + Retriever + Tool
```

**LangGraph** focuses on workflow orchestration and state:

``` text
Node → Node → Decision → Node → Loop
```

LangGraph can use LangChain components inside its nodes.

## LangSmith vs LangChain

They have different purposes:

``` text
LangChain
    ↓
Build Application
    ↓
LangSmith
    ↓
Trace + Debug + Evaluate
```

## Simple Analogy

Imagine building a car:

-   **LangChain = Parts:** reusable components for the application.
-   **LangGraph = Control System:** controls how components work
    together.
-   **LangSmith = Dashboard + Diagnostics:** shows what happened and
    helps find problems.

## When Should You Use Each?

### Use LangChain When:

-   Building an LLM application
-   Working with prompts
-   Calling LLMs
-   Building RAG pipelines
-   Connecting tools and retrievers

### Use LangGraph When:

-   Your application has multiple steps
-   You need state
-   You need conditional routing
-   You need loops
-   You are building agents
-   You are building complex RAG workflows

### Use LangSmith When:

-   Debugging an LLM application
-   Tracing agent execution
-   Evaluating responses
-   Monitoring applications
-   Comparing prompts or models
-   Finding retrieval or generation problems

## Key Takeaways

-   **LangChain** helps build LLM-powered applications using reusable
    components.
-   **LangGraph** helps build stateful and complex AI workflows and
    agents.
-   **LangSmith** helps trace, debug, evaluate, and monitor those
    applications.
-   LangChain and LangGraph can be used together.
-   LangSmith can observe applications built with LangChain and
    LangGraph.
-   They are complementary tools, not direct alternatives.
