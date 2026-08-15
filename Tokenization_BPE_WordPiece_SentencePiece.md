# Tokenization Explained: BPE, WordPiece, and SentencePiece

## What is Tokenization?

**Tokenization** is the process of converting text into smaller units called **tokens** that an AI model can process.

```text
Text
  ↓
Tokenizer
  ↓
Tokens
  ↓
Token IDs
  ↓
Model
```

Neural networks work with numbers rather than raw text, so tokenization converts human language into a numerical representation.

---

## Why Do We Need Tokenization?

For example:

```text
"I love AI"
     ↓
["I", "love", "AI"]
     ↓
[42, 891, 305]
```

The exact tokens and IDs depend on the tokenizer.

---

# Types of Tokenization

Common approaches include:

- Word-level tokenization
- Character-level tokenization
- Subword tokenization

Modern LLMs commonly use **subword tokenization** because it provides a good balance between vocabulary size and handling rare or unknown words.

Three important approaches are:

1. **BPE (Byte Pair Encoding)**
2. **WordPiece**
3. **SentencePiece**

---

# 1. BPE (Byte Pair Encoding)

BPE starts with small units and repeatedly merges frequently occurring pairs.

For example, a tokenizer may learn pieces such as:

```text
low
er
est
```

Then:

```text
lower → low + er
lowest → low + est
```

This allows the tokenizer to represent both common and previously unseen words using smaller pieces.

### Where is BPE Used?

BPE and BPE-like tokenization are used by several popular language models, including GPT-family tokenizers.

---

# 2. WordPiece

**WordPiece** is another subword tokenization method.

It builds a vocabulary of useful subword units and selects pieces that efficiently represent words.

For example:

```text
playing
```

could be represented approximately as:

```text
play + ##ing
```

The `##` convention indicates a continuation of a word in many WordPiece tokenizers.

### Where is WordPiece Used?

WordPiece is strongly associated with:

- BERT
- DistilBERT
- ALBERT

---

# 3. SentencePiece

**SentencePiece** is a tokenizer framework that can train subword models directly from raw text.

An important advantage is that it does not require traditional whitespace-based word splitting.

It can use algorithms such as:

- BPE
- Unigram Language Model

### Where is SentencePiece Used?

SentencePiece is used by many multilingual and generative models, including model families such as:

- T5
- LLaMA
- ALBERT

---

# BPE vs WordPiece vs SentencePiece

| Feature | BPE | WordPiece | SentencePiece |
|---|---|---|---|
| Main idea | Merge frequent pairs | Select useful subwords | Tokenize raw text into subwords |
| Subword based | Yes | Yes | Yes |
| Requires whitespace splitting | Usually implementation-dependent | Commonly word-oriented | No |
| Common association | GPT-style tokenizers | BERT | T5, LLaMA |
| Handles rare words | Yes | Yes | Yes |

> Modern tokenizer implementations can differ, so the model name alone does not always reveal every tokenizer detail.

---

# Why Subword Tokenization is Important

Consider an uncommon word:

```text
unhappiness
```

A word-level tokenizer may require the complete word to exist in its vocabulary.

A subword tokenizer can break it into pieces such as:

```text
un + happiness
```

or:

```text
un + happy + ness
```

This allows the model to process words it has never encountered exactly before.

---

# Tokenization in an LLM

A simplified LLM pipeline looks like:

```text
User Text
    ↓
Tokenizer
    ↓
Tokens
    ↓
Token IDs
    ↓
Transformer
    ↓
Predicted Next Token
    ↓
Tokenizer / Decoder
    ↓
Generated Text
```

---

# Tokenization and Context Windows

LLM context windows are measured in **tokens**.

For example, if a model supports a 128,000-token context window, the relevant input and output must fit within that budget according to the model's rules.

Therefore:

```text
More tokens
     ↓
More context usage
     ↓
Potentially higher cost and computation
```

This is why token optimization is important when building LLM applications.

---

# Tokenization vs Embeddings

These concepts are related but different.

### Tokenization

```text
Text → Token IDs
```

### Embeddings

```text
Text → Vector
```

A simplified flow can be:

```text
"What is RAG?"
       ↓
Tokenizer
       ↓
Token IDs
       ↓
Transformer / Embedding Model
       ↓
Vector Representation
```

---

# Why Tokenization Matters in RAG

Tokenization affects:

- Chunk size
- Context-window usage
- Cost
- Latency
- Amount of information sent to the LLM

For example:

```text
Query
  ↓
Retriever
  ↓
Large chunks
  ↓
LLM
```

If retrieved chunks are unnecessarily large, they can consume many tokens.

Better chunking and token awareness can reduce unnecessary context.

---

# Simple Example

Suppose a user asks:

> "What is a vector database?"

A simplified tokenizer might produce:

```text
["What", "is", "a", "vector", "database", "?"]
```

These tokens are converted into IDs:

```text
[101, 2003, 1037, 9204, 7809, 1029]
```

The model processes numerical representations rather than the original text.

> The exact tokens and IDs vary depending on the tokenizer.

---

# Key Takeaways

- **Tokenization** converts text into tokens that AI models can process.
- Tokens can be words, subwords, characters, or other learned units.
- Modern LLMs commonly use **subword tokenization**.
- **BPE** learns frequent token merges.
- **WordPiece** learns useful subword units and is strongly associated with BERT.
- **SentencePiece** can tokenize raw text without requiring whitespace-based word splitting.
- Tokenization affects context-window usage, cost, and latency.
- Tokenization is different from embeddings: tokenization produces tokens/IDs, while embeddings produce numerical vector representations.
