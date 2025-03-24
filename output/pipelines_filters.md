# Filters

## Key Concepts
- Pipelines
- Filters
- Incoming and outgoing messages
- Filter actions (monitoring, modification, blocking, translating, rate limiting)
- Filter workflow (inlet, processing, outlet)

## Detailed Description

**Reference:** [https://docs.openwebui.com/pipelines/filters](https://docs.openwebui.com/pipelines/filters)

### Overview
The document explains the role and functionality of **Filters** within **Pipelines**. Filters are essential components used to perform specific actions on both incoming user messages and outgoing assistant (LLM) messages.

### Functionality
Filters can execute a range of actions, including:
- **Monitoring:** Sending messages to platforms like Langfuse or DataDog.
- **Modification:** Altering message content.
- **Blocking:** Preventing toxic messages.
- **Translation:** Converting messages to other languages.
- **Rate Limiting:** Restricting message frequency from certain users.

### Workflow
The filter workflow is divided into three main stages:
1. **Inlet Processing:**
   - Incoming user messages are passed to the filter.
   - Filters perform the desired pre-processing actions.
2. **LLM Processing:**
   - After filtering, the chat completion request is sent to the LLM model.
3. **Outlet Processing:**
   - Outgoing LLM messages undergo post-processing by the filter before reaching the user.

> **Note:** Filters can be executed either as a Function or on a Pipelines server, providing flexibility in deployment and execution.

### Visual Representation
The workflow is often illustrated with a diagram labeled as *[Image: Filter Workflow]* to help users visualize the process from message intake (inlet) to message delivery (outlet).

## Summary
Filters within Pipelines are used to manage and manipulate message flows between users and LLM models. They provide critical functionalities such as monitoring, modifying, and securing communication, ensuring that messages are processed efficiently and safely throughout the pipeline.

# Tags
#filters #pipelines #LLM #messaging #workflow