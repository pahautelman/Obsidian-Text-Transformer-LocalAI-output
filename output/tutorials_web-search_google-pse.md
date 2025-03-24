# Google PSE

## Key Concepts
- Community contribution tutorial
- Customizing Open WebUI for specific use cases
- Setting up Google Programmable Search Engine (PSE)
- Configuring API key and Search engine ID in Open WebUI Admin panel
- Enabling web search functionality

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/web-search/google-pse](https://docs.openwebui.com/tutorials/web-search/google-pse)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI for specific use cases. It focuses on integrating Google's Programmable Search Engine (PSE) API.

### Setup Instructions

1. **Create a Google PSE Account**
   - Go to [Google Developers](https://developers.google.com/) and navigate to the Programmable Search Engine section.
   - Log in or create an account.
   - In the control panel, click the "Add" button.
   - Enter a search engine name and configure other properties as needed.
   - Verify that you are not a robot and click the "Create" button.

2. **Generate API Key and Search Engine ID**
   - After creating the search engine, generate an API key and obtain the Search Engine ID (available post-creation).

3. **Configure Open WebUI Admin Panel**
   - Open the Open WebUI Admin panel.
   - Navigate to the "Settings" tab and then click on "Web Search."
   - Enable web search and set the "Web Search Engine" to `google_pse`.
   - Fill in the "Google PSE API Key" with the generated API key and the "Google PSE Engine Id" with the Search Engine ID.
   - Click "Save."

### Enabling Web Search
To use the web search functionality:
- Enable web search in the prompt field using the plus (+) button.

> **Note:** The images referenced in the original text ([Image: Open WebUI Admin panel] and [Image: enable Web search]) provide visual guidance for these steps.

## Summary
This tutorial guides users through setting up Google PSE API with Open WebUI, enabling web search functionality. It involves creating a Google PSE account, generating necessary credentials, and configuring them in the Open WebUI Admin panel.

# Tags
#google #pse #api #websearch #openwebui