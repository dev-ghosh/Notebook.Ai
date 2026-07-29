# MCP Transport Layers and Sampling (Beginner Notes)

## Transport Layer

The transport layer is the communication channel between an MCP Client
and an MCP Server.

### STDIO

-   Uses standard input/output.
-   Client starts the server as a local process.
-   Best for local development and testing.
-   No network required.

### Streamable HTTP

-   Uses HTTP with streaming support.
-   Best for remote and cloud deployments.
-   Supports multiple clients.
-   Common for production systems.

## STDIO vs Streamable HTTP

  Feature       STDIO       Streamable HTTP
  ------------- ----------- -----------------
  Local         Yes         Optional
  Internet      No          Usually Yes
  Development   Excellent   Good
  Production    Limited     Excellent
  Multi-user    No          Yes

## Sampling in MCP

Sampling allows an MCP Server to request the client's configured LLM to
perform an AI task.

Workflow:

User → MCP Client → MCP Server → Sampling Request → Client's LLM →
Result → MCP Server → User

### Example

A code-analysis MCP server reads project files, asks the client's LLM to
summarize them through sampling, and returns the summary.

### Benefits

-   Reuses the client's model
-   Keeps servers lightweight
-   Produces consistent results with the user's chosen LLM

## Key Takeaways

-   STDIO is ideal for local MCP development.
-   Streamable HTTP is ideal for production deployments.
-   Sampling lets servers delegate AI inference to the client's LLM.
