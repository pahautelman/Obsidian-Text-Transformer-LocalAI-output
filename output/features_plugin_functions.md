# Functions

## Key Concepts
- Extending Open WebUI capabilities with Functions
- Types of Functions (Pipe, Filter, Action)
- Installation and usage of Functions
- Customizing workflows and integrations
- Security considerations for installing Functions

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/plugin/functions/](https://docs.openwebui.com/features/plugin/functions/)

### What Are Functions?
Functions in Open WebUI are modular, built-in tools that extend the platform's capabilities. They allow you to:

- Add support for new AI model providers (e.g., Anthropic, Vertex AI).
- Customize message processing.
- Introduce custom buttons for enhanced usability.

Unlike external tools, Functions run within the Open WebUI environment, making them fast, modular, and free from external dependencies. Written in pure Python, they offer high customizability and can be used to create new AI-powered workflows or integrate with various services like Google Search or Home Assistant.

### Types of Functions

#### 1. Pipe Function – Create Custom "Agents/Models"
Pipe Functions allow you to create custom agents/models or integrations that appear as standalone models in the interface. They enable complex workflows, such as:

- Sending data to multiple models and combining their outputs.
- Integrating with non-AI systems like search APIs or Home Assistant.

**Use Case Example:**
Creating a Pipe Function to query Google Search directly from Open WebUI:
1. Takes your message as the search query.
2. Sends the query to Google Search’s API.
3. Processes the response and returns it within the WebUI.

#### 2. Filter Function – Modify Inputs and Outputs
Filter Functions act as "hooks" in the workflow, allowing you to tweak data before it is sent to the AI or after it comes back. They have two main parts:

- **Inlet:** Adjust the input sent to the model (e.g., adding instructions, keywords).
- **Outlet:** Modify the output received from the model (e.g., cleaning up responses).

**Use Case Example:**
Ensuring precise formatting in a project:
1. Transforming input into the required format.
2. Cleaning up the output before displaying it.

#### 3. Action Function – Add Custom Buttons
Action Functions add custom buttons to the chat interface, providing interactive shortcuts that trigger specific functionality directly from the chat. These buttons appear underneath individual chat messages.

**Use Case Example:**
Adding a "Summarize" button under every incoming message:
1. When clicked, it triggers a custom function to process the message and return a summary.

### How to Use Functions

#### 1. Install Functions
- **Via Interface:** Install Functions directly through the Open WebUI interface.
- **Manually:** Import them manually from trusted sources.

> **Warning:** Only install Functions from trusted sources to avoid security risks.

#### 2. Enable Functions
- **Pipe Functions:** Become available as standalone models in the interface.
- **Filter and Action Functions:** Need to be assigned to specific models or enabled globally for all models.

#### 3. Assign Filters or Actions to Models
- Navigate to `Workspace => Models` and assign your Filter or Action to the relevant model.
- Enable Functions globally by going to `Workspace => Functions`, selecting the "..." menu, and toggling the Global switch.

### Quick Summary

- **Pipes:** Standalone models for complex workflows.
- **Filters:** Modify inputs/outputs for smoother AI interactions.
- **Actions:** Add clickable buttons to individual chat messages.

### Why Use Functions?
Functions allow you to:

- **Extend:** Add new models or integrate with non-AI tools.
- **Optimize:** Tweak inputs and outputs to fit specific use cases.
- **Simplify:** Add buttons or shortcuts for an intuitive interface.

By leveraging Functions, you can customize workflows, integrate external data, and enhance the usability of Open WebUI.

### Final Notes
- Always install Functions from trusted sources.
- Understand the differences between Pipe, Filter, and Action Functions.
- Explore the official guides: [Pipe Functions Guide](https://docs.openwebui.com/features/plugin/functions/pipe), [Filter Functions Guide](https://docs.openwebui.com/features/plugin/functions/filter), [Action Functions Guide](https://docs.openwebui.com/features/plugin/functions/action).

## Summary
Functions in Open WebUI are powerful tools that extend the platform's capabilities by allowing custom integrations, workflows, and interface enhancements. They come in three types: Pipe, Filter, and Action, each serving specific purposes to optimize and simplify user interactions.

# Tags
#functions #openwebui #customization #integration #workflows