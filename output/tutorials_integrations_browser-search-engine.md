# Browser Search Engine Integration

## Key Concepts
- Community contribution tutorial
- Integrating Open WebUI with browsers (Chrome, Firefox)
- Setting up WEBUI_URL environment variable
- Adding custom search engine in browser settings
- Using specific models for searches
- Troubleshooting integration issues

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/browser-search-engine](https://docs.openwebui.com/tutorials/integrations/browser-search-engine)

### Overview
This tutorial, contributed by the community, demonstrates how to integrate Open WebUI as a custom search engine in your web browser. It is not officially supported but serves as a practical guide for customizing Open WebUI.

### Prerequisites

Before starting, ensure you have:
- Chrome or another supported browser installed.
- The WEBUI_URL environment variable set correctly (via Docker or .env file).

### Setting Up Open WebUI as a Search Engine

#### Step 1: Set the WEBUI_URL Environment Variable
The WEBUI_URL environment variable directs your browser to the correct Open WebUI instance.

##### Using Docker Environment Variables
If running Open WebUI with Docker, set the environment variable in your docker run command:

```bash
docker run -d \
-p 3000:8080 \
--add-host=host.docker.internal:host-gateway \
-v open-webui:/app/backend/data \
--name open-webui \
--restart always \
-e WEBUI_URL="https://<your-open-webui-url>" \
ghcr.io/open-webui/open-webui:main
```

##### Using .env File
Alternatively, add the variable to your .env file:

```plaintext
WEBUI_URL=https://<your-open-webui-url>
```

#### Step 2: Add Open WebUI as a Custom Search Engine

##### For Chrome
1. Navigate to **Settings** > **Search engine** > **Manage search engines**.
2. Click **Add** to create a new search engine.
3. Fill in the details:
   - **Search engine:** Open WebUI
   - **Search Keyword:** webui (or your preferred keyword)
   - **URL with %s in place of query:** `https://<your-open-webui-url>/?q=%s`
4. Click **Add** to save.

##### For Firefox
1. Go to Open WebUI in Firefox.
2. Expand the address bar and click the plus icon in a green circle.
3. Alternatively, right-click on the address bar and select **"Add Open WebUI"** from the context menu.

### Optional: Using Specific Models

To use a specific model for your search, modify the URL format to include the model ID:

```plaintext
https://<your-open-webui-url>/?models=<model_id>&q=%s
```

**Note:** The model ID must be URL-encoded. For example, `my model` becomes `my%20model`.

### Example Usage

Once set up, perform searches directly from the address bar by typing your keyword followed by your query:

```plaintext
webui your search query
```

This command redirects you to the Open WebUI interface with your search results.

### Troubleshooting

If issues arise:
- Ensure WEBUI_URL is correctly configured.
- Verify the search engine URL format in browser settings.
- Confirm active internet connection and smooth operation of the Open WebUI service.

## Summary
This tutorial guides users through integrating Open WebUI as a custom search engine in browsers like Chrome and Firefox. It covers setting up environment variables, adding the search engine to browser settings, using specific models for searches, and troubleshooting common issues.

# Tags
#browser #searchengine #integration #tutorial #openwebui