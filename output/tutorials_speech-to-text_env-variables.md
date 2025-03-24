# Environment Variables List

## Key Concepts
- Open WebUI environment variables
- Speech to Text (STT) specific variables
  - WHISPER_MODEL
  - WHISPER_MODEL_DIR
  - AUDIO_STT_ENGINE
  - AUDIO_STT_MODEL
  - AUDIO_STT_OPENAI_API_BASE_URL
  - AUDIO_STT_OPENAI_API_KEY

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/speech-to-text/env-variables](https://docs.openwebui.com/tutorials/speech-to-text/env-variables)

### Overview
This document provides a summary of environment variables specifically related to Speech to Text (STT) functionality in Open WebUI. For a comprehensive list of all environment variables, refer to the [Environment Variable Configuration page](https://docs.openwebui.com/tutorials/speech-to-text/env-variables).

### STT Environment Variables

| Variable Name                | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| `WHISPER_MODEL`              | Specifies the model used for speech recognition.                           |
| `WHISPER_MODEL_DIR`          | Directory path where the Whisper model is stored.                          |
| `AUDIO_STT_ENGINE`           | Engine used for audio-to-text conversion (e.g., OpenAI).                    |
| `AUDIO_STT_MODEL`            | Model used by the STT engine for converting audio to text.                  |
| `AUDIO_STT_OPENAI_API_BASE_URL` | Base URL for the OpenAI API endpoint.                                       |
| `AUDIO_STT_OPENAI_API_KEY`   | API key required for authenticating requests to the OpenAI service.         |

## Summary
This document lists and describes the environment variables essential for configuring Speech to Text (STT) functionality in Open WebUI, including model specifications, engine settings, and API credentials.

# Tags
#environment #variables #speech-to-text #stt #openwebui