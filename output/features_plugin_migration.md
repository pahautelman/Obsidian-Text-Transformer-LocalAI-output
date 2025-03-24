# Migration Guide: Open WebUI 0.4 to 0.5

## Key Concepts
- Architecture changes (sub-app to single FastAPI app)
- Unified API endpoint
- Updated function signatures
- Import path updates
- Migration steps and examples

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/plugin/migration/](https://docs.openwebui.com/features/plugin/migration/)

### Overview
This guide walks you through the key changes from Open WebUI 0.4 to 0.5, providing a roadmap for upgrading your Functions and ensuring a smooth transition.

### Architecture Changes

#### Old Architecture
- **Sub-app Structure:** Each app (e.g., ollama, openai) was a separate FastAPI application.
- **Issues:** Fragmentation and extra complexity in managing apps.

#### New Architecture
- **Single FastAPI App with Multiple Routers:**
  - Better organization.
  - Centralized flow.
  - Reduced redundancy.

### Key Changes

1. **Apps to Routers**
   - Previous: `open_webui.apps`
   - Now: `open_webui.routers`

2. **Main App Structure Simplified**
   - Old: `open_webui.apps.webui`
   - New: `open_webui.main` (central entry point)

3. **Unified API Endpoint**
   - Introduced `chat_completion` in `open_webui.main`.
   - Replaces separate functions for models like ollama and openai.
   - Direct successor: `generate_chat_completion` from `open_webui.utils.chat`.

### Example Code Snippets

#### Full API Flow with Parsing
```python
from open_webui.main import chat_completion
```

#### Lightweight, Direct POST Request
```python
from open_webui.utils.chat import generate_chat_completion
```

### Updated Function Signatures

- **New Format:** Requires a request object.
- **Example:**
  ```python
  class Pipe:
      def __init__(self):
          pass

      async def pipe(self, body: dict, __user__: dict, __request__: Request) -> str:
          # Write your function here
  ```

### Why These Changes?

1. Simplify the codebase for easier extension and maintenance.
2. Unify APIs for a streamlined developer experience.
3. Enhance performance by consolidating redundant elements.

### Step-by-Step Migration Guide

#### 1. Shifting from Apps to Routers

- **Quick Changes:**
  - `open_webui.apps.ollama` → `open_webui.routers.ollama`
  - `open_webui.apps.openai` → `open_webui.routers.openai`
  - `open_webui.apps.audio` → `open_webui.routers.audio`
  - `open_webui.apps.retrieval` → `open_webui.routers.retrieval`
  - `open_webui.apps.webui` → `open_webui.main`

#### 2. Updating Import Statements

- **Before:**
  ```python
  from open_webui.apps.ollama import main as ollama
  from open_webui.apps.openai import main as openai
  ```

- **After:**
  ```python
  # Separate router imports
  from open_webui.routers.ollama import generate_chat_completion
  from open_webui.routers.openai import generate_chat_completion

  # Or use the unified endpoint
  from open_webui.main import chat_completion
  ```

#### 3. Adapting to Updated Function Signatures

- **Direct Successor:**
  ```python
  generate_chat_completion(request: Request, form_data: dict, user: UserModel)
  ```

- **Unified Option:**
  ```python
  chat_completion(request: Request, form_data: dict, user: UserModel)
  ```

### How to Refactor Your Custom Function

#### Before (0.4):
```python
from pydantic import BaseModel
from open_webui.apps.ollama import generate_chat_completion

class User(BaseModel):
    id: str
    email: str
    name: str
    role: str

class Pipe:
    def __init__(self):
        pass

    async def pipe(self, body: dict, __user__: dict) -> str:
        user = User(**__user__)
        body["model"] = "llama3.2:latest"
        return await ollama.generate_chat_completion(body, user)
```

#### After (0.5):
```python
from pydantic import BaseModel
from fastapi import Request
from open_webui.utils.chat import generate_chat_completion

class User(BaseModel):
    id: str
    email: str
    name: str
    role: str

class Pipe:
    def __init__(self):
        pass

    async def pipe(self, body: dict, __user__: dict, __request__: Request) -> str:
        user = User(**__user__)
        body["model"] = "llama3.2:latest"
        return await generate_chat_completion(__request__, body, user)
```

### Recap: Key Concepts in Simple Terms

- **Apps to Routers:** Update all imports from `open_webui.apps` to `open_webui.routers`.
- **Unified Endpoint:** Use `open_webui.main.chat_completion` for simplicity if both ollama and openai are involved.
- **Adapt Function Signatures:** Ensure your functions pass the required request object.

## Summary
This migration guide provides a comprehensive roadmap for upgrading from Open WebUI 0.4 to 0.5, focusing on architecture changes, unified API endpoints, updated function signatures, and import path updates. By following these steps, you can ensure a smooth transition and leverage the latest features in version 0.5.

# Tags
#migration #OpenWebUI #architecture #API #functionsignatures