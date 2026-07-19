# LangChain Token Limitation Handling Strategies

## Why do token limits matter?

Every Large Language Model (LLM) has a **context window**, which is the
maximum number of tokens it can process in a single request. The context
window includes:

-   System prompt
-   User prompt
-   Retrieved documents
-   Conversation history
-   Model output

If the total exceeds the model's context window, the request will fail
or documents must be reduced.

------------------------------------------------------------------------

# 1. Stuffing

## What is it?

Stuffing places **all retrieved documents into a single prompt** and
sends them to the LLM.

### Workflow

    Retrieve Documents
            │
            ▼
    Combine Everything
            │
            ▼
    Single LLM Call

### Advantages

-   Very simple
-   Fast (one LLM call)
-   Preserves complete context

### Disadvantages

-   Easily exceeds token limits
-   Not suitable for large document collections

### Best for

-   Small RAG applications
-   Few retrieved documents

------------------------------------------------------------------------

# 2. Map-Reduce

## What is it?

Map-Reduce breaks a large document collection into chunks.

Each chunk is processed independently (**Map**), then the partial
outputs are combined (**Reduce**).

### Workflow

    Documents
       │
       ├── Chunk 1 → LLM
       ├── Chunk 2 → LLM
       ├── Chunk 3 → LLM
       └── Chunk N → LLM
                │
                ▼
         Combine Summaries
                │
                ▼
          Final LLM Call

### Advantages

-   Handles very large datasets
-   Avoids context-window overflow
-   Scales well

### Disadvantages

-   Requires multiple LLM calls
-   May lose cross-document relationships

### Best for

-   Long reports
-   Books
-   Large document collections

------------------------------------------------------------------------

# 3. Refine

## What is it?

Refine processes documents sequentially.

The model creates an initial answer from the first document, then
iteratively improves that answer using each remaining document.

### Workflow

    Document 1
          │
          ▼
    Initial Answer
          │
          ▼
    Document 2
          │
          ▼
    Refined Answer
          │
          ▼
    Document 3
          │
          ▼
    Further Refined Answer
          │
          ▼
    Final Answer

### Advantages

-   Preserves information across documents
-   Produces detailed, progressively improved answers

### Disadvantages

-   Slower than Stuffing
-   More LLM calls
-   Errors early in the chain may propagate

### Best for

-   Research assistants
-   Detailed reports
-   High-quality RAG systems

------------------------------------------------------------------------

# Comparison

  Strategy       LLM Calls   Token Efficiency    Speed Best Use
  ------------ ----------- ------------------ -------- ---------------------------------
  Stuffing               1                Low     Fast Small document sets
  Map-Reduce          Many               High   Medium Large corpora and summarization
  Refine              Many               High     Slow Detailed answer generation

------------------------------------------------------------------------

# Which should you choose?

-   **Stuffing**: when all documents comfortably fit into the context
    window.
-   **Map-Reduce**: when you have many or very large documents.
-   **Refine**: when answer quality is more important than latency and
    you want the response to improve as each document is processed.
