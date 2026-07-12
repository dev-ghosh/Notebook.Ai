# LangChain Hub and StrOutputParser Notes

## LangChain Hub

``` python
from langchain_classic import hub
prompt = hub.pull("rlm/rag-prompt")
```

`hub.pull()` downloads a reusable prompt from LangChain Hub.

-   `rlm` = owner/namespace
-   `rag-prompt` = prompt name

It usually returns a `ChatPromptTemplate`.

``` python
print(type(prompt))
```

Typical output:

``` text
<class 'langchain_core.prompts.chat.ChatPromptTemplate'>
```

### RAG Flow

User Question → Retriever → Retrieved Context →
`hub.pull("rlm/rag-prompt")` → LLM → Answer

Advantages: - Reuse community prompts - Rapid prototyping - Learn prompt
engineering - Customize later for production

## StrOutputParser

Without parser:

``` python
response = llm.invoke("What is AI?")
print(response.content)
```

With parser:

``` python
from langchain_core.output_parsers import StrOutputParser

chain = prompt | llm | StrOutputParser()
answer = chain.invoke({"question":"What is AI?"})
```

The parser converts an `AIMessage` into a plain Python `str`.

### Visual Flow

Without parser: Prompt → LLM → AIMessage → `.content`

With parser: Prompt → LLM → StrOutputParser → Python string

### StrOutputParser vs with_structured_output()

  StrOutputParser        with_structured_output()
  ---------------------- -----------------------------------
  Returns `str`          Returns validated Pydantic object
  For normal text        For structured data
  No schema validation   Schema validation

## Quick Summary

-   LangChain Hub stores reusable prompts.
-   `hub.pull()` downloads prompts such as `rlm/rag-prompt`.
-   Returned object is usually a `ChatPromptTemplate`.
-   `StrOutputParser` extracts only the text from an LLM response.
-   Use `with_structured_output()` when your program needs structured,
    validated outputs.
