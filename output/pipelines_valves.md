# Valves

## Key Concepts
- Valves as input variables
- Initialization within the Pipeline class
- Reconfiguration options for valves
  - Environment variables with `os.getenv()`
  - Optional type for valves
- Error handling and logging

## Detailed Description

**Reference:** [https://docs.openwebui.com/pipelines/valves](https://docs.openwebui.com/pipelines/valves)

### Overview
Valves are input variables specific to each pipeline. They are defined as a subclass of the `Pipeline` class and initialized within the `__init__` method of this class.

### Initialization
When adding valves to your pipeline, ensure that they can be reconfigured by admins through the web UI. Here are some options for achieving this:

#### Using Environment Variables

You can use `os.getenv()` to set environment variables for the pipeline and provide default values if these variables are not set.

```python
self.valves = self.Valves(
    **{
        "LLAMAINDEX_OLLAMA_BASE_URL": os.getenv("LLAMAINDEX_OLLAMA_BASE_URL", "http://localhost:11434"),
        "LLAMAINDEX_MODEL_NAME": os.getenv("LLAMAINDEX_MODEL_NAME", "llama3"),
        "LLAMAINDEX_EMBEDDING_MODEL_NAME": os.getenv("LLAMAINDEX_EMBEDDING_MODEL_NAME", "nomic-embed-text")
    }
)
```

#### Using Optional Type

Set the valve to the `Optional` type, allowing the pipeline to load even if no value is set for the valve.

```python
class Pipeline:
    class Valves(BaseModel):
        target_user_roles: List[str] = ["user"]
        max_turns: Optional[int] = None
```

### Error Handling

If you do not provide a way to update valves in the web UI, you may encounter the following error in the Pipelines server log when trying to add a pipeline:

```
WARNING:root:No Pipeline class found in <pipeline name>
```

## Summary
Valves are crucial input variables for pipelines, initialized within the `Pipeline` class. They can be reconfigured using environment variables or set as optional types. Proper configuration ensures smooth operation and avoids errors during pipeline addition.

# Tags
#valves #pipelines #configuration #environment_variables #error_handling