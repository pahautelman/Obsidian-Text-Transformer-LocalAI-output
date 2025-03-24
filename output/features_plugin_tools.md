# Tools

## Key Concepts
- Definition and purpose of tools
- Installation methods (manual download, URL import)
- Enabling and using tools in LLM models
- Custom toolkit creation
- Event emitters for dynamic interactions

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/plugin/tools/](https://docs.openwebui.com/features/plugin/tools/)

### What are Tools?
Tools are Python scripts provided to an LLM at the time of a request, enabling actions and providing additional context. They require function calling support from the LLM for reliable use.

### Use Cases
Tools enable various functionalities within chats:
- **Web Search:** Fetch real-time information.
- **Image Generation:** Create images based on user prompts.
- **External Voice Synthesis:** Integrate services like ElevenLabs for audio generation.

### Installation Methods

#### Manual Download and Import
1. Navigate to the community site: [https://openwebui.com/tools/](https://openwebui.com/tools/)
2. Click on the desired tool.
3. Click the blue “Get” button.
4. Select “Download as JSON export.”
5. Upload the tool into Open WebUI via Workspace => Tools => Import Tools.

#### URL Import
1. Navigate to the community site: [https://openwebui.com/tools/](https://openwebui.com/tools/)
2. Click on the desired tool.
3. Click the blue “Get” button.
4. Enter your Open WebUI instance IP address and click “Import to WebUI.”

> **Warning:** Only import tools from trusted sources to avoid security risks.

### Enabling Tools
1. Navigate to Workspace => Models.
2. Select the model for which you want to enable tools.
3. Click the pencil icon to edit settings.
4. Scroll down to the Tools section and check the desired tools.
5. Save the changes.

### Using Tools in Chat
- Once enabled, click the “+” icon during a chat session to use various tools.
- Note: Enabling a tool does not force its use; it provides the LLM with the option to call the tool.

### AutoTool Filter
The community site offers an AutoTool filter that allows LLMs to autoselect tools without manual enabling:
[https://openwebui.com/f/hub/autotool_filter/](https://openwebui.com/f/hub/autotool_filter/)

## Writing a Custom Toolkit

### Structure
A toolkit is defined in a single Python file with a top-level docstring containing metadata and a Tools class.

#### Example Docstring
```python
"""title: String Inverse
author: Your Name
author_url: https://website.com
git_url: https://github.com/username/string-reverse.git
description: This tool calculates the inverse of a string
required_open_webui_version: 0.4.0
requirements: langchain-openai, langgraph, ollama, langchain_ollamaversion: 0.4.0
license: MIT"""
```

#### Tools Class
The Tools class contains methods for tool functionalities, with optional subclasses Valves and UserValves.

```python
class Tools:
    def __init__(self):
        """Initialize the Tool."""
        self.valves = self.Valves()

class Valves(BaseModel):
    api_key: str = Field("", description="Your API key here")

    def reverse_string(self, string: str) -> str:
        """Reverses the input string.
        :param string: The string to reverse
        """
        if self.valves.api_key != "42":
            return "Wrong API key"
        return string[::-1]
```

### Type Hints and Valves
- **Type Hints:** Essential for generating JSON schemas sent to the model. Example: `queries_and_docs: list[tuple[str, int]]`.
- **Valves and UserValves:** Allow dynamic details like API keys or configuration options.

#### Optional Arguments
Tools can depend on various optional arguments:
- `__event_emitter__`: Emit events.
- `__event_call__`: User interactions.
- `__user__`: User information.
- `__metadata__`: Chat metadata.
- `__messages__`: Previous messages.
- `__files__`: Attached files.
- `__model__`: Model name.

### Event Emitters
Event emitters add dynamic content to the chat interface. Types include:
- **Status:** Add statuses to messages during processing.
- **Message:** Append messages, images, or web pages.
- **Citation:** Provide citations or references.

#### Example Status Emitter
```python
await __event_emitter__({
    "type": "status",
    "data": {
        "description": "Message that shows up in the chat",
        "done": False,
        "hidden": False
    }
})
```

#### Example Message Emitter
```python
await __event_emitter__({
    "type": "message",
    "data": {"content": "This message will be appended to the chat."}
})
```

### External Packages
Specify custom packages in the tool definition metadata. These will be installed using `pip install`.

## Summary
Tools enhance LLM interactions by enabling actions like web searches, image generation, and voice synthesis. They can be installed manually or via URL import, enabled for specific models, and used dynamically during chats. Custom toolkits can be created with Python scripts, and event emitters add dynamic content to the chat interface.

# Tags
#tools #LLM #python #customization #eventemitters