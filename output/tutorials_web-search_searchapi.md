# SearchApi

## Key Concepts
- Community contribution tutorial
- Customizing Open WebUI for specific use cases
- SearchApi API and supported SERP engines
- Setting up SearchApi in Open WebUI Admin panel
- Enabling web search functionality

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/web-search/searchapi](https://docs.openwebui.com/tutorials/web-search/searchapi)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI using SearchApi for specific use cases. It is not officially supported by the Open WebUI team but serves as a valuable guide.

### SearchApi API

SearchApi is a collection of real-time SERP APIs that support various search engines. The default engine is Google, but you can configure it to use other engines such as:

- Bing
- Baidu
- Google News
- Bing News
- Google Scholar
- Google Patents

### Setup Instructions

1. **Create/Log in to SearchApi Account**
   - Go to the [SearchApi website](https://searchapi.io/) and log on or create a new account.
   - Navigate to the Dashboard and copy your API key.

2. **Configure Open WebUI Admin Panel**
   - Open the Open WebUI Admin panel.
   - Click on the Settings tab, then select Web Search.
   - Enable Web search and set the Web Search Engine to `searchapi`.
   - Fill in the SearchApi API Key with the key copied from the SearchApi dashboard.
   - Optionally, enter the specific SearchApi engine name you want to query (e.g., google, bing, baidu).
   - Click Save.

> **Note:** The default search engine is set to Google. You can change it to any of the supported engines as needed.

### Enabling Web Search

To use web search functionality:
- Enable Web search in the prompt field using the plus (+) button.
- This allows you to perform searches using the configured SearchApi engines.

## Summary
This tutorial guides users through setting up and customizing Open WebUI with SearchApi, enabling real-time SERP searches from various engines. By following the steps outlined, users can enhance their search capabilities within Open WebUI.

# Tags
#searchapi #tutorials #websearch #openwebui #serp