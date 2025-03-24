# Integrating openedai-speech into Open WebUI using Docker

## Key Concepts
- openedai-speech integration
- Docker Compose setup
- Docker run commands
- TTS configuration in Open WebUI
- Troubleshooting steps
- Model details and voice customization

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/text-to-speech/openedai-speech-integration](https://docs.openwebui.com/tutorials/text-to-speech/openedai-speech-integration)

### Overview
This tutorial guides you through integrating openedai-speech into Open WebUI using Docker. It is a community contribution and not officially supported by the Open WebUI team.

### What is openedai-speech?
openedai-speech is an API-compatible text-to-speech server that provides a free, private TTS experience with custom voice cloning capabilities. It serves the `/v1/audio/speech` endpoint and does not require an OpenAI API key.

### Requirements
- Docker installed on your system.
- Open WebUI running in a Docker container.
- Basic understanding of Docker and Docker Compose.

### Option 1: Using Docker Compose

#### Step-by-Step Guide

1. **Create a New Folder**
   - Create a new folder, e.g., `openedai-speech-service`, to store the `docker-compose.yml` and `speech.env` files.

2. **Clone the Repository**
   ```bash
   git clone https://github.com/matatonic/openedai-speech.git
   ```
   This command downloads the repository, including Docker Compose files (`docker-compose.yml`, `docker-compose.min.yml`, `docker-compose.rocm.yml`) and other necessary files.

3. **Configure Environment Variables**
   - Rename `sample.env` to `speech.env`.
   - Customize `speech.env` with the following content:
     ```env
     TTS_HOME=voicesHF_HOME=voices#PRELOAD_MODEL=xtts#PRELOAD_MODEL=xtts_v2.0.2#PRELOAD_MODEL=parler-tts/parler_tts_mini_v0.1#EXTRA_ARGS=--log-level DEBUG --unload-timer 300#USE_ROCM=1
     ```

4. **Choose a Docker Compose File**
   - `docker-compose.yml`: Uses the `ghcr.io/matatonic/openedai-speech` image.
   - `docker-compose.min.yml`: Minimal version with Piper support, no GPU required.
   - `docker-compose.rocm.yml`: Supports ROCm for AMD GPUs.

5. **Build the Docker Image**
   - For Nvidia GPU (CUDA):
     ```bash
     docker build -t ghcr.io/matatonic/openedai-speech .
     ```
   - For AMD GPU (ROCm):
     ```bash
     docker build -f Dockerfile --build-arg USE_ROCM=1 -t ghcr.io/matatonic/openedai-speech-rocm .
     ```
   - For CPU only:
     ```bash
     docker build -f Dockerfile.min -t ghcr.io/matatonic/openedai-speech-min .
     ```

6. **Run the Docker Compose Command**
   - Nvidia GPU (CUDA):
     ```bash
     docker compose up -d
     ```
   - AMD GPU (ROCm):
     ```bash
     docker compose -f docker-compose.rocm.yml up -d
     ```
   - ARM64 (Apple M-series, Raspberry Pi) or CPU only:
     ```bash
     docker compose -f docker-compose.min.yml up -d
     ```

### Option 2: Using Docker Run Commands

#### Step-by-Step Guide

1. **Nvidia GPU (CUDA)**
   ```bash
   docker build -t ghcr.io/matatonic/openedai-speech .
   docker run -d --gpus=all -p 8000:8000 -v voices:/app/voices -v config:/app/config --name openedai-speech ghcr.io/matatonic/openedai-speech
   ```

2. **ROCm (AMD GPU)**
   ```bash
   docker build -f Dockerfile --build-arg USE_ROCM=1 -t ghcr.io/matatonic/openedai-speech-rocm .
   docker run -d --privileged --init --name openedai-speech -p 8000:8000 -v voices:/app/voices -v config:/app/config ghcr.io/matatonic/openedai-speech-rocm
   ```

3. **CPU only**
   ```bash
   docker build -f Dockerfile.min -t ghcr.io/matatonic/openedai-speech-min .
   docker run -d -p 8000:8000 -v voices:/app/voices -v config:/app/config --name openedai-speech ghcr.io/matatonic/openedai-speech-min
   ```

### Configuring Open WebUI to Use openedai-speech for TTS

1. **Open WebUI Settings**
   - Navigate to `Admin Panel > Settings > Audio`.
   - Add the following configuration:
     - API Base URL: `http://host.docker.internal:8000/v1`
     - API Key: Any dummy value (openedai-speech does not require an API key).

2. **Choose a Voice**
   - Under `TTS Voice`, select from the available models:
     - `tts-1` or `tts-1-hd`: alloy, echo, echo-alt, fable, onyx, nova, shimmer.

3. **Save and Apply Changes**
   - Press `Save` to apply the changes.
   - Refresh the page for the changes to take effect.

### Model Details

openedai-speech supports multiple TTS models:

- **Piper TTS**: Fast, runs on CPU, supports multilingual voices.
- **Coqui AI/TTS XTTS v2**: High-quality voices, requires GPU with CUDA.
- **Beta Parler-TTS Support**: Experimental, slower, allows basic voice description.

### Troubleshooting

1. **Verify openedai-speech Service**
   - Ensure the service is running and the port is exposed.

2. **Check Access to host.docker.internal**
   - Verify that `host.docker.internal` is resolvable from within the Open WebUI container.
   - Add a volume to `docker-compose.yml` if necessary.

3. **Review API Key Configuration**
   - Ensure the API key is set to a dummy value.

4. **Check Voice Configuration**
   - Verify that the voice exists in `voice_to_speaker.yaml`.

5. **Verify Voice Model Paths**
   - Double-check paths in `voice_to_speaker.yaml` match actual locations.

### Additional Troubleshooting Tips

- Check openedai-speech logs for errors.
- Verify `docker-compose.yml` configuration.
- Restart the service or Docker environment if issues persist.
- Consult the GitHub repository or community forums for further help.

## Summary
This tutorial provides a comprehensive guide to integrating openedai-speech into Open WebUI using Docker. It covers both Docker Compose and Docker run command methods, TTS configuration in Open WebUI, troubleshooting steps, and model details. By following these steps, you can enhance your Open WebUI setup with high-quality text-to-speech capabilities.

# Tags
#openedai-speech #Docker #TTS #OpenWebUI #integration