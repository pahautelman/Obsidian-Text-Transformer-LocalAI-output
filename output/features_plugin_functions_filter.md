# Filter Function: Modify Inputs and Outputs

## Key Concepts
- Filter Functions in Open WebUI
- Inlet function (input pre-processing)
- Stream function (real-time output modification)
- Outlet function (output post-processing)
- Valves for configuration options
- Practical examples of filter usage

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/plugin/functions/filter](https://docs.openwebui.com/features/plugin/functions/filter)

### Overview
Filter Functions in Open WebUI are powerful tools designed to modify data before it reaches the Large Language Model (LLM) or after it is returned from the LLM. These functions enhance the clarity, context, and readability of both inputs and outputs.

### Key Components

#### 1️⃣ Valves Class
Valves serve as configuration options for filters, allowing users to adjust the filter's behavior dynamically.
```python
class Valves(BaseModel):
    OPTION_NAME: str = "Default Value"
```
**Example:**
A filter that converts responses into uppercase might include a valve like `TRANSFORM_UPPERCASE: bool = True/False`.

#### 2️⃣ Inlet Function
The inlet function pre-processes user inputs before they are sent to the LLM. This step ensures that the input is clean, contextual, and helpful for the AI model.
```python
def inlet(self, body: dict) -> dict:
    print(f"inlet called: {body}")
    return body
```
**Use Cases:**
- **Adding Context:** Automatically append crucial information to user inputs.
- **Formatting Data:** Transform input data into specific formats like JSON or Markdown.
- **Sanitizing Input:** Remove unwanted characters or sensitive information.
- **Streamlining User Input:** Inject clarifying instructions automatically.

#### 3️⃣ Stream Function
The stream function intercepts and modifies the model's responses in real-time as they are generated. This is useful for real-time modifications like filtering out sensitive information or formatting output for better readability.
```python
def stream(self, event: dict) -> dict:
    print(f"stream event: {event}")
    return event
```
**Use Cases:**
- **Real-Time Censorship:** Implement real-time censorship or cleanup.
- **Monitoring:** Log streamed data for debugging purposes.

#### 4️⃣ Outlet Function
The outlet function post-processes the AI's responses after they are generated, allowing for final adjustments before the output is sent to the user. This can help refine, log, or adapt the data for a cleaner user experience.
```python
def outlet(self, body: dict) -> None:
    print(f"outlet called: {body}")
```
**Use Cases:**
- **Logging:** Prefer logging over direct edits for debugging or analytics.
- **Sensitive Information:** Strip out sensitive information from API responses.

### Practical Examples

#### Example #1: Adding Context to User Inputs
Add instructions like "You're a software troubleshooting assistant" to every user query.
```python
class Filter:
    def inlet(self, body: dict, __user__: Optional[dict] = None) -> dict:
        context_message = {
            "role": "system",
            "content": "You're a software troubleshooting assistant."
        }
        body.setdefault("messages", []).insert(0, context_message)
        return body
```

#### Example #2: Highlighting Outputs for Easy Reading
Return outputs in Markdown or another formatted style using the outlet function.
```python
class Filter:
    def outlet(self, body: dict, __user__: Optional[dict] = None) -> dict:
        for message in body["messages"]:
            if message["role"] == "assistant":
                message["content"] = f"**{message['content']}**"
        return body
```

### FAQ

#### How Are Filters Different From Pipe Functions?
Filters modify data going to and coming from models but do not significantly interact with logic outside of these phases. Pipes, on the other hand, can integrate external APIs or transform backend operations.

#### Can I Do Heavy Post-Processing Inside Outlet?
While possible, it's not best practice. Filters are designed for lightweight changes or logging. For heavy modifications, consider using a Pipe Function instead.

## Summary
Filter Functions in Open WebUI allow users to modify inputs and outputs of the LLM, enhancing clarity, context, and readability. The inlet function pre-processes user inputs, the stream function modifies real-time outputs, and the outlet function post-processes AI responses. Valves provide configurable options for dynamic behavior.

# Tags
#filters #OpenWebUI #LLM #inlet #stream #outlet