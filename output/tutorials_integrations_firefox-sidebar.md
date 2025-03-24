# Firefox AI Chatbot Sidebar

## Key Concepts
- Community contribution tutorial
- Prerequisites for integration (Open WebUI instance URL, Firefox browser)
- Enabling AI Chatbot in Firefox settings
- Configuring about:config settings
- Adding custom prompts and provider URLs
- URL parameters for Open WebUI customization
- Additional about:config settings
- Accessing the AI chatbot sidebar

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/firefox-sidebar](https://docs.openwebui.com/tutorials/integrations/firefox-sidebar)

### Overview
This tutorial, contributed by the community, demonstrates how to integrate Open WebUI as an AI chatbot browser assistant in Mozilla Firefox. It is not officially supported but serves as a valuable guide for customizing Open WebUI.

### Prerequisites

Before proceeding with the integration, ensure you have:

- **Open WebUI Instance URL:** This can be either local or domain-based.
- **Firefox Browser Installed:** Ensure that your browser is up to date.

### Enabling AI Chatbot in Firefox
To enable the AI chatbot feature in Firefox, follow these steps:

1. Click on the hamburger button (three horizontal lines) at the top right corner of the browser.
2. Open Firefox settings.
3. Navigate to the **Firefox Labs** section.
4. Toggle on the **AI Chatbot** option.

Alternatively, you can enable it through the `about:config` page:

1. Type `about:config` in the Firefox address bar and accept the risk.
2. Search for `browser.ml.chat.enabled` and set it to true if not already enabled.
3. Search for `browser.ml.chat.hideLocalhost` and set it to false.

### Configuring about:config Settings

To further customize your AI chatbot experience, you can adjust various settings in the `about:config` page:

- **Custom Prompts:**
  - Search for `browser.ml.chat.prompts.#` (replace `#` with a number).
  - Click the + button to add a new prompt.
  - Enter the prompt label, value, and ID.

- **Provider URL:**
  - Search for `browser.ml.chat.provider`.
  - Enter your Open WebUI instance URL along with any optional parameters.

### URL Parameters for Open WebUI

You can customize your Open WebUI instance using various URL parameters:

| Parameter | Description |
| --- | --- |
| models | Specify multiple models (comma-separated list) for the chat session. |
| model | Specify a single model for the chat session. |
| youtube | Provide a YouTube video ID to transcribe the video in the chat. |
| web-search | Enable web search functionality by setting this parameter to true. |
| tools or tool-ids | Specify a comma-separated list of tool IDs to activate in the chat. |
| call | Enable a video or call overlay in the chat interface by setting this parameter to true. |
| q | Set an initial query or prompt for the chat. |
| temporary-chat | Mark the chat as a temporary session by setting this parameter to true. |

For more detailed information, refer to [URL Parameters](https://docs.openwebui.com/features/chat-features/url-params).

### Additional about:config Settings

You can adjust additional settings in `about:config` for further customization:

| Setting | Description |
| --- | --- |
| browser.ml.chat.shortcuts | Enable custom shortcuts for the AI chatbot sidebar. |
| browser.ml.chat.shortcuts.custom | Enable custom shortcut keys for the AI chatbot sidebar. |
| browser.ml.chat.shortcuts.longPress | Set the long press delay for shortcut keys. |
| browser.ml.chat.sidebar | Enable the AI chatbot sidebar. |
| browser.ml.checkForMemory | Check for available memory before loading models. |
| browser.ml.defaultModelMemoryUsage | Set the default memory usage for models. |
| browser.ml.enable | Enable machine learning features in Firefox. |
| browser.ml.logLevel | Set the log level for machine learning features. |
| browser.ml.maximumMemoryPressure | Set the maximum memory pressure threshold. |
| browser.ml.minimumPhysicalMemory | Set the minimum physical memory required. |
| browser.ml.modelCacheMaxSize | Set the maximum size of the model cache. |
| browser.ml.modelCacheTimeout | Set the timeout for model cache. |
| browser.ml.modelHubRootUrl | Set the root URL for the model hub. |
| browser.ml.modelHubUrlTemplate | Set the URL template for the model hub. |
| browser.ml.queueWaitInterval | Set the interval for queue wait. |
| browser.ml.queueWaitTimeout | Set the timeout for queue wait. |

### Accessing the AI Chatbot Sidebar

To access the AI chatbot sidebar, use one of the following methods:

- Press `CTRL+B` to open the bookmarks sidebar and switch to **AI Chatbot**.
- Press `CTRL+Alt+X` to open the AI chatbot sidebar directly.

## Summary
This tutorial guides users through integrating Open WebUI as an AI chatbot in Firefox. It covers prerequisites, enabling the feature, configuring settings, customizing prompts, and accessing the sidebar. The integration allows for a personalized browsing experience with AI assistance.

# Tags
#firefox #ai-chatbot #integration #tutorial #openwebui