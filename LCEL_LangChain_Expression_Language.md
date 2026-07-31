# LCEL (LangChain Expression Language)

## What is LCEL?

LCEL (**LangChain Expression Language**) is a way to build LangChain
pipelines by connecting components with the `|` (pipe) operator.

Instead of manually calling each component one after another, LCEL lets
you define the entire workflow as a single chain.

## Why Use LCEL?

Without LCEL:

``` python
prompt_value = prompt.invoke({"topic": "AI"})
response = llm.invoke(prompt_value)
final = parser.invoke(response)
```

With LCEL:

``` python
chain = prompt | llm | parser
result = chain.invoke({"topic": "AI"})
```

This is shorter, cleaner, and easier to maintain.

## How LCEL Works

``` text
Input
  │
  ▼
Prompt
  │
  ▼
LLM
  │
  ▼
Output Parser
  │
  ▼
Final Output
```

Each component automatically passes its output to the next.

## Common LCEL Components

-   PromptTemplate
-   ChatPromptTemplate
-   Chat Models
-   Output Parsers
-   Retrievers
-   RunnableLambda
-   RunnableParallel
-   RunnablePassthrough

## Example

``` python
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_groq import ChatGroq

prompt = ChatPromptTemplate.from_template(
    "Explain {topic} in simple words."
)

llm = ChatGroq(model="llama-3.3-70b-versatile")

chain = prompt | llm | StrOutputParser()

response = chain.invoke(
    {
        "topic": "Transformers"
    }
)

print(response)
```

## LCEL in RAG

``` python
generation_chain = prompt | llm | StrOutputParser()

answer = generation_chain.invoke(
    {
        "context": documents,
        "question": question
    }
)
```

This is the common pattern used in LangChain RAG pipelines.

## Advantages

-   Clean syntax
-   Less boilerplate
-   Easy to compose
-   Reusable
-   Supports async and streaming
-   Works well with LangGraph

## LCEL vs Traditional

  Traditional          LCEL
  -------------------- ----------------------
  Manual calls         Pipe operator
  More code            Less code
  Harder to maintain   Cleaner and reusable

## Key Takeaways

-   LCEL stands for LangChain Expression Language.
-   It connects components using the `|` operator.
-   The output of one component becomes the input of the next.
-   LCEL is widely used for RAG pipelines, AI agents, and LangGraph
    workflows.
