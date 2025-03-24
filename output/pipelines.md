# Pipelines: UI-Agnostic OpenAI API Plugin Framework

## Key Concepts
- Overview of Pipelines
- Use cases for Pipelines vs. Open WebUI Functions
- Benefits and features of Pipelines
  - Limitless possibilities
  - Seamless integration
  - Custom hooks
- Examples of achievable tasks with Pipelines
- How Pipelines work
- Quick start guide with Docker
- Installation and setup process
- Directory structure and examples
- Community involvement

## Detailed Description

**Reference:** [https://docs.openwebui.com/pipelines/](https://docs.openwebui.com/pipelines/)

### Overview
Pipelines is an Open WebUI initiative designed to bring modular, customizable workflows to any UI client supporting OpenAI API specifications. It allows users to extend functionalities, integrate unique logic, and create dynamic workflows with minimal code.

### When to Use Pipelines

- **For Computationally Heavy Tasks:** Offload tasks like running large models or complex logic from your main Open WebUI instance for better performance.
- **Custom Logic Integration:** Add custom Python libraries and logic, such as AI agents or home automation APIs.
- **Seamless Integration:** Compatible with any UI/client supporting OpenAI API specs (note: only pipe-type pipelines are supported; filter types require clients with Pipelines support).

### Benefits of Pipelines

#### Limitless Possibilities
Easily add custom logic and integrate Python libraries, from AI agents to home automation APIs.

#### Seamless Integration
Compatible with any UI/client supporting OpenAI API specs. (Only pipe-type pipelines are supported; filter types require clients with Pipelines support.)

#### Custom Hooks
Build and integrate custom pipelines tailored to your specific needs.

### Examples of Achievable Tasks

- **Function Calling Pipeline:** Handle function calls and enhance applications with custom logic.
- **Custom RAG Pipeline:** Implement sophisticated Retrieval-Augmented Generation pipelines.
- **Message Monitoring Using Langfuse:** Monitor and analyze message interactions in real-time using Langfuse.
- **Rate Limit Filter:** Control the flow of requests to prevent exceeding rate limits.
- **Real-Time Translation Filter with LibreTranslate:** Integrate real-time translations into LLM interactions.
- **Toxic Message Filter:** Detect and handle toxic messages effectively.

### How It Works

Integrating Pipelines with any OpenAI API-compatible UI client is straightforward:

1. Launch your Pipelines instance.
2. Set the OpenAI URL on your client to the Pipelines URL.
3. You're ready to leverage any Python library for your needs.

### Quick Start with Docker
For a streamlined setup using Docker, follow these steps:

1. **Run the Pipelines Container:**
   ```bash
   docker run -d -p 9099:9099 --add-host=host.docker.internal:host-gateway -v pipelines:/app/pipelines --name pipelines --restart always ghcr.io/open-webui/pipelines:main
   ```

2. **Connect to Open WebUI:**
   - Navigate to the Admin Panel > Settings > Connections section in Open WebUI.
   - Press the + button to add another connection.
   - Set the API URL to `http://localhost:9099` and the API key to `0p3n-w3bu!`.
   - Verify the connection; an icon labeled Pipelines will appear within the API Base URL field.

### Installation and Setup

1. **Ensure Python 3.11 is Installed:**
   - This is the only officially supported Python version.
2. **Clone the Pipelines Repository:**
   ```bash
   git clone https://github.com/open-webui/pipelines.git
   cd pipelines
   ```
3. **Install Required Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
4. **Start the Pipelines Server:**
   ```bash
   sh ./start.sh
   ```

### Directory Structure and Examples

The `/pipelines` directory is the core of your setup. Add new modules, customize existing ones, and manage your workflows here. All pipelines in this directory will be automatically loaded when the server launches.

You can change this directory from `/pipelines` to another location using the `PIPELINES_DIR` environment variable.

### Integration Examples

Find various integration examples in the [examples directory](https://github.com/open-webui/pipelines/blob/main/examples). These examples show how to integrate different functionalities, providing a foundation for building your own custom pipelines.

## Summary
Pipelines is a powerful framework for creating modular, customizable workflows within Open WebUI. It offers seamless integration with any UI supporting OpenAI API specs and allows for the addition of custom logic and Python libraries. With Pipelines, you can handle computationally heavy tasks, monitor messages, implement rate limiting, and more, all while enhancing your applications with dynamic workflows.

# Tags
#pipelines #openwebui #api #integration #customization #workflows