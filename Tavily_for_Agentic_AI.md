# Tavily for Agentic AI - Beginner Notes

## What is Tavily?

Tavily is a search and web data platform designed specifically for AI
agents and LLM applications. It provides structured web information that
is easier for AI systems to consume than traditional search results.

## Why Use Tavily?

-   Live web search
-   Website crawling
-   Content extraction
-   AI-friendly responses
-   Easy integration with LangChain

## Tavily Tools

### Tavily Search

Searches the web and returns relevant results.

Example: User asks: "Latest LangGraph updates"

Agent -\> Tavily Search -\> Relevant pages -\> LLM summarizes.

### Tavily Crawl

Crawls an entire website by following internal links.

Useful for indexing documentation websites into a vector database.

### Tavily Extract

Extracts the main content from one or more URLs, removing unnecessary
HTML.

Useful for RAG ingestion pipelines.

### Tavily Map

Discovers important pages on a website without downloading everything.

Useful for finding documentation sections before crawling.

## Agentic AI Workflow

User → AI Agent → Tavily Search / Crawl / Extract / Map → LLM or RAG
System → Final Answer

## Real Example

Documentation Assistant:

1.  Tavily Map discovers documentation pages.
2.  Tavily Crawl collects them.
3.  Tavily Extract cleans the text.
4.  Chunk documents.
5.  Generate embeddings.
6.  Store in Qdrant.
7.  Retrieve relevant chunks during user queries.

## When to Use Each Tool

  Tool             Purpose
  ---------------- ------------------------------
  Tavily Search    Search the live web
  Tavily Crawl     Crawl an entire website
  Tavily Extract   Extract clean text from URLs
  Tavily Map       Discover important pages

## Advantages

-   Built for AI agents
-   Structured responses
-   Great for RAG
-   LangChain integration
-   Reduces manual scraping

## Key Takeaways

-   Tavily is designed for AI-first web access.
-   Search retrieves live information.
-   Crawl collects website content.
-   Extract cleans web pages.
-   Map discovers useful pages before crawling.
