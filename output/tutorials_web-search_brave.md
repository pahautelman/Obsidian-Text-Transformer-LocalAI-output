# Brave

## Key Concepts
- Community contribution tutorial
- Customizing Open WebUI for specific use cases
- Contributing to tutorials
- Brave API integration
- Docker Compose setup for Brave search engine

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/web-search/brave](https://docs.openwebui.com/tutorials/web-search/brave)

### Overview
This tutorial is a community-contributed guide on customizing Open WebUI to integrate the Brave search engine. It is not officially supported by the Open WebUI team but serves as a demonstration for specific use cases.

### Contributing to Tutorials
If you are interested in contributing your own tutorials, refer to the [contributing tutorial](https://docs.openwebui.com/tutorials/web-search/brave) for guidelines and best practices.

### Brave API Integration

To integrate the Brave search engine with Open WebUI, follow these steps:

1. **Docker Compose Setup**
   - Add the following environment variables to your `docker-compose.yaml` file:
```yaml
services:
  open-webui:
    environment:
      ENABLE_RAG_WEB_SEARCH: True
      RAG_WEB_SEARCH_ENGINE: "brave"
      BRAVE_SEARCH_API_KEY: "YOUR_API_KEY"
      RAG_WEB_SEARCH_RESULT_COUNT: 3
      RAG_WEB_SEARCH_CONCURRENT_REQUESTS: 10
```
   - Replace `"YOUR_API_KEY"` with your actual Brave API key.
   - Adjust `RAG_WEB_SEARCH_RESULT_COUNT` and `RAG_WEB_SEARCH_CONCURRENT_REQUESTS` as needed to fit your requirements.

## Summary
This community-contributed tutorial demonstrates how to customize Open WebUI for integrating the Brave search engine. By following the Docker Compose setup instructions, users can enable web search functionalities tailored to their specific needs.

# Tags
#brave #websearch #tutorials #dockercompose #apiintegration