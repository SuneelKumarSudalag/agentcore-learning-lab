# Architecture

This file evolves as we build the application. We keep older stages conceptually so we can see how the system grows.

## Stage 0 — Before learning starts

No implementation yet.

```text
User
  |
  v
[Agent application — not built yet]
```

## Target architecture

This is a direction, not something we will build all at once.

```text
                         USER
                           |
                     Authentication
                           |
                    AgentCore Identity
                           |
                           v
                  Supervisor Agent
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
    Internal RAG       Web Research      Analysis
       Agent               Agent           Agent
          |                |               |
      Gateway          Browser/Search  Code Interpreter
          |
        Policy
          |
   Retrieval capability
          |
    Knowledge store

       <---- AgentCore Memory ---->

Agents / tools discoverable through Registry where appropriate.
Agent communication may use A2A where appropriate.
Runtime hosts code-based agents.
Harness is learned separately as the managed agent-loop path.
Observability traces the system.
Evaluations measure agent quality.
```

## Architectural rule

AgentCore is not the vector database. Retrieval remains a separate capability that agents invoke. AgentCore operates, secures, connects, hosts, observes, and evaluates agentic workloads.
