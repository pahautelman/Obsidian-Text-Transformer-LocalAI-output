# Integrating openai-edge-tts 🗣️ with Open WebUI

## Key Concepts
- openai-edge-tts API
- Text-to-Speech (TTS)
- Docker setup
- Python environment configuration
- API endpoints and parameters
- Community contributions

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/text-to-speech/openai-edge-tts-integration](https://docs.openwebui.com/tutorials/text-to-speech/openai-edge-tts-integration)

### Overview
This tutorial guides you through integrating the openai-edge-tts API with Open WebUI, enabling high-quality text-to-speech functionality. This community-contributed guide is not officially supported by the Open WebUI team but serves as a demonstration for customizing Open WebUI.

### What is openai-edge-tts?
openai-edge-tts is a TTS API that mimics the OpenAI API endpoint, allowing it to be used as a direct substitute in scenarios where the endpoint URL can be configured. It leverages the Edge browser's free "Read Aloud" feature to provide high-quality text-to-speech.

### Requirements
To get started with openai-edge-tts, ensure you have:
- Docker installed on your system.
- Open WebUI running.

### Quick Start with Docker

The simplest way to start is by running the following Docker command:

```bash
docker run -d -p 5050:5050 travisvn/openai-edge-tts:latest
```

This command runs the service at port 5050 with default configurations.

### Setting Up Open WebUI

1. **Open Admin Panel:**
   - Navigate to Settings -> Audio.
   - Set your TTS settings as shown in the provided screenshot.
   - Specify the TTS Voice if needed.

2. **API Key Configuration:**
   - The default API key is `your_api_key_here`. Change it only if additional security is required.

### Running with Python

If you prefer to run openai-edge-tts directly with Python, follow these steps:

1. **Clone the Repository:**

```bash
git clone https://github.com/travisvn/openai-edge-tts.git
cd openai-edge-tts
```

2. **Set Up a Virtual Environment:**
   - For macOS/Linux:
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```
   - For Windows:
     ```bash
     python -m venv venv
     venv\Scripts\activate
     ```

3. **Install Dependencies:**

```bash
pip install -r requirements.txt
```

4. **Configure Environment Variables:**
   Create a `.env` file in the root directory with the following variables:

```env
API_KEY=your_api_key_here
PORT=5050
DEFAULT_VOICE=en-US-AvaNeural
DEFAULT_RESPONSE_FORMAT=mp3
DEFAULT_SPEED=1.0
DEFAULT_LANGUAGE=en-US
REQUIRE_API_KEY=True
REMOVE_FILTER=False
EXPAND_API=True
```

5. **Run the Server:**

```bash
python app/server.py
```

The server will start running at [http://localhost:5050](http://localhost:5050).

### Testing the API

You can interact with the API at [http://localhost:5050/v1/audio/speech](http://localhost:5050/v1/audio/speech). Here are some example requests:

- **Basic Request:**

```bash
curl -X POST http://localhost:5050/v1/audio/speech \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here" \
-d '{ "input": "Hello, I am your AI assistant! Just let me know how I can help bring your ideas to life.", "voice": "echo", "response_format": "mp3", "speed": 1.0 }' \
--output speech.mp3
```

- **OpenAI API Endpoint Parameters:**

```bash
curl -X POST http://localhost:5050/v1/audio/speech \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here" \
-d '{ "model": "tts-1", "input": "Hello, I am your AI assistant! Just let me know how I can help bring your ideas to life.", "voice": "alloy" }' \
--output speech.mp3
```

- **Non-English Language:**

```bash
curl -X POST http://localhost:5050/v1/audio/speech \
-H "Content-Type: application/json" \
-H "Authorization: Bearer your_api_key_here" \
-d '{ "model": "tts-1", "input": "じゃあ、行く。電車の時間、調べておくよ。", "voice": "ja-JP-KeitaNeural" }' \
--output speech.mp3
```

### Additional Endpoints

- **List Available TTS Models:**
  ```bash
  POST/GET /v1/models
  ```

- **List edge-tts Voices for a Given Language/Locale:**
  ```bash
  POST/GET /v1/voices
  ```

- **List All edge-tts Voices with Language Support Information:**
  ```bash
  POST/GET /v1/voices/all
  ```

### Quick Config for Docker

You can configure environment variables directly in the Docker run command:

```bash
docker run -d -p 5050:5050 \
-e API_KEY=your_api_key_here \
-e PORT=5050 \
-e DEFAULT_VOICE=en-US-AvaNeural \
-e DEFAULT_RESPONSE_FORMAT=mp3 \
-e DEFAULT_SPEED=1.0 \
-e DEFAULT_LANGUAGE=en-US \
-e REQUIRE_API_KEY=True \
-e REMOVE_FILTER=False \
-e EXPAND_API=True \
travisvn/openai-edge-tts:latest
```

### Additional Resources

For more information, visit the [openai-edge-tts GitHub repo](https://github.com/travisvn/openai-edge-tts).

For direct support, join the Voice AI & TTS Discord community.

## Summary
This tutorial provides a step-by-step guide to integrating openai-edge-tts with Open WebUI using Docker or Python. It covers setting up the environment, configuring API keys, and testing various endpoints to enable high-quality text-to-speech functionality.

# Tags
#openwebui #texttospeech #docker #python #api #integration