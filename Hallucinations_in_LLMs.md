# Hallucinations in Large Language Models (LLMs)

## What are Hallucinations?

A hallucination occurs when an LLM generates information that is
incorrect, fabricated, or unsupported while presenting it confidently.

The model is not intentionally lying---it predicts the most likely next
tokens based on patterns learned during training.

## Why Do Hallucinations Happen?

-   Limited knowledge
-   Missing context
-   Ambiguous prompts
-   Poor retrieval in RAG systems
-   Weak prompt engineering

## Example

**Question:** Who invented Python?

**Hallucinated Answer:** Elon Musk invented Python.

❌ Incorrect

**Correct Answer:** Guido van Rossum created Python.

## Types of Hallucinations

1.  Factual Hallucinations
2.  Contextual Hallucinations
3.  Fabricated Citations
4.  Fabricated Code

## How to Reduce Hallucinations

### 1. Retrieval-Augmented Generation (RAG)

Provide relevant documents from a vector database before generation.

### 2. Better Prompt Engineering

Example: "Answer only from the provided context. If the answer is
unavailable, say 'I don't know.'"

### 3. Improve Retrieval

-   Better embedding models
-   Better chunking
-   Metadata filtering
-   Hybrid search

### 4. Use a Reranker

Retrieve many documents, rerank them, and send only the best ones to the
LLM.

### 5. Corrective RAG

Check retrieved documents and retrieve again if necessary.

### 6. Self-RAG

Allow the model to evaluate and revise its own answer.

### 7. Adaptive RAG

Select the retrieval strategy based on the query.

### 8. Fact Verification

Verify important answers using trusted sources or APIs.

## Example: Without vs With RAG

Without RAG: - Model may answer using outdated knowledge.

With RAG: - Retrieve current documents. - Generate an answer using fresh
context.

## Hallucination Reduction Pipeline

User Query → Retriever → Vector Database → Top Documents → Reranker →
LLM → Self-Check / Corrective Step → Final Answer

## Best Practices

-   Use RAG
-   Use high-quality embeddings
-   Improve retrieval quality
-   Add rerankers
-   Use prompt engineering
-   Validate important responses

## Key Takeaways

-   Hallucinations are incorrect or unsupported outputs.
-   They occur because LLMs predict text rather than verify facts.
-   RAG, rerankers, prompt engineering, and verification significantly
    reduce hallucinations.
