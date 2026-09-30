# TypeSafe JEV — What It Is, What It Is Used For, and Example

## 1. What is TypeSafe JEV?

**JEV** is a new AI model/system from **TypeSafe** designed around the idea of a **System 1 model**.

The main idea is to make an AI system that can perform many tasks with a fast, direct style of reasoning instead of relying on the long, expensive reasoning process commonly associated with System 2-style reasoning models.

A simple way to think about it:  

> **Traditional fast LLM:** Generate an answer directly.  
> **Reasoning model:** Spend additional compute thinking through the problem before answering.  
> **JEV/System 1 approach:** Use a trained model that is optimized to make useful decisions/actions quickly, particularly in agentic workflows.

JEV is particularly interesting for applications where an AI agent has to repeatedly decide **what information to retrieve, which tool to use, or which result is useful**.

---

## 2. System 1 vs System 2

The terms "System 1" and "System 2" are inspired by the distinction between fast and deliberate thinking.

### System 1

System 1 is generally:

- Fast
- Automatic
- Low-latency
- Suitable for repeated decisions
- Useful when a decision does not require extensive reasoning

For AI systems, a System 1 model can be useful when an application needs to make many small decisions quickly.

### System 2

System 2 is generally:

- Slower
- More deliberate
- More computationally expensive
- Useful for difficult multi-step problems
- More suitable when the model needs substantial reasoning

For example:

```text
User question
      ↓
Reasoning model
      ↓
Long reasoning process
      ↓
Final answer
```

This can produce strong results, but it can also increase latency and computational cost.

---

# 3. Why is JEV interesting?

One important use case is **information retrieval and RAG**.

A normal RAG pipeline might look like:

```text
User Query
    ↓
Embedding Model
    ↓
Vector Search
    ↓
Top-K Documents
    ↓
LLM
    ↓
Answer
```

The problem is that vector similarity alone does not always select the best documents.

For example, suppose the query is:

> "What hardware is required to run a 70B parameter model?"

A semantic search system may return documents containing words and concepts related to:

- GPUs
- AI hardware
- model deployment
- VRAM
- inference

But the retrieved documents may not all directly answer the question.

A **reranker** can evaluate the retrieved documents and determine which ones are actually relevant.

This is where a model such as JEV can be interesting for retrieval/agent workflows.

---

# 4. JEV as a Reranking / Retrieval Component

Consider a RAG system containing 100,000 documents.

A user asks:

> "How much VRAM is required to run a 70B model using INT4 quantization?"

The system could first perform a fast retrieval:

```text
100,000 documents
        ↓
    Search
        ↓
    Top 50
```

Then JEV can be used as a decision/ranking component:

```text
Top 50 documents
        ↓
       JEV
        ↓
Relevant documents
        ↓
      Top 5
        ↓
       LLM
        ↓
     Answer
```

The important distinction is:

**Search finds candidates.**

**Reranking determines which candidates are more useful.**

---

# 5. Example: Hybrid RAG + Reranking

A stronger RAG architecture can combine several retrieval methods.

```text
                    User Query
                        |
              +---------+---------+
              |                   |
          BM25 Search        Vector Search
              |                   |
           Top 20              Top 20
              |                   |
              +---------+---------+
                        |
                   Merge Results
                        |
                     Top 40
                        |
                    JEV/Reranker
                        |
                     Top 5
                        |
                     LLM
                        |
                  Final Answer
```

### BM25

BM25 is a keyword-based search algorithm.

It is good when the query contains exact terms.

Example:

> "Qdrant collection vector size 768"

BM25 can strongly match documents containing:

- Qdrant
- collection
- vector
- 768

### Semantic Search

Semantic/vector search finds documents based on meaning.

For example:

> "How much memory does a large language model need?"

It can retrieve documents discussing:

- model weights
- VRAM
- RAM
- quantization
- inference memory

even if the exact wording is different.

### Reranker

The reranker looks at the query and retrieved documents together and determines which documents are most relevant.

---

# 6. A Simple Example

Imagine the user asks:

> "What is the VRAM requirement for running a 70B model in INT4?"

The initial search returns:

### Document A

> "70B parameter models contain approximately 70 billion parameters. Quantization reduces the memory required for storing model weights."

### Document B

> "NVIDIA GPUs are commonly used for large language model inference."

### Document C

> "INT4 quantization stores model weights using approximately 4 bits per parameter."

### Document D

> "A 7B model can run on consumer GPUs with appropriate quantization."

All four documents are related to the topic.

However, Documents A and C are likely more directly useful for the exact question.

A reranker can score the query-document relationships and prioritize the most relevant documents.

The final RAG pipeline might therefore use:

```text
Query
  ↓
BM25 + Vector Search
  ↓
A, B, C, D
  ↓
Reranker
  ↓
A, C
  ↓
LLM
  ↓
Answer
```

---

# 7. How This Differs From Using an LLM Directly

A general LLM can also be asked:

> "Which of these 50 documents are relevant?"

But doing this repeatedly can be expensive and slow.

A specialized model/system designed for fast decision-making can be useful for these repeated operations.

For example:

```text
100 queries
×
50 candidate documents
=
5,000 relevance decisions
```

If every decision requires a large reasoning model, the system can become expensive and slow.

A fast specialized model can make these decisions more efficiently.

---

# 8. JEV in an Agentic System

JEV is not limited to RAG.

An AI agent repeatedly needs to make decisions such as:

```text
Should I search?
      ↓
Which tool should I use?
      ↓
Which result is relevant?
      ↓
Do I need another search?
      ↓
Which information should be kept?
```

A fast decision-oriented model can potentially be useful for these kinds of operations.

Example:

```text
User
 ↓
Agent
 ↓
JEV
 ├── Search Web
 ├── Search Database
 ├── Call API
 └── Use Existing Context
          ↓
       Result
          ↓
        JEV
          ↓
    Is information sufficient?
       /               Yes           No
      ↓             ↓
    Answer       Search Again
```

This can reduce unnecessary expensive LLM calls.

---

# 9. JEV and Reinforcement Learning

JEV is particularly interesting in the context of **reinforcement learning**.

Instead of only training a model to predict the next token, an AI system can be trained around a reward signal.

A simplified concept is:

```text
Model makes decision
        ↓
Environment evaluates decision
        ↓
Reward
        ↓
Model learns
```

For example, in a retrieval task:

```text
Query
 ↓
Model selects documents
 ↓
Documents are evaluated
 ↓
Relevant → higher reward
Irrelevant → lower reward
 ↓
Model improves
```

This is different from simply teaching the model to imitate example answers.

---

# 10. RLHF vs RLVR vs RLCD

These terms are useful when understanding modern AI training.

## RLHF

**Reinforcement Learning from Human Feedback**

Humans provide preferences or feedback.

```text
Model Output
     ↓
Human Feedback
     ↓
Reward
     ↓
Model Training
```

Example:

Two answers are generated:

- Answer A
- Answer B

A human says A is better.

That preference can be used to train the model.

---

## RLVR

**Reinforcement Learning with Verifiable Rewards**

Instead of depending primarily on human judgment, the result can be checked automatically.

Example:

```text
2 + 2 = 4
```

A program can verify whether the answer is correct.

Therefore:

```text
Model
 ↓
Answer
 ↓
Automatic Verification
 ↓
Reward
```

This is especially useful for tasks with objectively checkable outcomes.

---

## RLCD

**Reinforcement Learning from Contrastive/Comparative Data**

The exact implementation can vary by system, but the central idea is to use comparisons or contrasts between outputs as a training signal.

A simplified example:

```text
Good behavior
      vs
Bad behavior
      ↓
Training signal
      ↓
Model learns preferred behavior
```

JEV's training approach is interesting because it focuses on creating a model that can make fast, useful decisions rather than simply increasing the amount of inference-time reasoning.

---

# 11. JEV vs Traditional Rerankers

A traditional reranker is usually designed specifically for relevance ranking.

Example:

```text
Query + Document
       ↓
Reranker
       ↓
Relevance Score
```

A JEV-style system can be thought of more broadly as a decision-oriented component.

Depending on the exact implementation, it can potentially be used for:

- Retrieval decisions
- Ranking
- Agent decisions
- Tool selection
- Information filtering
- Other repeated low-latency decisions

The exact capabilities and APIs should be checked against the current TypeSafe JEV documentation before implementing it in production.

---

# 12. Example RAG Architecture

For an advanced RAG project, an architecture could look like this:

```text
                 USER QUERY
                     |
          +----------+----------+
          |                     |
       BM25 Search        Vector Search
          |                     |
       Top 20                  Top 20
          |                     |
          +----------+----------+
                     |
                  Merge
                     |
                  Top 40
                     |
                JEV/Reranker
                     |
                  Top 5
                     |
             Context Filtering
                     |
                    LLM
                     |
              Final Answer
```

This is often stronger than relying on only one retrieval method.

---

# 13. When Should You Use a JEV-Type System?

It can make sense when:

- Your application makes many repeated decisions.
- Latency matters.
- You need to rank/filter retrieved information.
- You are building an agent.
- You want to reduce unnecessary calls to a large reasoning model.
- You need a component that is optimized for fast decisions.

It may be less appropriate when:

- The task requires deep mathematical reasoning.
- The task requires a long chain of reasoning.
- You need a general-purpose conversational LLM.
- A simple keyword/vector search already solves the problem.

---

# 14. Simple Mental Model

The easiest way to remember the concept is:

```text
LLM
→ Generates language

Reasoning Model
→ Spends more compute solving difficult problems

Retriever
→ Finds candidate information

Reranker
→ Determines which retrieved information is most relevant

JEV / System-1 style model
→ Fast decision-making for repeated AI operations
```

These components do not necessarily replace one another.

They can work together.

---

# 15. Example: Advanced RAG

Suppose you are building a company-document assistant.

A user asks:

> "What are the hardware requirements mentioned in the government tender for this AI system?"

The pipeline could be:

```text
                User Query
                    ↓
             Query Processing
                    ↓
          +---------+---------+
          |                   |
       BM25              Vector Search
          |                   |
          +---------+---------+
                    ↓
               50 Documents
                    ↓
             JEV / Reranker
                    ↓
                Top 5
                    ↓
              Context Check
                    ↓
                 LLM
                    ↓
        Answer + Citations
```

The important point is that JEV/reranking happens **before the final LLM generation**.

The LLM receives a smaller set of higher-value documents instead of all retrieved documents.

---

# 16. Key Takeaways

1. **JEV is associated with TypeSafe's System 1 approach to AI.**
2. The key idea is **fast, efficient decision-making** rather than always relying on expensive extended reasoning.
3. It can be relevant to **RAG, retrieval, ranking, filtering, and agentic workflows**.
4. A reranking stage can improve the quality of context given to the final LLM.
5. BM25 and vector search find candidate documents; a reranker helps select the most relevant ones.
6. JEV should not automatically be viewed as a replacement for a general-purpose LLM.
7. For complex reasoning, a dedicated reasoning model may still be more appropriate.
8. The strongest architecture can combine multiple specialized components:

```text
Fast Search
    +
Semantic Search
    +
Reranking / Decision Model
    +
LLM
    =
Advanced RAG / Agent System
```

---

## Important Note

JEV is a relatively new technology, so its exact capabilities, APIs, model variants, training details, and recommended use cases can change. For implementation, always check the latest official TypeSafe documentation and repository rather than relying only on a conceptual description.
