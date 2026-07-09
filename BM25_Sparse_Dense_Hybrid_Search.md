# BM25 Search, Sparse Search, Dense Search & Hybrid Search

## Overview

Modern Retrieval-Augmented Generation (RAG) systems retrieve relevant
documents before sending them to an LLM. There are three common
retrieval approaches:

1.  **Sparse Search (BM25 / keyword search)**
2.  **Dense Search (embedding/vector search)**
3.  **Hybrid Search (Sparse + Dense)**

------------------------------------------------------------------------

# 1. Sparse Search

Sparse search represents text using keyword-based features rather than
semantic embeddings.

The most widely used sparse retrieval algorithm is **BM25**.

## What is BM25?

BM25 (Best Matching 25) ranks documents based on: - Exact keyword
matches - Keyword frequency - Document length - Inverse Document
Frequency (IDF)

It **does not understand meaning**. It only scores documents using
keywords.

### Example

Documents:

-   **Doc 1:** "LangGraph Reflection Agent tutorial"
-   **Doc 2:** "Artificial Intelligence agents and planning"

Query:

    LangGraph Reflection Agent

BM25 returns **Doc 1** because it contains the exact keywords.

------------------------------------------------------------------------

# 2. Dense Search

Dense search converts text into numerical vectors (embeddings).

Instead of matching words, it matches **meaning**.

Example embedding pipeline:

    Text
       ↓
    Embedding Model
       ↓
    Vector

### Example

Documents:

-   **Doc 1:** "Machine Learning is a branch of Artificial
    Intelligence."
-   **Doc 2:** "Today's weather is sunny."

Query:

    Explain AI

Even though the document may not contain the exact phrase **"Explain
AI"**, dense search retrieves **Doc 1** because the meanings are
semantically similar.

------------------------------------------------------------------------

# Sparse vs Dense

  -----------------------------------------------------------------------
  Sparse (BM25)                       Dense Search
  ----------------------------------- -----------------------------------
  Keyword matching                    Semantic matching

  No embeddings                       Uses embeddings

  Finds exact terms                   Finds similar meaning

  Excellent for product names, error  Excellent for natural language
  codes, APIs                         questions
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 3. Hybrid Search

Hybrid search combines:

-   Sparse Search (BM25-style)
-   Dense Search (Embeddings)

```{=html}
<!-- -->
```
    User Query
          │
     ┌────┴────┐
     │         │
     ▼         ▼
    Sparse   Dense
    Search   Search
     │         │
     └────┬────┘
          ▼
    Score Fusion
          ▼
    Best Documents

This approach captures both: - Exact keyword matches - Semantic
similarity

It generally provides better retrieval quality than using only one
method.

------------------------------------------------------------------------

# Why Hybrid Search?

Suppose the query is:

    LangGraph StateGraph add_conditional_edges

Dense search understands the overall meaning.

Sparse search recognizes the exact API/function name.

Hybrid search benefits from both.

------------------------------------------------------------------------

# Which Vector Databases Support Hybrid Search?

  Vector Database    Dense Search     Hybrid Search
  ----------------- -------------- --------------------
  FAISS                   ✅                ❌
  ChromaDB                ✅        Limited / indirect
  Qdrant                  ✅                ✅
  Pinecone                ✅                ✅
  Milvus                  ✅                ✅
  Weaviate                ✅                ✅

------------------------------------------------------------------------

# Typical RAG Pipeline

    PDFs
       ↓
    Chunking
       ↓
    Embedding Model
       ↓
    Vector Database
       ↓
    Retriever
       ↓
    LLM

For hybrid search:

    User Query
          │
          ▼
    Embedding Model (Dense)
          │
    Sparse Representation (BM25/SPLADE)
          │
          ▼
    Hybrid Search in Vector Database
          │
          ▼
    Top Documents
          │
          ▼
    LLM

------------------------------------------------------------------------

# Key Takeaways

-   **BM25** is a keyword-based ranking algorithm.
-   **Sparse Search** focuses on exact term matching.
-   **Dense Search** uses embeddings to understand semantic meaning.
-   **Hybrid Search** combines sparse and dense retrieval for improved
    accuracy.
-   **Qdrant**, **Pinecone**, **Milvus**, and **Weaviate** support
    hybrid search.
-   **FAISS** supports only dense vector search.
-   Embedding quality often has a greater impact on retrieval
    performance than the choice of vector database.

------------------------------------------------------------------------

# Interview Questions

1.  What is BM25 and how does it rank documents?
2.  What is the difference between sparse and dense retrieval?
3.  Why are embeddings required for dense search?
4.  What are the advantages of hybrid search?
5.  Why would you choose Qdrant over FAISS for an advanced RAG system?
6.  When is BM25 better than dense search?
7.  Can hybrid search improve retrieval quality? Why?
