# Retrieval Augmented Generation (RAG)

## Key Concepts
- RAG technology overview
- Local and remote document integration
- Web content retrieval
- Customization of RAG templates
- Embedding support for different models
- Citations in RAG feature
- Enhanced RAG pipeline
- YouTube video summarization
- Document parsing
- Google Drive integration

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/rag](https://docs.openwebui.com/features/rag)

### Overview of Retrieval Augmented Generation (RAG)
Retrieval Augmented Generation (RAG) is an advanced technology designed to enhance the conversational capabilities of chatbots by incorporating context from various sources. This includes local and remote documents, web content, and multimedia like YouTube videos.

### Local and Remote RAG Integration
To integrate local documents:
1. **Upload Documents:**
   - Upload via the Documents section in the Workspace area.
   - Access using the `#` symbol before a query.
2. **Retrieval Process:**
   - Click on the formatted URL above the chat box.
   - A document icon appears, indicating successful retrieval.

To integrate web content:
1. **Start Query with URL:**
   - Begin a prompt with `#`, followed by the target URL.
2. **Retrieval Process:**
   - Click on the formatted URL in the box that appears.
   - Open WebUI fetches and parses information from the URL.

### RAG Template Customization
Customize the RAG template via:
- Admin Panel > Settings > Documents menu

### RAG Embedding Support
Change the embedding model directly in:
- Admin Panel > Settings > Documents menu
Supports Ollama and OpenAI models for enhanced document processing.

### Citations in RAG Feature
The RAG feature allows users to track the context of documents fed to LLMs with added citations, ensuring transparency and accountability.

### Enhanced RAG Pipeline
The hybrid search sub-feature enhances RAG functionality via:
- BM25 for initial retrieval.
- CrossEncoder for re-ranking.
- Configurable relevance score thresholds for precise results.

### YouTube RAG Pipeline
Summarize YouTube videos directly from video URLs, enabling smooth interaction with video transcriptions and enriching conversation experiences.

### Document Parsing
Various parsers extract content from local and remote documents. For more details, see the `get_loader` function.

### Google Drive Integration
Integrate Google Drive by:
1. **Enable APIs:**
   - Google Picker API.
   - Google Drive API.
2. **Configure OAuth 2.0 Client:**
   - Set Authorized JavaScript origins and Authorized redirect URI to your Open-WebUI instance URL.
3. **Set Environment Variables:**
   - `GOOGLE_DRIVE_API_KEY`
   - `GOOGLE_DRIVE_CLIENT_ID`
   - `GOOGLE_REDIRECT_URI`

## Summary
Retrieval Augmented Generation (RAG) enhances chatbot conversations by integrating context from diverse sources, including documents and multimedia. It offers customization options for templates and embedding models, supports detailed document parsing, and integrates with Google Drive for seamless file access.

# Tags
#RAG #chatbots #documentintegration #webcontent #customization #embeddingmodels #citations #pipelineenhancement #YouTube #GoogleDrive