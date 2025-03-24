# Integrating Continue.dev VSCode Extension with Open WebUI

## Key Concepts
- Community contribution tutorial
- Installing and configuring the Continue.dev VSCode extension
- Configuring `config.json` for Open WebUI integration
- Using OpenAI API spec compatibility
- Setting up models in Continue.dev

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/continue-dev](https://docs.openwebui.com/tutorials/integrations/continue-dev)

### Overview
This tutorial demonstrates how to integrate the **Continue.dev VSCode Extension** with Open WebUI. It is a community-contributed guide and not officially supported by the Open WebUI team.

### Installation

1. **Download the Extension**
   - Download the Continue.dev extension from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=continue.continue).

2. **Access Settings**
   - After installation, open the 'continue' tab in the VSCode sidebar.
   - Click on the settings icon (cog) at the bottom right to open `config.json`.

### Configuration

1. **Edit `config.json`**

   - Change the provider to `openai`.
     ```json
     "provider": "openai"
     ```

   - Set `apiBase` to your Open WebUI domain.
     ```json
     "apiBase": "http://localhost:3000/"
     ```
     *Note:* This assumes you followed the Getting Started Docker instructions.

   - Add your API key.
     ```json
     "apiKey": "sk-79970662256d425eb274fc4563d4525b"
     ```
     *Note:* Replace `sk-79970662256d425eb274fc4563d4525b` with your actual API key, which you can find in Open WebUI under Settings -> Account -> API Keys.

### Example Configuration

Here is an example of a `config.json` file configured to use Open WebUI via the OpenAI provider:

```json
{
  "models": [
    {
      "title": "Granite Code",
      "provider": "openai",
      "model": "granite-code:latest",
      "useLegacyCompletionsEndpoint": false,
      "apiBase": "http://YOUROPENWEBUI/ollama/v1",
      "apiKey": "sk-YOUR-API-KEY"
    },
    {
      "title": "Model ABC from pipeline",
      "provider": "openai",
      "model": "PIPELINE_MODEL_ID",
      "useLegacyCompletionsEndpoint": false,
      "apiBase": "http://YOUROPENWEBUI/api",
      "apiKey": "sk-YOUR-API-KEY"
    }
  ],
  "customCommands": [
    {
      "name": "test",
      "prompt": "{{{ input }}}\n\nWrite a comprehensive set of unit tests for the selected code. It should setup, run tests that check for correctness including important edge cases, and teardown. Ensure that the tests are complete and sophisticated. Give the tests just as chat output, don't edit any file.",
      "description": "Write unit tests for highlighted code"
    }
  ],
  "tabAutocompleteModel": {
    "title": "Granite Code",
    "provider": "openai",
    "model": "granite-code:latest",
    "useLegacyCompletionsEndpoint": false,
    "apiBase": "http://localhost:3000/ollama/v1",
    "apiKey": "sk-YOUR-API-KEY"
  }
}
```

### Final Steps

1. Save `config.json`.
2. Select your model from the Continue tab.
3. Start chatting via Open WebUI.

> **Note:** You can configure multiple models in this manner, but it is recommended to use models designed for code.

For additional configuration options, refer to the [Continue Documentation](https://docs.continue.dev/).

## Summary
This tutorial guides users through installing and configuring the Continue.dev VSCode extension to work with Open WebUI. By following these steps, you can integrate Open WebUI's capabilities into your development workflow within VSCode.

# Tags
#integration #vscode #continue #openwebui #tutorial