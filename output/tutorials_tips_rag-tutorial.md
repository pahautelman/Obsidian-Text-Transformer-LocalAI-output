# Tutorial: Configuring RAG with Open WebUI Documentation

## Key Concepts
- Retrieval-Augmented Generation (RAG)
- Open WebUI Documentation
- Knowledge base setup
- Custom model configuration
- Querying the knowledge base

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/tips/rag-tutorial](https://docs.openwebui.com/tutorials/tips/rag-tutorial)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI for specific use cases using Retrieval-Augmented Generation (RAG). RAG combines Large Language Models (LLMs) with retrieved knowledge from external sources, enhancing response quality and accuracy.

### What is RAG?
Retrieval-Augmented Generation (RAG) enhances LLM responses by retrieving relevant data from uploaded documents or knowledge bases. This tutorial focuses on using the latest Open WebUI Documentation as a knowledge base for this setup.

### Setup

#### Step-by-Step Setup: Open WebUI Documentation as Knowledge Base
1. **Download the Documentation**
   - Download the latest documentation from [https://github.com/open-webui/docs/archive/refs/heads/main.zip](https://github.com/open-webui/docs/archive/refs/heads/main.zip).

2. **Extract the Files**
   - Extract the `main.zip` file to access all documentation files.

3. **Locate the Markdown Files**
   - In the extracted folder, find all files with `.md` and `.mdx` extensions (use search for `*.md*`).

4. **Create a Knowledge Base**
   - Navigate to Workspace > Knowledge > + Create a Knowledge Base.
   - Name it: Open WebUI Documentation
   - Purpose: Assistance
   - Click Create Knowledge.

5. **Upload the Files**
   - Drag and drop the `.md` and `.mdx` files from the extracted folder into the Open WebUI Documentation knowledge base.

### Create and Configure the Model

#### Create a Custom Model with the Knowledge Base
1. **Navigate to Models**
   - Go to Workspace > Models > + Add New Model.

2. **Configure the Model**
   - Name: Open WebUI
   - Base Model: Select the appropriate Llama or other available model.
   - Knowledge Source: Select Open WebUI Documentation from the dropdown.
   - Save the Model.

### Examples and Usage

#### Query the Open WebUI Documentation Model
1. **Start a New Chat**
   - Navigate to New Chat and select the Open WebUI model.

2. **Example Queries**
   - User: "How do I configure environment variables?"
     - System: "Refer to Section 3.2: Use the `.env` file to manage configurations."
   - User: "How do I update Open WebUI using Docker?"
     - System: "Refer to `docker/updating.md`: Use `docker pull` and restart the container."

With the RAG-enabled model, the system retrieves the most relevant sections from the documentation to answer your query.

### Next Steps
- **Add More Knowledge**
  - Continue expanding your knowledge base by adding more documents.
  - With this setup, you can effectively use the Open WebUI Documentation to assist users by retrieving relevant information for their queries. Enjoy building and querying your custom knowledge-enhanced models!

## Summary
This tutorial guides users through setting up Retrieval-Augmented Generation (RAG) with Open WebUI using the latest documentation as a knowledge base. It covers downloading, extracting, and uploading documentation files, creating a custom model, and querying the knowledge base for enhanced assistance.

# Tags
#tutorial #RAG #OpenWebUI #documentation #knowledgebase