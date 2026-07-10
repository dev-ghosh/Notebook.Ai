# Embedding Models, Dense vs Sparse, and Qdrant Notes

## What is an Embedding Model?

An embedding model converts text into numerical vectors so computers can compare meaning.

Example:

```text
"What is LangGraph?"
      ↓
Embedding Model
      ↓
[0.12, -0.45, 0.89, ...]
```

---

# Types of Embedding Models

## 1. Dense Embedding Models

Examples:
- BAAI/bge-base-en-v1.5
- BAAI/bge-small-en-v1.5
- sentence-transformers/all-MiniLM-L6-v2
- nomic-ai/nomic-embed-text-v1.5

Output:

```text
[0.23, -0.81, 0.45, 0.71, ...]
```

Used for semantic search.

---

## 2. Sparse Embedding Models

Examples:
- SPLADE
- Qdrant FastEmbed Sparse Models
- MiniCOIL

Conceptual output:

```text
{
  42: 0.93,
  187: 1.45,
  904: 0.62
}
```

Used for keyword-based retrieval.

---

## 3. Multi-Representation Models

Example:
- BAAI/bge-m3

These are useful in advanced retrieval pipelines but do not automatically enable hybrid search.

---

# Dense vs Sparse

| Dense | Sparse |
|---|---|
| Understands meaning | Matches keywords |
| Dense vectors | Sparse vectors |
| Great for natural language | Great for API names, error codes, product names |

---

# Example

Documents

```text
Doc 1:
LangGraph supports add_conditional_edges()

Doc 2:
StateGraph supports dynamic workflow execution.
```

Query:

```text
How do I create dynamic routing in LangGraph?
```

Dense retrieval understands:

```text
dynamic routing ≈ add_conditional_edges()
```

Sparse retrieval focuses on exact keywords.

---

# Why Don't We Use Only Sparse Embeddings with Qdrant?

Qdrant supports:

- Dense Search
- Sparse Search
- Hybrid Search

It searches whatever vectors you store.

Only dense:

```text
Documents
   ↓
Dense Model
   ↓
Dense Vectors
   ↓
Qdrant
   ↓
Dense Search
```

Only sparse:

```text
Documents
   ↓
Sparse Model
   ↓
Sparse Vectors
   ↓
Qdrant
   ↓
Sparse Search
```

Both:

```text
                  Documents
                       │
        ┌──────────────┴──────────────┐
        ▼                             ▼
 Dense Embedding Model       Sparse Embedding Model
        │                             │
 Dense Vectors               Sparse Vectors
        └──────────────┬──────────────┘
                       ▼
                    Qdrant
                       ▼
                 Hybrid Search
```

---

# Why Dense Embeddings Are Still Needed

Dense embeddings understand semantic meaning.

Example:

Document:

```text
LangGraph supports add_conditional_edges().
```

Query:

```text
How do I create dynamic routing?
```

Dense retrieval understands the relationship and retrieves the correct document.

Sparse retrieval is stronger for exact identifiers such as:

- add_conditional_edges
- HTTP 404
- ORA-12541
- Depends()

Neither is universally better—they complement each other.

---

# Recommendation for My Advanced RAG

- Vector Database: Qdrant
- Dense Embedding Model: BAAI/bge-base-en-v1.5
- Start with Dense Search
- Later add BM25 or another sparse retriever for Hybrid Search

---

# Key Takeaways

- Most embedding models are dense.
- Sparse embedding models also exist.
- Dense = semantic understanding.
- Sparse = keyword matching.
- Hybrid = Dense + Sparse.
- Qdrant supports all three retrieval modes.
