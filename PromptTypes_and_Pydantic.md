# LangChain & Pydantic Summary

## PromptTemplate vs ChatPromptTemplate

### PromptTemplate

-   Used for creating a **single text prompt**.
-   Best suited for traditional text completion models.
-   Produces one formatted string.
-   Does not distinguish between system, user, or assistant roles.

Example:

``` python
from langchain_core.prompts import PromptTemplate

prompt = PromptTemplate.from_template(
    "Answer the following question:\n{question}"
)
```

### ChatPromptTemplate

-   Used with modern **chat models** (ChatGroq, GPT, Gemini, Claude,
    Llama, etc.).
-   Produces a list of chat messages.
-   Supports roles like **system**, **human**, and **assistant**.
-   Recommended for RAG, Agents, and LangGraph projects.

Example:

``` python
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant."),
    ("human", "{question}")
])
```

### Key Difference

  PromptTemplate       ChatPromptTemplate
  -------------------- ---------------------------------------------
  Creates one string   Creates chat messages
  No roles             Supports system/human/assistant roles
  Simpler              More flexible and preferred for chat models

------------------------------------------------------------------------

# What is Pydantic?

Pydantic is a Python library for **data validation, parsing, and
serialization** using Python type hints.

It helps ensure that data has the correct structure and type before your
program uses it.

Example:

``` python
from pydantic import BaseModel

class Student(BaseModel):
    name: str
    age: int
```

Benefits: - Validates input - Checks data types - Converts compatible
values automatically (e.g., `"20"` → `20`) - Produces clear validation
errors

------------------------------------------------------------------------

# BaseModel

`BaseModel` is the parent class from which every Pydantic model
inherits.

It allows you to define a schema for your data.

Example:

``` python
from pydantic import BaseModel

class GradeDocuments(BaseModel):
    binary_score: str
```

In LangChain, BaseModel is commonly used with:

``` python
structured_llm = llm.with_structured_output(GradeDocuments)
```

This ensures the LLM returns data matching the schema instead of
unpredictable free-form text.

------------------------------------------------------------------------

# Field

`Field()` adds metadata and validation rules to model fields.

Example:

``` python
from pydantic import BaseModel, Field

class GradeDocuments(BaseModel):
    binary_score: str = Field(
        description="Whether the retrieved documents are relevant. Answer only 'yes' or 'no'."
    )
```

## Why Field is important in LangChain

The `description` is passed to the LLM as guidance when using structured
outputs, helping it produce correctly formatted responses.

`Field()` can also provide: - Default values - Numeric limits (`gt`,
`lt`) - String length constraints - Regular-expression validation -
Descriptions for documentation and LLM guidance

------------------------------------------------------------------------

# Quick Summary

-   **PromptTemplate**: Builds a single text prompt.
-   **ChatPromptTemplate**: Builds role-based chat prompts; preferred
    for modern chat models.
-   **Pydantic**: Validates and structures Python data.
-   **BaseModel**: Defines the schema for structured data.
-   **Field()**: Adds metadata and validation; in LangChain,
    `description` helps guide the LLM's structured output.
