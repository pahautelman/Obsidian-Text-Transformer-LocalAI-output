# Pipe Function: Create Custom "Agents/Models"

## Key Concepts
- Introduction to Pipes
- Pipe structure (Pipe class, Valves, __init__ method, pipe function)
- Creating multiple models with Pipes
- Example: OpenAI Proxy Pipe
- Using internal Open WebUI functions

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/plugin/functions/pipe](https://docs.openwebui.com/features/plugin/functions/pipe)

### Introduction to Pipes
Pipes in Open WebUI are customizable plugins that introduce new data pathways, allowing for the injection of custom logic and processing. Think of them as extensions that enhance the functionality of your models.

### Pipe Structure

#### The Pipe Class
The `Pipe` class is where you define your custom logic. It acts as a blueprint for your plugin, determining how it behaves within Open WebUI.

```python
from pydantic import BaseModel, Field

class Pipe:
    class Valves(BaseModel):
        MODEL_ID: str = Field(default="")

    def __init__(self):
        self.valves = self.Valves()

    def pipe(self, body: dict):
        # Logic goes here
        print(self.valves, body)
        return "Hello, World!"
```

#### Valves: Configuring Your Pipe
`Valves` is a nested class within `Pipe`, inheriting from `BaseModel`. It contains configuration options that persist across the use of your Pipe.

```python
class Valves(BaseModel):
    MODEL_ID: str = Field(default="")
```

#### The __init__ Method
The constructor method for the `Pipe` class. It initializes the Pipe's state and sets up any necessary components.

```python
def __init__(self):
    self.valves = self.Valves()
```

#### The pipe Function
The core function where your custom logic resides. It processes the input data using your custom logic and returns the result.

```python
def pipe(self, body: dict):
    # Logic goes here
    print(self.valves, body)
    return "Hello, World!"
```

### Creating Multiple Models with Pipes

To create multiple models within Open WebUI using a single Pipe, define a `pipes` function or variable inside your `Pipe` class. This setup allows your Pipe to represent multiple models.

```python
def pipes(self):
    return [
        {"id": "model_id_1", "name": "model_1"},
        {"id": "model_id_2", "name": "model_2"},
        {"id": "model_id_3", "name": "model_3"},
    ]
```

### Example: OpenAI Proxy Pipe

#### Valves Configuration
- `NAME_PREFIX`: Adds a prefix to the model names displayed in Open WebUI.
- `OPENAI_API_BASE_URL`: Specifies the base URL for the OpenAI API.
- `OPENAI_API_KEY`: Your OpenAI API key for authentication.

```python
class Valves(BaseModel):
    NAME_PREFIX: str = Field(default="OPENAI/", description="Prefix to be added before model names.")
    OPENAI_API_BASE_URL: str = Field(default="https://api.openai.com/v1", description="Base URL for accessing OpenAI API endpoints.")
    OPENAI_API_KEY: str = Field(default="", description="API key for authenticating requests to the OpenAI API.")
```

#### The pipes Function
Fetches available OpenAI models and makes them accessible in Open WebUI.

```python
def pipes(self):
    if self.valves.OPENAI_API_KEY:
        try:
            headers = {
                "Authorization": f"Bearer {self.valves.OPENAI_API_KEY}",
                "Content-Type": "application/json",
            }
            r = requests.get(f"{self.valves.OPENAI_API_BASE_URL}/models", headers=headers)
            models = r.json()
            return [
                {"id": model["id"], "name": f'{self.valves.NAME_PREFIX}{model.get("name", model["id"])}'}
                for model in models["data"]
                if "gpt" in model["id"]
            ]
        except Exception as e:
            return [{"id": "error", "name": "Error fetching models. Please check your API Key."}]
    else:
        return [{"id": "error", "name": "API Key not provided."}]
```

#### The pipe Function
Handles the request to the selected OpenAI model and returns the response.

```python
def pipe(self, body: dict, __user__: dict):
    headers = {
        "Authorization": f"Bearer {self.valves.OPENAI_API_KEY}",
        "Content-Type": "application/json",
    }
    model_id = body["model"][body["model"].find(".") + 1:]
    payload = {**body, "model": model_id}
    try:
        r = requests.post(
            url=f"{self.valves.OPENAI_API_BASE_URL}/chat/completions",
            json=payload,
            headers=headers,
            stream=True,
        )
        r.raise_for_status()
        if body.get("stream", False):
            return r.iter_lines()
        else:
            return r.json()
    except Exception as e:
        return f"Error: {e}"
```

### Extending the Proxy Pipe
Modify this proxy Pipe to support additional service providers like Anthropic, Perplexity, and more by adjusting the API endpoints, headers, and logic within the `pipes` and `pipe` functions.

### Using Internal Open WebUI Functions

Sometimes, you may want to leverage the internal functions of Open WebUI within your Pipe. You can import these functions directly from the `open_webui` package.

```python
from pydantic import BaseModel, Field
from fastapi import Request
from open_webui.models.users import Users
from open_webui.utils.chat import generate_chat_completion

class Pipe:
    def __init__(self):
        pass

    async def pipe(self, body: dict, __user__: dict, __request__: Request) -> str:
        user = Users.get_user_by_id(__user__["id"])
        body["model"] = "llama3.2:latest"
        return await generate_chat_completion(__request__, body, user)
```

### Important Notes
- **Function Signatures**: Refer to the latest Open WebUI codebase or documentation for the most accurate function signatures and parameters.
- **Best Practices**: Always handle exceptions and errors gracefully to ensure a smooth user experience.

## Summary

Pipes in Open WebUI allow you to create custom "agents/models" by defining your own logic and processing within the Pipe class. You can configure Pipes using Valves, create multiple models with the `pipes` function, and even integrate external APIs like OpenAI. By following best practices and consulting the latest documentation, you can extend Open WebUI's capabilities to suit your specific needs.

# Tags
#pipe #openwebui #custommodels #plugins #apiintegration