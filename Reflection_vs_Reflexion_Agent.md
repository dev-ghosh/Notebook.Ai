# Reflection Agent vs Reflexion Agent

## Introduction

Both **Reflection Agents** and **Reflexion Agents** improve the quality
of AI responses through self-evaluation.

-   **Reflection** improves the answer within the current interaction.
-   **Reflexion** improves future answers by learning from previous
    experiences using memory.

------------------------------------------------------------------------

## What is a Reflection Agent?

A Reflection Agent generates an answer, critiques it, and revises it if
needed.

### Workflow

User Question → Generate Answer → Self Critique → Improve Answer → Final
Response

### Characteristics

-   No long-term memory
-   Improves only the current response
-   Simpler architecture

### Example

The agent answers a question, realizes it missed an important concept,
revises the answer, and returns the improved version. The critique is
not stored after the task finishes.

------------------------------------------------------------------------

## What is a Reflexion Agent?

A Reflexion Agent extends reflection by storing lessons learned in
memory.

Future tasks can retrieve these memories to avoid repeating mistakes.

### Workflow

User Question → Generate Answer → Self Reflection → Store Memory →
Future Question → Retrieve Memory → Better Answer

### Characteristics

-   Uses long-term memory
-   Learns from previous mistakes
-   Improves across multiple tasks
-   More advanced architecture

### Example

After solving a coding problem, the agent stores the lesson "Always
handle edge cases." On future coding tasks, it recalls this memory
before generating a solution.

------------------------------------------------------------------------

## Reflection vs Reflexion

  Feature                    Reflection   Reflexion
  -------------------------- ------------ -----------
  Self-Critique              Yes          Yes
  Revises Current Answer     Yes          Yes
  Long-Term Memory           No           Yes
  Learns Across Tasks        No           Yes
  Stores Previous Mistakes   No           Yes
  Complexity                 Lower        Higher

------------------------------------------------------------------------

## When to Use Reflection

-   Essay refinement
-   Code review
-   Grammar correction
-   One-time question answering

------------------------------------------------------------------------

## When to Use Reflexion

-   Coding assistants
-   Research assistants
-   Personal AI assistants
-   Long-running autonomous agents
-   Personalized AI systems

------------------------------------------------------------------------

## Key Takeaways

-   Reflection improves only the current answer.
-   Reflexion combines self-reflection with memory.
-   Reflection is suitable for one-off tasks.
-   Reflexion is ideal for systems that should continuously improve over
    time.
