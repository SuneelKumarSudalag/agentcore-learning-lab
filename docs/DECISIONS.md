# Architecture Decisions

This file records important decisions so we remember not just what we built, but why.

## D-001 — Use one evolving application
We will learn AgentCore by incrementally building one Enterprise Multi-Agent RAG Research Assistant.

Why:
- keeps learning practical
- shows how components connect
- prevents isolated examples from becoming disconnected knowledge

## D-002 — Keep RAG retrieval separate from AgentCore
AgentCore will host, operate, secure, connect, and observe agents. Retrieval will be implemented as a separate knowledge/retrieval capability that agents call.

Why:
- AgentCore is not itself a vector database
- keeps architecture accurate
- makes component responsibilities clearer

## D-003 — Official AWS docs are the source of truth
Every AgentCore concept and code path should be tied back to current AWS documentation when available.

Why:
- reduce hallucination risk
- make examples independently verifiable
- help navigate official docs confidently

## D-004 — Learn one component at a time
Do not jump ahead merely because a later feature sounds interesting.

Each component should cover:
1. what problem it solves
2. what AWS says
3. beginner mental model
4. intermediate technical model
5. professional/production model
6. code
7. request flow
8. testing
9. architecture update
10. next problem that motivates the next component
