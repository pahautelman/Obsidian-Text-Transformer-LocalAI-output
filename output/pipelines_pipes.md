# Pipes

## Key Concepts
- Pipelines
- Pipes
- Retrieval Augmented Generation (RAG)
- Non-OpenAI LLM providers
- Function execution within web UI
- Pipe workflow
- External model designation

## Detailed Description

**Reference:** [https://docs.openwebui.com/pipelines/pipes](https://docs.openwebui.com/pipelines/pipes)

### Overview
Pipes are specialized functions designed to perform actions on LLM messages before they are returned to the user. These actions can include:

- **Retrieval Augmented Generation (RAG)**
- Sending requests to non-OpenAI LLM providers such as Anthropic, Azure OpenAI, or Google.
- Executing functions directly within your web UI.

### Hosting Options
Pipes can be hosted in two primary ways:
1. As a Function
2. On a Pipelines server

### Workflow
The general workflow for pipes is illustrated below:

[Image: Pipe Workflow]

### Integration with WebUI
When pipes are defined within your WebUI, they appear as new models with an "External" designation. This helps users easily identify and manage these specialized functions.

#### Examples of Pipe Models:
- **Database RAG Pipeline**
- **DOOM**

These examples can be visualized in the WebUI alongside self-hosted models:

[Image: Pipe Models in WebUI]

## Summary
Pipes are essential components within Pipelines that enable various actions on LLM messages before they reach the user. They support Retrieval Augmented Generation, integration with non-OpenAI providers, and direct function execution within the web UI.

# Tags
#pipes #pipelines #RAG #LLM #webUI