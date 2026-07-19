# Function Calling vs ReAct Prompting

## Introduction

Both **Function Calling** and **ReAct (Reason + Act)** enable LLMs to
use external tools, but they solve different problems.

-   **Function Calling** answers: *How does the model execute a tool?*
-   **ReAct Prompting** answers: *How does the model decide when and why
    to use a tool?*

------------------------------------------------------------------------

# Function Calling

## Definition

Function Calling is a capability where the LLM returns a structured
function name and arguments instead of directly answering the user.

Example function:

``` python
def get_weather(city):
    ...
```

User:

> What is the weather in Delhi?

Model output:

``` json
{
  "name": "get_weather",
  "arguments": {
    "city": "Delhi"
  }
}
```

Application:

``` python
result = get_weather("Delhi")
```

Tool returns:

    32°C

Final response:

> The weather in Delhi is 32°C.

### Workflow

    User
     ↓
    LLM
     ↓
    Structured Function Call
     ↓
    Application Executes Function
     ↓
    Tool Result
     ↓
    LLM Final Answer

### Advantages

-   Reliable structured output
-   Easy API integration
-   Great for databases, calculators, APIs

### Limitations

-   Doesn't provide a reasoning process
-   Usually one tool call at a time

------------------------------------------------------------------------

# ReAct Prompting

## Definition

ReAct stands for **Reason + Act**.

The model repeatedly reasons, performs actions, observes results, and
reasons again until it has enough information.

Example

User:

> Who is the CEO of Tesla?

Agent:

    Thought:
    I need current information.

    Action:
    Search the web.

    Observation:
    Tesla CEO is Elon Musk.

    Thought:
    I now have enough information.

    Final Answer:
    Elon Musk is the CEO of Tesla.

### Workflow

    Question
       │
    Thought
       │
    Action
       │
    Observation
       │
    Thought
       │
    Action
       │
    Observation
       │
    Final Answer

### Advantages

-   Multi-step reasoning
-   Multiple tool usage
-   Better for complex agents

### Limitations

-   Slower
-   More LLM calls

------------------------------------------------------------------------

# Comparison Example

Question:

> What is the population density of Japan?

## Function Calling

1.  Call `get_country_data("Japan")`
2.  Receive population and area.
3.  Compute density.
4.  Return answer.

## ReAct

    Thought:
    Need population.

    Action:
    Search population.

    Observation:
    125 million.

    Thought:
    Need area.

    Action:
    Search area.

    Observation:
    377,975 km².

    Thought:
    Calculate density.

    Final Answer:
    ≈331 people/km².

------------------------------------------------------------------------

# Key Differences

  -----------------------------------------------------------------------
  Feature                 Function Calling        ReAct Prompting
  ----------------------- ----------------------- -----------------------
  Primary purpose         Execute tools           Reason then use tools

  Reasoning               Minimal                 Explicit iterative
                                                  reasoning

  Tool calls              Usually single          Multiple possible

  Output                  Structured JSON         Thought → Action →
                                                  Observation

  Best for                APIs, calculators,      AI agents, research,
                          databases               planning
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Do They Work Together?

Yes. Modern agents combine both.

    User
      │
      ▼
    ReAct Reasoning
      │
      ▼
    Function Calling
      │
      ▼
    Tool Execution
      │
      ▼
    Observation
      │
      ▼
    ReAct Continues
      │
      ▼
    Final Answer

ReAct decides **which tool** to use and **when**. Function Calling is
the mechanism that actually invokes the tool.

------------------------------------------------------------------------

# Relation to LangChain and LangGraph

-   `create_react_agent()` implements the ReAct reasoning pattern.
-   Tool execution typically uses the model's tool/function-calling
    capability.
-   LangGraph lets you orchestrate these reasoning and tool steps into
    workflows.

------------------------------------------------------------------------

# Which Should You Use?

-   Use **Function Calling** when you need structured interaction with
    APIs or Python functions.
-   Use **ReAct Prompting** when building autonomous agents that must
    decide which tools to use.
-   For advanced systems like Reflexion Agents, combine **ReAct +
    Function Calling + Reflection/Memory** for the best results.
