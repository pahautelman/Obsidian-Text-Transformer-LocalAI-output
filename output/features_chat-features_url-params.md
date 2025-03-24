# URL Parameters

## Key Concepts
- Customizing chat sessions with URL parameters
- Model selection (models, model)
- YouTube transcription (youtube)
- Web search functionality (web-search)
- Tool activation (tools, tool-ids)
- Call overlay (call)
- Initial query prompt (q)
- Temporary chat sessions (temporary-chat)

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/chat-features/url-params](https://docs.openwebui.com/features/chat-features/url-params)

### Overview
In Open WebUI, URL parameters allow for customization of chat sessions. These parameters enable specific configurations and features on a per-chat basis directly from the URL.

### URL Parameter Overview

| Parameter       | Function                                                                 | Example Usage                                 |
|-----------------|--------------------------------------------------------------------------|-----------------------------------------------|
| models          | Specify multiple language models for the chat session                   | /?models=model1,model2                        |
| model           | Set a single language model for the chat session                       | /?model=model1                                |
| youtube         | Transcribe a specified YouTube video                                     | /?youtube=VIDEO_ID                            |
| web-search      | Enable web search functionality within the chat                         | /?web-search=true                             |
| tools           | Activate specific tools within the chat session                          | /?tools=tool1,tool2                           |
| tool-ids        | Activate specific tools within the chat session (alternative to tools)  | /?tool-ids=tool1,tool2                        |
| call            | Enable a video or call overlay in the chat interface                    | /?call=true                                   |
| q               | Set an initial query or prompt for the chat                             | /?q=Hello%20there                              |
| temporary-chat  | Mark the chat as a temporary session, limiting features like saving history | /?temporary-chat=true                         |

### Detailed Parameter Descriptions

#### Models and Model Selection
- **Description:** Specify which language models to use for a particular chat session.
- **How to Set:**
  - Use `models` for multiple models or `model` for a single model.
- **Examples:**
  - `/?models=model1,model2`: Initializes the chat with both `model1` and `model2`.
  - `/?model=model1`: Sets `model1` as the sole model for the chat.

#### YouTube Transcription
- **Description:** Enables transcription of a specified YouTube video within the chat.
- **How to Set:**
  - Use the YouTube video ID as the value for this parameter.
- **Example:**
  - `/?youtube=VIDEO_ID`: Triggers transcription functionality for the provided YouTube video.

#### Web Search
- **Description:** Enables web search functionality within the chat session.
- **How to Set:**
  - Set `web-search` to true.
- **Example:**
  - `/?web-search=true`: Allows the chat to retrieve web search results as part of its responses.

#### Tool Selection
- **Description:** Specify which tools to activate within the chat.
- **How to Set:**
  - Provide a comma-separated list of tool IDs.
- **Examples:**
  - `/?tools=tool1,tool2`: Activates `tool1` and `tool2`.
  - `/?tool-ids=tool1,tool2`: Alternative syntax for activating tools.

#### Call Overlay
- **Description:** Enables a video or call overlay in the chat interface.
- **How to Set:**
  - Set `call` to true.
- **Example:**
  - `/?call=true`: Activates a call interface overlay with features like live transcription and video input.

#### Initial Query Prompt
- **Description:** Sets an initial query or prompt for the chat session.
- **How to Set:**
  - Specify the query or prompt text as the parameter value.
- **Example:**
  - `/?q=Hello%20there`: Starts the chat with the specified prompt.

#### Temporary Chat Sessions
- **Description:** Marks the chat as a temporary session, limiting features like saving history.
- **How to Set:**
  - Set `temporary-chat` to true.
- **Example:**
  - `/?temporary-chat=true`: Initiates a disposable chat session without saving history.

### Combining Multiple Parameters
URL parameters can be combined to create highly customized chat sessions. For example:

```
/chat?models=model1,model2&youtube=VIDEO_ID&web-search=true&tools=tool1,tool2&call=true&q=Hello%20there&temporary-chat=true
```

This URL will:
- Initialize the chat with `model1` and `model2`.
- Enable YouTube transcription.
- Enable web search functionality.
- Activate specified tools (`tool1`, `tool2`).
- Display a call overlay.
- Set an initial prompt of "Hello there."
- Mark the chat as temporary, avoiding any history saving.

## Summary
URL parameters in Open WebUI allow for extensive customization of chat sessions. By using these parameters, users can specify models, enable features like YouTube transcription and web search, activate tools, set initial prompts, and manage session persistence directly from the URL.

# Tags
#urlparameters #chatcustomization #webui #models #youtube #websearch #tools #calloverlay #initialprompt #temporarychat