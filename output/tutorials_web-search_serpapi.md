# SerpApi

## Key Concepts
- Community contribution tutorial
- Customizing Open WebUI for specific use cases
- SerpApi API overview
- Supported search engines (google, bing, baidu, etc.)
- Setup instructions for integrating SerpApi with Open WebUI
- Enabling web search in the prompt field

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/web-search/serpapi](https://docs.openwebui.com/tutorials/web-search/serpapi)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI using SerpApi for web search functionalities. It is not officially supported by the Open WebUI team but serves as a valuable guide for specific use cases.

### SerpApi API

SerpApi allows you to scrape Google and other search engines through a fast, easy-to-use API. Supported search engines include:

- **google**
- **bing**
- **baidu**
- **google_news**
- **google_scholar**
- **google_patents**

### Setup Instructions
Follow these steps to integrate SerpApi with Open WebUI:

1. **Create/Log in to SerpApi Account:**
   - Go to the [SerpApi website](https://serpapi.com/) and log in or create a new account.
   - Navigate to the Dashboard and copy your API key.

2. **Configure Open WebUI Admin Panel:**
   - Open the Open WebUI Admin panel.
   - Click on the Settings tab, then select Web Search.
   - Enable Web search and set the Web Search Engine to `serpapi`.
   - Enter the SerpApi API Key you copied earlier.
   - [Optional] Specify the SerpApi engine name (e.g., google, bing, baidu) if you want to query a specific engine. The default is set to google.

3. **Save Settings:**
   - Click Save to apply your changes.

> **Note:** Ensure that Web search is enabled in the prompt field to use SerpApi engines for web searches.

### Visual Aids
The setup process can be visualized with images such as:
- *[Image: Open WebUI Admin panel]*
- *[Image: enable Web search]*

## Summary
This tutorial guides users through integrating SerpApi with Open WebUI, enabling web search functionalities using various supported engines. By following the setup instructions and enabling web search in the prompt field, users can customize their Open WebUI experience for specific use cases.

# Tags
#serpapi #websearch #tutorial #openwebui #customization