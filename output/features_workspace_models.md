# Models

## Key Concepts
- Model management in Workspace
- Modelfile actions (edit, clone, share, export, hide)
- Modelfile editing options
- Importing and exporting models
- Model switching for multi-stage tasks

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/workspace/models](https://docs.openwebui.com/features/workspace/models)

### Overview
The Models section within the Workspace of Open WebUI is a comprehensive tool designed to create and manage custom models tailored to specific needs. This central hub allows users to perform various actions on their modelfiles, including editing, cloning, sharing, exporting, and hiding.

### Modelfile Management

From the Models section, you can perform several key actions:

- **Edit:** Modify details of your modelfile.
- **Clone:** Create a copy of an existing modelfile. Note that base models cannot be cloned directly; you must create a model first before cloning it.
- **Share:** Share your modelfile with the Open WebUI community by clicking the Share button, which redirects to [https://openwebui.com/models/create](https://openwebui.com/models/create).
- **Export:** Download the modelfile's .json export to your PC.
- **Hide:** Hide the modelfile from the model selector dropdown within chats.

### Modelfile Editing

When editing a modelfile, you can customize various settings:

- **Avatar Photo:** Upload an avatar photo to represent your modelfile.
- **Model Name:** Change the name of your modelfile.
- **System Prompt:** Provide an optional system prompt for your modelfile.
- **Model Parameters:** Adjust the parameters of your modelfile.
- **Prompt Suggestions:** Add prompts that will be displayed on a fresh new chat page.
- **Documents:** Add documents to the modelfile (always RAG [Retrieval Augmented Generation]).
- **Tools, Filters, and Actions:** Select the tools, filters, and actions available to the modelfile.
- **Vision:** Toggle to enable Vision for multi-modals.
- **Tags:** Add tags to the modelfile that will be displayed beside the model name in the model selector dropdown.

### Model Discovery and Import/Export

The Models section also includes features for importing and exporting models:

- **Import Models:** Use this button to import models from a .json file or other sources.
- **Export Models:** Use this button to export all your modelfiles in a single .json file.

To download models, navigate to the Ollama Settings in the Connections tab. Alternatively, you can also download models directly by typing a command like `ollama run hf.co/[model creator]/[model name]` in the model selection dropdown. This action will create a button labeled "Pull [Model Name]" for downloading.

### Model Switching

#### Example: Switching between Mistral, LLaVA, and GPT-3.5 in a Multi-Stage Task

**Scenario:**
A multi-stage conversation involves different task types, such as starting with a simple FAQ, interpreting an image, and then generating a creative response.

**Reason for Switching:**
The user can leverage each model's specific strengths for each stage:
- **Mistral:** For general questions to reduce computation time and costs.
- **LLaVA:** For visual tasks to gain insights from image-based data.
- **GPT-3.5:** For generating more sophisticated and nuanced language output.

**Process:**
The user switches between models, depending on the task type, to maximize efficiency and response quality.

**How To:**

1. **Select the Model:** Within the chat interface, select the desired models from the model switcher dropdown. You can select up to two models simultaneously, and both responses will be generated.
2. **Navigate Between Responses:** Use the back and forth arrows to navigate between the responses.
3. **Context Preservation:** Open WebUI retains the conversation context across model switches, allowing smooth transitions.

## Summary
The Models section in Open WebUI's Workspace is a powerful tool for managing custom models. It offers features for editing, cloning, sharing, exporting, and hiding modelfiles, as well as importing and exporting models. Additionally, it supports switching between different models for multi-stage tasks, leveraging each model's strengths to enhance efficiency and response quality.

# Tags
#models #workspace #modelfile #management #editing #importing #exporting #switching