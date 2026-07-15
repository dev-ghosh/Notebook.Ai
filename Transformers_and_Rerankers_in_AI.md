# Transformers and Rerankers in AI

## What are Transformers?

A **Transformer** is a deep learning architecture introduced in the
paper **"Attention Is All You Need" (2017)**. It processes all words in
parallel using **self-attention**, making it the foundation of modern
NLP.

### Advantages

-   Understands long-range dependencies
-   Parallel processing
-   Faster training
-   Better contextual understanding

## Types of Transformers

### 1. Encoder-Only

Examples: BERT, RoBERTa, MiniLM, BAAI/bge-base-en-v1.5, E5

Uses: - Embeddings - Semantic Search - Classification

### 2. Decoder-Only

Examples: GPT, Llama, Mistral, Gemma, Claude

Uses: - Chatbots - Text Generation - Code Generation

### 3. Encoder-Decoder

Examples: T5, BART, FLAN-T5

Uses: - Translation - Summarization

------------------------------------------------------------------------

# What are Rerankers?

A **Reranker** is a Transformer model that reorders documents returned
by a vector database according to their relevance.

Workflow:

Documents → Embedding Model → Vector Database → Retrieve Top 20 →
Reranker → Keep Best 5 → LLM

## Embedding Model vs Reranker

  Feature                      Embedding Model   Reranker
  ---------------------------- ----------------- ----------
  Creates vectors              Yes               No
  Used before retrieval        Yes               No
  Used after retrieval         No                Yes
  Searches vector DB           Yes               No
  Scores retrieved documents   No                Yes

## Popular Rerankers

-   BAAI/bge-reranker-base
-   BAAI/bge-reranker-large
-   Cohere Rerank
-   Jina Reranker

## Key Takeaways

-   Transformers are the foundation of modern AI models.
-   Encoder models are mainly used for embeddings.
-   Decoder models are mainly used for text generation.
-   Encoder-Decoder models are used for translation and summarization.
-   Rerankers improve retrieval quality before the LLM generates the
    answer.
