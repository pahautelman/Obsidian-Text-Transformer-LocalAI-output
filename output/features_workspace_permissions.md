# Permissions

## Key Concepts
- Workspace permissions
  - Models Access
  - Knowledge Access
  - Prompts Access
  - Tools Access
- Chat permissions
  - Allow Chat Controls
  - Allow File Upload
  - Allow Chat Delete
  - Allow Chat Edit
  - Allow Temporary Chat
- Features permissions
  - Web Search
  - Image Generation
  - Code Interpreter

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/workspace/permissions](https://docs.openwebui.com/features/workspace/permissions)

### Workspace Permissions
Workspace permissions control access to core components of the Open WebUI platform. These include:

- **Models Access**
  - Allows users to access and manage custom models.
  - Environment variable: `USER_PERMISSIONS_WORKSPACE_MODELS_ACCESS`

- **Knowledge Access**
  - Allows users to access and manage knowledge bases.
  - Environment variable: `USER_PERMISSIONS_WORKSPACE_KNOWLEDGE_ACCESS`

- **Prompts Access**
  - Allows users to access and manage saved prompts.
  - Environment variable: `USER_PERMISSIONS_WORKSPACE_PROMPTS_ACCESS`

- **Tools Access**
  - Allows users to access and manage tools.
  - Enabling this gives users the ability to upload arbitrary code to the server.
  - Environment variable: `USER_PERMISSIONS_WORKSPACE_TOOLS_ACCESS`

### Chat Permissions
Chat permissions determine what actions users can perform within chat conversations. These include:

- **Allow Chat Controls**
  - Enables access to chat control options.

- **Allow File Upload**
  - Permits users to upload files during chat sessions.
  - Environment variable: `USER_PERMISSIONS_CHAT_FILE_UPLOAD`

- **Allow Chat Delete**
  - Permits users to delete chat conversations.
  - Environment variable: `USER_PERMISSIONS_CHAT_DELETE`

- **Allow Chat Edit**
  - Permits users to edit messages in chat conversations.
  - Environment variable: `USER_PERMISSIONS_CHAT_EDIT`

- **Allow Temporary Chat**
  - Permits users to create temporary chat sessions.
  - Environment variable: `USER_PERMISSIONS_CHAT_TEMPORARY`

### Features Permissions
Features permissions control access to specialized capabilities within Open WebUI. These include:

- **Web Search**
  - Allows users to perform web searches during chat sessions.
  - Environment variable: `ENABLE_RAG_WEB_SEARCH`

- **Image Generation**
  - Allows users to generate images.
  - Environment variable: `ENABLE_IMAGE_GENERATION`

- **Code Interpreter**
  - Allows users to use the code interpreter feature.

### Default Permission Settings
By default, Open WebUI applies the following permission settings:

#### Workspace Permissions:
| Permission                | Default Setting |
|---------------------------|------------------|
| Models Access             | Disabled         |
| Knowledge Access          | Disabled         |
| Prompts Access            | Disabled         |
| Tools Access              | Disabled         |

#### Chat Permissions:
| Permission                | Default Setting |
|---------------------------|-----------------|
| Allow Chat Controls       | Enabled         |
| Allow File Upload         | Enabled         |
| Allow Chat Delete         | Enabled         |
| Allow Chat Edit           | Enabled         |
| Allow Temporary Chat      | Enabled         |

#### Features Permissions:
| Permission                | Default Setting |
|---------------------------|-----------------|
| Web Search                | Enabled         |
| Image Generation          | Enabled         |
| Code Interpreter          | Enabled         |

### Managing Permissions
Administrators can adjust these permissions through the user interface or by setting the corresponding environment variables in the configuration. All permission-related environment variables are marked as `PersistentConfig` variables, meaning they are stored internally after the first launch and can be managed through the Open WebUI interface.

> **Note:** For more detailed information about environment variables related to permissions, see the [Environment Variable Configuration documentation](https://docs.openwebui.com/features/workspace/permissions).

## Summary
The Permissions section in Open WebUI allows administrators to configure access controls and feature availability for users. This includes managing workspace permissions, chat permissions, and features permissions through a user-friendly interface or environment variables.

# Tags
#permissions #workspace #chat #features #accesscontrol