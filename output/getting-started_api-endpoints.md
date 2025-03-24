# API Endpoints

## Key Concepts
- Authentication (Bearer Token)
- Retrieving models
- Chat completions
- Retrieval Augmented Generation (RAG)
  - Uploading files
  - Adding files to knowledge collections
  - Using files and collections in chat completions
- Advantages of Open WebUI

## Detailed Description

**Reference:** [https://docs.openwebui.com/getting-started/api-endpoints](https://docs.openwebui.com/getting-started/api-endpoints)

### Authentication
To securely access the API, use Bearer Token authentication. Obtain your API key from **Settings > Account** in Open WebUI or use a JWT (JSON Web Token).

### Notable API Endpoints

#### Retrieve All Models
- **Endpoint:** `GET /api/models`
- **Description:** Fetches all models created or added via Open WebUI.
- **Example Request:**
  ```bash
  curl -H "Authorization: Bearer YOUR_API_KEY" http://localhost:3000/api/models
  ```

#### Chat Completions
- **Endpoint:** `POST /api/chat/completions`
- **Description:** Serves as an OpenAI API compatible chat completion endpoint for models on Open WebUI, including Ollama models, OpenAI models, and Open WebUI Function models.
- **Curl Example:**
  ```bash
  curl -X POST http://localhost:3000/api/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "model": "llama3.1", "messages": [ { "role": "user", "content": "Why is the sky blue?" } ] }'
  ```
- **Python Example:**
  ```python
  import requests

  def chat_with_model(token):
      url = 'http://localhost:3000/api/chat/completions'
      headers = {
          'Authorization': f'Bearer {token}',
          'Content-Type': 'application/json'
      }
      data = {
          "model": "granite3.1-dense:8b",
          "messages": [
              {"role": "user", "content": "Why is the sky blue?"}
          ]
      }
      response = requests.post(url, headers=headers, json=data)
      return response.json()
  ```

### Retrieval Augmented Generation (RAG)

#### Uploading Files
- **Endpoint:** `POST /api/v1/files/`
- **Description:** Upload files to utilize external data in RAG responses.
- **Curl Example:**
  ```bash
  curl -X POST -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Accept: application/json" \
  -F "file=@/path/to/your/file" http://localhost:3000/api/v1/files/
  ```
- **Python Example:**
  ```python
  import requests

  def upload_file(token, file_path):
      url = 'http://localhost:3000/api/v1/files/'
      headers = {
          'Authorization': f'Bearer {token}',
          'Accept': 'application/json'
      }
      files = {'file': open(file_path, 'rb')}
      response = requests.post(url, headers=headers, files=files)
      return response.json()
  ```

#### Adding Files to Knowledge Collections
- **Endpoint:** `POST /api/v1/knowledge/{id}/file/add`
- **Description:** Group uploaded files into a knowledge collection or reference them individually in chats.
- **Curl Example:**
  ```bash
  curl -X POST http://localhost:3000/api/v1/knowledge/{knowledge_id}/file/add \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"file_id": "your-file-id-here"}'
  ```
- **Python Example:**
  ```python
  import requests

  def add_file_to_knowledge(token, knowledge_id, file_id):
      url = f'http://localhost:3000/api/v1/knowledge/{knowledge_id}/file/add'
      headers = {
          'Authorization': f'Bearer {token}',
          'Content-Type': 'application/json'
      }
      data = {'file_id': file_id}
      response = requests.post(url, headers=headers, json=data)
      return response.json()
  ```

#### Using Files and Collections in Chat Completions

##### Using an Individual File
- **Endpoint:** `POST /api/chat/completions`
- **Description:** Focus the chat model's response on the content of a specific file.
- **Curl Example:**
  ```bash
  curl -X POST http://localhost:3000/api/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "model": "gpt-4-turbo", "messages": [ {"role": "user", "content": "Explain the concepts in this document."} ], "files": [ {"type": "file", "id": "your-file-id-here"} ] }'
  ```
- **Python Example:**
  ```python
  import requests

  def chat_with_file(token, model, query, file_id):
      url = 'http://localhost:3000/api/chat/completions'
      headers = {
          'Authorization': f'Bearer {token}',
          'Content-Type': 'application/json'
      }
      payload = {
          'model': model,
          'messages': [{'role': 'user', 'content': query}],
          'files': [{'type': 'file', 'id': file_id}]
      }
      response = requests.post(url, headers=headers, json=payload)
      return response.json()
  ```

##### Using a Knowledge Collection
- **Endpoint:** `POST /api/chat/completions`
- **Description:** Enhance the response when the inquiry may benefit from a broader context or multiple documents.
- **Curl Example:**
  ```bash
  curl -X POST http://localhost:3000/api/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "model": "gpt-4-turbo", "messages": [ {"role": "user", "content": "Provide insights on the historical perspectives covered in the collection."} ], "files": [ {"type": "collection", "id": "your-collection-id-here"} ] }'
  ```
- **Python Example:**
  ```python
  import requests

  def chat_with_collection(token, model, query, collection_id):
      url = 'http://localhost:3000/api/chat/completions'
      headers = {
          'Authorization': f'Bearer {token}',
          'Content-Type': 'application/json'
      }
      payload = {
          'model': model,
          'messages': [{'role': 'user', 'content': query}],
          'files': [{'type': 'collection', 'id': collection_id}]
      }
      response = requests.post(url, headers=headers, json=payload)
      return response.json()
  ```

### Advantages of Using Open WebUI as a Unified LLM Provider
- **Unified Interface:** Simplify interactions with different LLMs through a single platform.
- **Ease of Implementation:** Quick start integration with comprehensive documentation and community support.

### Swagger Documentation Links
To access the Swagger documentation for any of these services, set the `ENV` environment variable to `dev`. Without this configuration, the documentation will not be available. Access detailed API documentation at `/docs`.

## Summary
This guide provides essential information on how to interact with Open WebUI's API endpoints effectively. It covers authentication methods, key endpoints for retrieving models and chat completions, and advanced features like Retrieval Augmented Generation (RAG) for enhanced responses using external data.

# Tags
#api #endpoints #authentication #chatcompletions #rag