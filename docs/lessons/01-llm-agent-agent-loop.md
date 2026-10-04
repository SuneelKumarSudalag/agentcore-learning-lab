# Lesson 1.1 — LLM vs Agent vs Agent Loop

Status: IN PROGRESS

## Goal

Understand the difference between:
- an LLM
- an agent
- an agent loop

This is the foundation for understanding AgentCore Harness and Runtime.

## Official AWS anchors

1. AgentCore overview  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/

AWS describes AgentCore Harness as a managed agent loop.

2. Harness vs Runtime  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/harness-vs-runtime.html

AWS states:
- with Runtime, the orchestration loop is customer-owned code
- with Harness, AgentCore provides the orchestration loop
- a Harness agent is configured with a model, system prompt, tools, memory, and limits

3. Harness models and instructions  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/harness-models.html

The official examples show a harness configured with:
- a model
- a system prompt
- tools
- messages
- execution limits

## Simple mental model

### LLM

An LLM is the reasoning/generation engine.

Input:
"Find the weather in Hartford."

If the LLM has no live weather tool, it can only produce an answer from the information available in its context/model knowledge.

### Agent

An agent is an application that uses a model together with instructions and capabilities such as tools and state so that it can work toward a goal.

Mental model:

Agent = Model + Instructions + Tools + State/Context + Orchestration

This equation is a teaching model, not an AWS API definition.

### Agent loop

The agent loop repeatedly coordinates the model and tools.

Typical conceptual flow:

1. Receive the user's goal.
2. Send current context, instructions, and available tool definitions to the model.
3. Model decides either:
   - answer, or
   - request a tool.
4. If a tool is requested, execute the tool.
5. Put the tool result back into the context.
6. Call the model again.
7. Repeat until the model produces a final answer or an execution limit is reached.

## Example

User:
"Find AWS's definition of AgentCore and summarize it."

Possible loop:

Iteration 1:
Model decides it needs documentation.

Tool:
browser/search official AWS docs.

Tool result:
AWS documentation content.

Iteration 2:
Model reads retrieved content and produces the final explanation.

## Why this matters for AgentCore

AgentCore gives us two important choices:

### Harness

AWS owns/provides the agent orchestration loop.

We mainly configure:
- model
- system prompt
- tools
- memory
- limits

### Runtime

AWS hosts the agent securely, but our application/framework owns the agent orchestration loop.

This distinction will be studied in depth later.

## Beginner checkpoint

Explain:
- LLM = intelligence/generation engine
- Agent = application around the model that can pursue a goal and use capabilities
- Agent loop = repeated think/act/observe cycle coordinating the model and tools

## Important caveat

"Think → Act → Observe" is a useful teaching shorthand. It should not be interpreted as exposing a model's private chain-of-thought. In implementations we work with observable model outputs such as tool requests, tool results, messages, and final responses.
