# Kokoro-FastAPI Using Docker

## Key Concepts
- Kokoro-FastAPI overview
- Key features (OpenAI compatibility, GPU/CPU support)
- Supported voices and languages
- Requirements for setup
- Quick start guide (GPU and CPU versions)
- Integration with Open WebUI
- Building the Docker container

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/text-to-speech/Kokoro-FastAPI-integration](https://docs.openwebui.com/tutorials/text-to-speech/Kokoro-FastAPI-integration)

### Overview
Kokoro-FastAPI is a Dockerized FastAPI wrapper for the Kokoro-82M text-to-speech model. It adheres to the OpenAI API endpoint specification, offering high-performance text-to-speech capabilities with impressive generation speeds.

### Key Features

| Feature | Description |
|---------|-------------|
| **OpenAI Compatibility** | Supports inline voice combination and integrates seamlessly with OpenAI endpoints. |
| **Hardware Support** | Can run on NVIDIA GPUs with CUDA 12.3 or CPUs using ONNX inference. |
| **Streaming Support** | Offers variable chunking for efficient streaming. |
| **Audio Formats** | Supports multiple audio formats: .mp3, .wav, .opus, .flac, .aac, .pcm. |
| **Web Interface** | Integrated web interface accessible at `localhost:8880/web`. |
| **Phoneme Endpoints** | Provides endpoints for phoneme conversion and generation. |

### Supported Voices
- **African Languages:**
  - af_bella
  - af_irulan
  - af_nicole
  - af_sarah
  - af_sky

- **American Languages:**
  - am_adam
  - am_michael
  - am_gurney

- **British Female Voices:**
  - bf_emma
  - bf_isabella

- **British Male Voices:**
  - bm_george
  - bm_lewis

### Supported Languages
- English (US)
- English (UK)

### Requirements
To set up Kokoro-FastAPI, ensure you have the following:
- Docker installed on your system.
- Open WebUI running.
- For GPU support: NVIDIA GPU with CUDA 12.3.
- For CPU-only setup: No special requirements.

### Quick Start Guide

#### GPU Version
Requires an NVIDIA GPU with CUDA 12.3.

**Using Docker Run:**
```bash
docker run --gpus all -p 8880:8880 ghcr.io/remsky/kokoro-fastapi-gpu
```

**Using Docker Compose:**
Create a `docker-compose.yml` file:
```yaml
name: kokoroservices
services:
  kokoro-fastapi-gpu:
    ports:
      - "8880:8880"
    image: ghcr.io/remsky/kokoro-fastapi-gpu:v0.2.1
    restart: always
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```
Run the compose file:
```bash
docker compose up
```

#### CPU Version (ONNX Optimized Inference)

**Using Docker Run:**
```bash
docker run -p 8880:8880 ghcr.io/remsky/kokoro-fastapi-cpu
```

**Using Docker Compose:**
Create a `docker-compose.yml` file:
```yaml
name: kokoroservices
services:
  kokoro-fastapi-cpu:
    ports:
      - "8880:8880"
    image: ghcr.io/remsky/kokoro-fastapi-cpu
    restart: always
```
Run the compose file:
```bash
docker compose up
```

### Setting Up Open WebUI to Use Kokoro-FastAPI

1. **Open Admin Panel:**
   - Navigate to `Settings -> Audio`.

2. **Configure TTS Settings:**
   - **Text-to-Speech Engine:** OpenAI API
   - **Base URL:** `http://localhost:8880/v1` (or `host.docker.internal`)
   - **API Key:** not-needed
   - **TTS Model:** kokoro
   - **TTS Voice:** af_bella

### Building the Docker Container

1. Clone the repository:
```bash
git clone https://github.com/remsky/Kokoro-FastAPI.git
cd Kokoro-FastAPI
```

2. Navigate to the appropriate directory (CPU or GPU):
```bash
cd docker/cpu # or cd docker/gpu
```

3. Build and run the Docker container:
```bash
docker compose up --build
```
For more detailed instructions, refer to the [Kokoro-FastAPI repository](https://github.com/remsky/Kokoro-FastAPI).

## Summary

This tutorial provides a comprehensive guide on integrating Kokoro-FastAPI with Open WebUI using Docker. It covers key features, setup requirements, quick start instructions for both GPU and CPU versions, and detailed steps to configure Open WebUI for text-to-speech functionality.

# Tags
#kokoro-fastapi #docker #text-to-speech #openwebui #tutorial