# Mojeek

## Key Concepts
- Community contribution tutorial
- Customizing Open WebUI for specific use cases
- Mojeek Search API setup
- Docker Compose environment variables

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/web-search/mojeek](https://docs.openwebui.com/tutorials/web-search/mojeek)

### Overview
This tutorial demonstrates how to customize Open WebUI for integrating the Mojeek Search API. It is a community contribution and not officially supported by the Open WebUI team.

### Setup Instructions

#### Obtaining an API Key
1. **Visit Mojeek Search API Page**
   - Go to the [Mojeek Search API page](https://docs.openwebui.com/tutorials/web-search/mojeek) to obtain your API key.
2. **Open Open WebUI Admin Panel**
   - Navigate to the Settings tab and then click on Web Search.

#### Configuring Web Search
1. **Enable Web Search**
   - Enable web search functionality.
2. **Set Web Search Engine**
   - Set the Web Search Engine to `mojeek`.
3. **Enter API Key**
   - Fill in the Mojeek Search API Key field with your obtained API key.
4. **Save Settings**
   - Click Save to apply the changes.

### Docker Compose Setup
To integrate Mojeek Search API using Docker Compose, add the following environment variables to your `docker-compose.yaml` file:

```yaml
services:
  open-webui:
    environment:
      ENABLE_RAG_WEB_SEARCH: True
      RAG_WEB_SEARCH_ENGINE: "mojeek"
      BRAVE_SEARCH_API_KEY: "YOUR_MOJEEK_API_KEY"
      RAG_WEB_SEARCH_RESULT_COUNT: 3
      RAG_WEB_SEARCH_CONCURRENT_REQUESTS: 10
```

### Contributing
If you want to contribute your own tutorials or customizations, check out the contributing tutorial for guidelines on how to get involved.

## Summary

This tutorial guides users through integrating the Mojeek Search API with Open WebUI. It involves obtaining an API key, configuring settings in the admin panel, and setting up Docker Compose environment variables. The tutorial is a community contribution aimed at demonstrating customization for specific use cases.

# Tags
#mojeek #websearch #tutorial #customization #docker