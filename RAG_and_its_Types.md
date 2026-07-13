# Advanced RAG Types

## What is RAG?

**RAG (Retrieval-Augmented Generation)** is an AI architecture that
combines the power of **Large Language Models (LLMs)** with an external
knowledge source such as a **Vector Database**, **PDFs**, **web pages**,
or **company documents**.

Instead of relying only on the knowledge stored during training, the LLM
first retrieves relevant information from an external knowledge base and
then uses that information to generate an accurate, grounded response.

### Traditional RAG Workflow

``` text
            User Question
                  │
                  ▼
        Retrieve Relevant Documents
          (Vector Database)
                  │
                  ▼
      Pass Documents to the LLM
                  │
                  ▼
         Generate Final Answer
```

### Example

Suppose your vector database contains your company's HR documents.

**User Question**

> What is our company's maternity leave policy?

Traditional RAG: 1. Searches the vector database. 2. Retrieves the HR
policy document. 3. Sends the retrieved document to the LLM. 4. The LLM
generates an answer using that document.

------------------------------------------------------------------------

# Why Advanced RAG?

Traditional RAG assumes retrieval is always correct and sufficient.
Advanced RAG architectures improve this.

-   **Corrective RAG (CRAG):** Checks whether retrieved documents are
    relevant. If not, it performs another retrieval (often web search).
-   **Adaptive RAG:** Decides whether retrieval is needed before
    retrieving anything.
-   **Self-RAG:** Continuously reflects on retrieval quality and its own
    generated answer, retrieving more information if necessary.

------------------------------------------------------------------------

# Corrective RAG (CRAG)

## Workflow

``` text
User Question
      │
      ▼
Retrieve Documents
      │
      ▼
Grade Retrieved Documents
     / \
 Good  Bad
  │      │
  ▼      ▼
Answer  Web Search
           │
           ▼
     Generate Answer
```

### Example

Question: **Who won IPL 2025?**

Vector DB contains only IPL 2024 data.

CRAG detects the retrieved document is irrelevant, performs a web
search, retrieves the latest result, and generates the correct answer.

------------------------------------------------------------------------

# Adaptive RAG

## Workflow

``` text
User Question
      │
      ▼
Need Retrieval?
   /      \
 No       Yes
 │         │
 ▼         ▼
Answer   Retrieve Docs
             │
             ▼
          Generate
```

### Example

Question: **What is 10 × 12?**

No retrieval is needed.

Question: **What is our company's leave policy?**

Retrieval is required.

------------------------------------------------------------------------

# Self-RAG

## Workflow

``` text
User Question
      │
      ▼
Retrieve Documents
      │
      ▼
Self Reflection
      │
Enough Information?
   /      \
 Yes      No
 │         │
 ▼         ▼
Answer  Retrieve More
            │
            ▼
      Reflect Again
```

### Example

Question: **Explain LangGraph checkpoints.**

If the first retrieval is incomplete, the model retrieves additional
documents, reflects again, and only then generates the final answer.

------------------------------------------------------------------------

# Comparison

  Feature                          Traditional   CRAG           Adaptive       Self-RAG
  -------------------------------- ------------- -------------- -------------- ----------
  Always retrieves                 ✅            ✅             ❌             Usually
  Checks retrieval quality         ❌            ✅             ❌             ✅
  Uses web search fallback         ❌            ✅             Optional       Optional
  Decides if retrieval is needed   ❌            ❌             ✅             Can
  Multiple retrieval rounds        ❌            Usually once   Usually once   ✅
  Self-evaluates answer            ❌            ❌             ❌             ✅
