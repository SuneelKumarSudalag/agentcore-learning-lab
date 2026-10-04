# Lesson 1.2 — Tool vs Function vs MCP Tool

Status: IN PROGRESS

## Goal

Understand the difference between:
- a normal function
- an agent tool
- an MCP tool

## Official AWS anchors

1. Harness tools  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/harness-tools.html

AWS documents five Harness tool types plus built-in shell/filesystem tools:
- remote MCP
- AgentCore Gateway
- AgentCore Browser
- AgentCore Code Interpreter
- inline function

2. Use an AgentCore Gateway  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway-using.html

AWS explains that MCP provides a standardized way for agents to discover and invoke tools.

3. List Gateway tools  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway-using-mcp-list.html

4. Call a Gateway tool  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway-using-mcp-call.html

5. Gateway core concepts  
https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/gateway-core-concepts.html

## Simple mental model

### Function

A function is normal application code.

Example:

def get_weather(city):
    ...

Nothing about this ordinary Python function automatically tells an LLM:
- that it exists
- what it does
- what inputs it needs
- how to call it

### Tool

A tool is a capability exposed to an agent/model with a machine-readable contract.

Typical contract includes:
- name
- description
- input schema
- execution mechanism

The model can select the tool and produce arguments. The agent/orchestration layer executes it.

### MCP tool

An MCP tool is a tool exposed through the Model Context Protocol.

MCP standardizes operations such as:
- discovering/listing tools
- calling a specific tool
- passing structured arguments
- receiving structured results

In AgentCore Gateway, clients can discover tools and invoke them through MCP.

## Teaching equation

Function = executable code

Tool = function/capability + model-facing contract + orchestration integration

MCP Tool = tool exposed through a standardized MCP server/interface

This is a learning model, not an AWS API definition.

## Our project example

Ordinary Python function:

search_documents(query)

Agent tool:

name: search_documents
description: Search internal research documents
input: query string

MCP version:

Supervisor/RAG Agent
    ->
MCP client
    ->
AgentCore Gateway / MCP server
    ->
search_documents tool
    ->
retrieval backend

## Important AWS-specific point

Harness inline functions are declared as tools, but the implementation executes in client code rather than on the Harness VM. Harness pauses at the tool-use boundary and the caller sends the matching tool result back using the same runtime session.

Gateway can convert or aggregate Lambda functions, OpenAPI APIs, Smithy services, remote MCP servers, integrations, and connectors into a unified tool surface.

## Checkpoint

Be able to explain:
1. Why a Python function is not automatically an agent tool.
2. What metadata/schema makes a capability usable as a tool.
3. Why MCP is useful when many agents and tools need to interoperate.
