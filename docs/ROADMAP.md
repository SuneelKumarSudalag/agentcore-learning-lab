# AgentCore Learning Roadmap

## Goal

Build and understand a production-style Enterprise Multi-Agent RAG Research Assistant while learning Amazon Bedrock AgentCore one component at a time from official AWS documentation.

## Learning method

For every component we will follow the same progression:

1. What problem are we solving?
2. What does the official AWS documentation say?
3. Beginner mental model.
4. Intermediate technical explanation.
5. Professional / production explanation.
6. Official AWS example or API.
7. Our practical implementation.
8. Run and test it.
9. Update the architecture.
10. Record decisions and references.
11. Update learning progress.
12. Explain what problem leads naturally to the next component.

## Components

1. AgentCore mental model
2. Development environment and prerequisites
3. Foundation models and first agent
4. AgentCore Harness
5. Harness execution environment and InvokeAgentRuntimeCommand
6. Custom container environments
7. AgentCore Runtime
8. RAG fundamentals
9. Internal RAG agent
10. MCP fundamentals
11. AgentCore Gateway
12. AgentCore Browser
13. Web Search connector
14. Code Interpreter
15. AgentCore Memory
16. AgentCore Identity
17. Multi-agent architecture
18. A2A protocol
19. Agent Registry
20. AgentCore Policy
21. AgentCore Observability
22. AgentCore Evaluations
23. Production hardening and end-to-end architecture

## Application we are building

Enterprise Multi-Agent RAG Research Assistant

Target shape:

```text
User
  |
  v
Supervisor / Router
  |--------------------|--------------------|
  v                    v                    v
Internal RAG Agent     Web Research Agent   Analysis Agent
  |                    |                    |
Retrieval layer        Browser / Search     Code Interpreter
  |
Knowledge store

          |
          v
Validation Agent
          |
          v
Cited final answer
```

AgentCore capabilities will be introduced only when the application reaches a problem that needs them.
