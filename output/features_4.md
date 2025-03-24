# Conversations

## Key Concepts
- True Asynchronous Chat
- Chat Completion Notifications
- Notification Webhook Integration
- Channels (Beta)
- Typing Indicators in Channels
- User Status Indicators
- Chat Controls
- Favorite Response Management
- Pinned Chats
- RAG Embedding Support
- Citations in RAG Feature
- Enhanced RAG Pipeline
- YouTube RAG Pipeline
- Comprehensive Document Retrieval
- RAG Citation Relevance
- Advanced RAG
- Inline Citations for RAG
- Large Text Handling
- Multi-Modal Support
- Multiple Model Support
- Merge Responses in Many Model Chat
- Multiple Instances of Same Model in Chats
- Temporary Chat Feature
- User Message Editing
- Efficient Conversation Editing
- Client-Side Image Compression
- '@' Model Integration
- Conversation Tagging
- Auto-Tagging
- Chat Cloning
- Visualized Conversation Flows
- Chat Folders
- Easy Chat Import
- Prompt Preset Support
- Prompt Variables Support
- Memory Feature

## Detailed Description

### True Asynchronous Chat
Enjoy uninterrupted multitasking with true asynchronous chat support, allowing you to create chats, navigate away, and return anytime with responses ready.

### Chat Completion Notifications
Stay updated with instant in-UI notifications when a chat finishes in a non-active tab, ensuring you never miss a completed response.

### Notification Webhook Integration
Receive timely updates for long-running chats or external integration needs with configurable webhook notifications, even when your tab is closed.

### Channels (Beta)
Explore real-time collaboration between users and AIs with Discord/Slack-style chat rooms, build bots for channels, and unlock asynchronous communication for proactive multi-agent workflows.

### Typing Indicators in Channels
Enhance collaboration with real-time typing indicators in channels, keeping everyone engaged and informed.

### User Status Indicators
Quickly view a user's status by clicking their profile image in channels, providing better coordination and availability insights.

### Chat Controls
Easily adjust parameters for each chat session, offering more precise control over your interactions.

### Favorite Response Management
Easily mark and organize favorite responses directly from the chat overview, enhancing ease of retrieval and access to preferred responses.

### Pinned Chats
Support for pinned chats, allowing you to keep important conversations easily accessible.

### RAG Embedding Support
Change the Retrieval Augmented Generation (RAG) embedding model directly in the Admin Panel > Settings > Documents menu, enhancing document processing. This feature supports Ollama and OpenAI models.

### Citations in RAG Feature
The Retrieval Augmented Generation (RAG) feature allows users to easily track the context of documents fed to LLMs with added citations for reference points.

### Enhanced RAG Pipeline
A togglable hybrid search sub-feature for our RAG embedding feature that enhances the RAG functionality via BM25, with re-ranking powered by CrossEncoder, and configurable relevance score thresholds.

### YouTube RAG Pipeline
The dedicated Retrieval Augmented Generation (RAG) pipeline for summarizing YouTube videos via video URLs enables smooth interaction with video transcriptions directly.

### Comprehensive Document Retrieval
Toggle between full document retrieval and traditional snippets, enabling comprehensive tasks like summarization and supporting enhanced document capabilities.

### RAG Citation Relevance
Easily assess citation accuracy with the addition of relevance percentages in RAG results.

### Advanced RAG
Improve RAG accuracy with smart pre-processing of chat history to determine the best queries before retrieval.

### Inline Citations for RAG
Benefit from seamless inline citations for Retrieval-Augmented Generation (RAG) responses, improving traceability and providing source clarity for newly uploaded files.

### Large Text Handling
Optionally convert large pasted text into a file upload to be used directly with RAG, keeping the chat interface cleaner.

### Multi-Modal Support
Effortlessly engage with models that support multi-modal interactions, including images (e.g., LLaVA).

### Multiple Model Support
Quickly switch between different models for diverse chat interactions.

### Merge Responses in Many Model Chat
Enhances the dialogue by merging responses from multiple models into a single, coherent reply.

### Multiple Instances of Same Model in Chats
Enhanced many model chat to support adding multiple instances of the same model.

### Temporary Chat Feature
Introduced a temporary chat feature, deprecating the old chat history setting to enhance user interaction flexibility.

### User Message Editing
Enhanced the user chat editing feature to allow saving changes without sending.

### Efficient Conversation Editing
Create new message pairs quickly and intuitively using the Cmd/Ctrl+Shift+Enter shortcut, streamlining conversation length tests.

### Client-Side Image Compression
Save bandwidth and improve performance with client-side image compression, allowing you to compress images before upload from Settings > Interface.

### '@' Model Integration
By seamlessly switching to any accessible local or external model during conversations, users can harness the collective intelligence of multiple models in a single chat. This can be done by using the @ command to specify the model by name within a chat.

### Conversation Tagging
Effortlessly categorize and locate tagged chats for quick reference and streamlined data collection using our efficient 'tag:' query system, allowing you to manage, search, and organize your conversations without cluttering the interface.

### Auto-Tagging
Conversations can optionally be automatically tagged for improved organization, mirroring the efficiency of auto-generated titles.

### Chat Cloning
Easily clone and save a snapshot of any chat for future reference or continuation. This feature makes it easy to pick up where you left off or share your session with others. To create a copy of your chat, simply click on the Clone button in the chat's dropdown options. Can you keep up with your clones?

### Visualized Conversation Flows
Interactive messages diagram for improved visualization of conversation flows, enhancing understanding and navigation of complex discussions.

### Chat Folders
Organize your chats into folders, drag and drop them for easy management, and export them seamlessly for sharing or analysis.

### Easy Chat Import
Import chats into your workspace by simply dragging and dropping chat exports (JSON) onto the sidebar.

### Prompt Preset Support
Instantly access custom preset prompts using the / command in the chat input. Load predefined conversation starters effortlessly and expedite your interactions. Import prompts with ease through Open WebUI Community integration or create your own!

### Prompt Variables Support
Prompt variables such as {{CLIPBOARD}}, {{CURRENT_DATE}}, {{CURRENT_DATETIME}}, {{CURRENT_TIME}}, {{CURRENT_TIMEZONE}}, {{CURRENT_WEEKDAY}}, {{USER_NAME}}, {{USER_LANGUAGE}}, and {{USER_LOCATION}} can be utilized in the system prompt or by using a slash command to select a prompt directly within a chat. Please note that the {{USER_LOCATION}} prompt variable requires a secure connection over HTTPS. To utilize this particular prompt variable, please ensure that {{USER_LOCATION}} is toggled on from the Settings > Interface menu. Please note that the {{CLIPBOARD}} prompt variables require access to your device's clipboard.

### Memory Feature
Manually add information you want your LLMs to remember via the Settings > Personalization > Memory menu. Memories can be added, edited, and deleted.

## Summary
Open WebUI enhances conversation management with features like asynchronous chat support, real-time notifications, collaborative channels, advanced RAG capabilities, multi-modal interactions, model integration, and efficient editing tools. These enhancements ensure a seamless and productive user experience.

# Tags
#conversations #asynchronouschat #notifications #collaboration #RAG #multimodal #modelintegration #editing