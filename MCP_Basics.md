# Model Context Protocol (MCP) - Beginner Notes

## What is MCP?

Model Context Protocol (MCP) is an open standard that lets AI models
communicate with external tools, applications, databases, and services
using a common protocol.

## Why is MCP Needed?

Without MCP, every tool has a different API. MCP provides one standard
way for AI applications to connect with many tools.

## Where is MCP Used?

-   AI agents
-   AI assistants
-   File systems
-   Databases
-   GitHub
-   Email tools
-   External APIs

## Main Components

### MCP Host

The AI application the user interacts with.

### MCP Client

Lives inside the host application. It sends requests to MCP servers and
receives responses.

### MCP Server

Provides tools or resources such as file access, databases, GitHub, or
search.

### AI Model

The LLM decides when a tool should be used.

## Workflow

User → Host Application → MCP Client → MCP Server → Tool / Database /
API → MCP Client → AI Model → Final Answer

## Example

User: "List all Python files in my project."

1.  AI decides it needs a file tool.
2.  MCP Client sends a request.
3.  File System MCP Server reads the folder.
4.  Results are returned.
5.  AI presents the answer.

## Advantages

-   Standard protocol
-   Easier integrations
-   Reusable tool servers
-   Simplifies AI agent development

## MCP vs Traditional APIs

  Traditional APIs                  MCP
  --------------------------------- ----------------------
  Different API for every service   One common protocol
  Custom integration                Standard integration
  Harder to maintain                Easier to extend

## Key Takeaways

-   MCP = Model Context Protocol.
-   MCP standardizes communication between AI models and external tools.
-   MCP Client sends requests.
-   MCP Server exposes tools.
-   The AI model decides when tools are needed.
