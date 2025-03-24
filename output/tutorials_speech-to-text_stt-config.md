# Configuration

## Key Concepts
- Speech-to-text support (local, browser, remote)
- Cloud speech-to-text providers
- Configuring STT provider
- User-level settings for STT
- Using STT functionality
- STT mode operation

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/speech-to-text/stt-config](https://docs.openwebui.com/tutorials/speech-to-text/stt-config)

### Speech-to-Text Support
Open Web UI supports multiple modes for speech-to-text functionality:
- **Local:** Processes audio directly on the user's device.
- **Browser:** Utilizes built-in browser capabilities for STT.
- **Remote:** Leverages cloud-based services for enhanced accuracy and features.

### Cloud / Remote Speech To Text Providers

Several cloud providers are supported, each requiring specific API keys:

| Provider | Configuration Method |
| --- | --- |
| OpenAI | Environment variables |
| Other Providers | Admin settings page |

### Configuring Your STT Provider
To set up a speech-to-text provider:
1. **Navigate to the admin settings.**
2. **Choose Audio Provider:** Select your preferred provider.
3. **Enter API Key:** Input the required API key.
4. **Select Model:** Choose a model from the dropdown menu.

### User-Level Settings

In addition to instance-wide settings configured in the admin panel, users can adjust specific STT preferences:

| Setting | Description |
| --- | --- |
| Speech-to-Text Engine | Determines the engine used for speech recognition (Default or Web API). |

### Using STT
Speech-to-text allows users to input prompts via voice, offering a convenient and efficient method for both desktop and mobile devices. To use STT:
1. Click on the microphone icon to start recording.
2. A live audio waveform will confirm successful voice capture.

### STT Mode Operation

During recording, you have several options:

- **Save Recording:** Click the tick icon to save. If "auto send after completion" is enabled, the recording will be sent automatically; otherwise, manual sending is required.
- **Abort Recording:** Click the 'x' icon to discard the current recording and start fresh.

## Summary
The configuration guide for speech-to-text in Open Web UI covers support for local, browser, and remote STT, cloud provider setup, user-level settings, usage instructions, and operational modes. This ensures a seamless experience for users leveraging voice input.

# Tags
#speech-to-text #configuration #STT #cloud-providers #user-settings