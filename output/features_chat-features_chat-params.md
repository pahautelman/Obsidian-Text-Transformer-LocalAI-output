# Chat Parameters

## Key Concepts
- System Prompt and Advanced Parameters hierarchy
  - Per-chat basis settings
  - Per-account basis settings
  - Per-model basis settings
- Setting and overriding capabilities for each level
- Flexibility in system prompt configuration

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/chat-features/chat-params](https://docs.openwebui.com/features/chat-features/chat-params)

### System Prompt and Advanced Parameters Hierarchy

Open WebUI provides a hierarchical system for setting **System Prompts** and **Advanced Parameters**, allowing flexibility while maintaining structured administration. The hierarchy includes three levels:

1. **Per-chat Basis**
   - **Description:** Settings configured for a specific chat instance, applicable only to the current conversation.
   - **How to Set:**
     - Users can modify settings within the Chat Controls section in Open WebUI.
   - **Override Capabilities:**
     - Users cannot override settings already defined by an administrator on a per-model basis.

2. **Per-account Basis**
   - **Description:** Default settings configured for a specific user account, serving as a fallback when lower-level settings are not defined.
   - **How to Set:**
     - Users can set their own system prompt and advanced parameters within the General section of the Settings menu in Open WebUI.
   - **Override Capabilities:**
     - User-defined settings can be overridden by administrator settings on a per-model basis.

3. **Per-model Basis**
   - **Description:** Default settings configured for a specific model, applicable to all chat instances using that model.
   - **How to Set:**
     - Administrators set these within the Models section of the Workspace in Open WebUI.
   - **Override Capabilities:**
     - User accounts cannot modify these settings, ensuring consistency and preventing inappropriate alterations.

### Optimizing System Prompt Settings

To achieve maximum flexibility with system prompts:

- **Primary System Prompt:** Set this at the per-account level in the General settings. This prompt will apply across all LLMs without requiring adjustments within individual models.
- **Secondary System Prompt:**
  - For administrators, set this on a per-model basis using the Models section of the Workspace.
  - For users, set this on a per-chat basis using the Chat Controls sidebar.

### Priority Order

Understanding the priority order is crucial:
1. Per-model settings take precedence over per-account and per-chat settings.
2. Per-account settings serve as a fallback when lower-level settings are not defined.
3. Per-chat settings apply only to the current conversation.

## Summary
Open WebUI offers a hierarchical system for setting System Prompts and Advanced Parameters at per-chat, per-account, and per-model levels. This structure provides flexibility while ensuring consistency and control over chat configurations.

# Tags
#chatparameters #systemprompt #advancedparameters #hierarchy #flexibility