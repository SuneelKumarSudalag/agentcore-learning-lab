# Lesson 1.3 — Context vs State vs Session

Status: IN PROGRESS

## Goal

Understand the difference between:
- context
- state
- session

These concepts are related but not interchangeable.

## Official AWS anchors

1. Runtime isolated sessions  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-sessions.html

AWS states that Runtime sessions preserve contextual state across invocations, isolate each session in its own execution environment, and use a runtimeSessionId for session affinity.

2. Runtime architecture / microVM sessions  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/runtime-how-it-works.html

3. Harness Memory  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/harness-memory.html

AWS explains that when Harness memory is enabled, conversation state is persisted in AgentCore Memory, and later invocations with the same session ID load stored history.

4. AgentCore Memory types  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/memory-types.html

## Simple mental model

### Context
The information currently available to the model/agent when making a decision.

Examples:
- system instructions
- user messages
- recent conversation history
- retrieved RAG chunks
- tool results
- relevant long-term memories

Context is what the model can see for the current reasoning step.

### State
The changing working information that represents where the agent/workflow currently is.

Examples:
- current plan
- selected company
- tool outputs
- completed workflow steps
- intermediate calculations
- files created in the session
- retry counters

State can exist outside the model context and only relevant portions may be inserted into context.

### Session
The boundary/identity that groups related interactions and resources.

In AgentCore Runtime, runtimeSessionId identifies a session. Related invocations should reuse the same session ID. Runtime can route them to the same isolated execution environment and preserve ephemeral contextual state.

## Teaching analogy

Context = what is on the worker's desk right now.

State = all current work-in-progress information about the job.

Session = the private office/workroom assigned to one conversation/job.

Memory = the filing system used when information needs to survive beyond the temporary workroom.

## Important distinction

A Runtime session is not a durable database.

By default, microVM compute is ephemeral. AWS recommends:
- session storage for filesystem data that must survive stop/resume
- AgentCore Memory for structured conversational information that must survive the session lifecycle

## Our application example

Question 1:
"Analyze Acme's Q3 filing."

Session state might contain:
- company = Acme
- quarter = Q3
- retrieved filing path
- current workflow step = risk analysis

Model context for one call might contain:
- system prompt
- user's question
- top 5 retrieved chunks
- latest tool result

The runtimeSessionId groups the related invocations so they remain in the same isolated session.

Question 2:
"Now compare it with Q2."

Using the same session lets the application build on prior session context/state.

## Checkpoint

Be able to explain:
1. Context is what the model/agent currently has available to reason over.
2. State is the evolving working information for the workflow.
3. Session is the identity/boundary grouping related interactions and execution resources.
4. Session state is usually ephemeral; durable retention requires explicit storage such as AgentCore Memory.
