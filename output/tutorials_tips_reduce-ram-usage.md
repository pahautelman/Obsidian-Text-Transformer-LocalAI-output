# Reduce RAM Usage

## Key Concepts
- RAM optimization in constrained environments
- Environment variables for model selection
- Memory consumption by ML models
- Speech-to-text and RAG embedding engines
- Image generation engine
- Docker container stats

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/tips/reduce-ram-usage](https://docs.openwebui.com/tutorials/tips/reduce-ram-usage)

### RAM Optimization in Constrained Environments
Deploying this image in a RAM-constrained environment requires optimizing memory usage. Here are steps to reduce idle memory consumption:

1. **Set Environment Variables**
   - Use the following environment variables or configure them via the UI for an existing deployment:
     ```plaintext
     RAG_EMBEDDING_ENGINE: ollama
     AUDIO_STT_ENGINE: openai
     ```

### Memory Consumption by ML Models

Much of the memory consumption is due to loaded machine learning (ML) models. Even when using external language models like OpenAI or unbundled Ollama, several models may still be loaded for additional purposes.

#### Default Loaded Models (as of v0.3.10)
- **Speech-to-text:** Uses Whisper by default.
- **RAG embedding engine:** Uses a local SentenceTransformers model by default.
- **Image generation engine:** Disabled by default.

### Optimizing Model Usage

To reduce memory usage, you can change the models in the admin panel or set environment variables for a fresh Docker deployment:

1. **Admin Panel Configuration**
   - **RAG Embedding Engine:**
     - Navigate to RAG: Documents category.
     - Set it to Ollama or OpenAI.
   - **Speech-to-text:**
     - Go to Audio section.
     - Work with OpenAI or WebAPI.

2. **Environment Variables for Docker Deployment**
   - Use the following environment variables:
     ```plaintext
     RAG_EMBEDDING_ENGINE: ollama
     AUDIO_STT_ENGINE: openai
     ```
   - Note: These environment variables have no effect if a `config.json` already exists.

### Example Optimization

On a Raspberry Pi 4 (arm64) with version v0.3.10, these optimizations reduced idle memory consumption from >1GB to ~200MB, as observed with Docker container stats:

```plaintext
docker container stats
```

## Summary
To reduce RAM usage in constrained environments, configure the RAG embedding engine and speech-to-text models appropriately. This can significantly lower memory consumption, making deployment more efficient on devices like the Raspberry Pi 4.

# Tags
#RAM #optimization #Docker #MLmodels #RaspberryPi