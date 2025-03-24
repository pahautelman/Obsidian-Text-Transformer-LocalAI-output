# Server Connectivity Issues

## Key Concepts
- Troubleshooting server connectivity issues
- Configuring Ollama to listen broadly
- Docker connection errors
- SSL connection issues with Hugging Face
- Podman on MacOS

## Detailed Description

**Reference:** [https://docs.openwebui.com/troubleshooting/connection-error](https://docs.openwebui.com/troubleshooting/connection-error)

### Connection to Ollama Server

#### Accessing Ollama from Open WebUI

If you're having trouble connecting to Ollama from Open WebUI, follow these steps:

1. **Configure Ollama to Listen Broadly**
   - Set `OLLAMA_HOST` to `0.0.0.0` to make Ollama listen on all network interfaces.
     ```plaintext
     OLLAMA_HOST=0.0.0.0
     ```
2. **Update Environment Variables**
   - Ensure that the `OLLAMA_HOST` is accurately set within your deployment environment.

3. **Restart Ollama**
   - A restart is needed for the changes to take effect.
4. **Verify Connectivity**
   - After setting up, verify that Ollama is accessible by visiting the WebUI interface.
5. **Refer to Official Documentation**
   - For more detailed instructions on configuring Ollama, please refer to the [Ollama's Official Documentation](https://docs.openwebui.com/troubleshooting/connection-error).

### Docker Connection Error

If you encounter a connection error when trying to access Ollama, it might be due to the WebUI docker container not being able to communicate with the Ollama server running on your host. Here’s how to fix it:

1. **Adjust Network Settings**
   - Use the `--network=host` flag in your Docker command.
     ```plaintext
     --network=host
     ```
2. **Change Port**
   - Remember that the internal port changes from 3000 to 8080.

Example Docker Command:
```bash
docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```
After running the above command, your WebUI should be available at [http://localhost:8080](http://localhost:8080).

### SSL Connection Issue with Hugging Face

If you encounter an SSL error, it could be due to issues with the Hugging Face server. Follow these steps:

1. **Check Hugging Face Server Status**
   - Verify if there's a known outage or issue on their end.
2. **Switch Endpoint**
   - If Hugging Face is down, switch the endpoint in your Docker command.

Example Docker Command for Connection Issues:
```bash
docker run -d -p 3000:8080 -e HF_ENDPOINT=https://hf-mirror.com/ --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

### Podman on MacOS

If you're running on MacOS with Podman, follow these steps to ensure connectivity:

1. **Enable Host Loopback**
   - Use `--network slirp4netns:allow_host_loopback=true` in your command.
     ```plaintext
     --network slirp4netns:allow_host_loopback=true
     ```
2. **Set OLLAMA_BASE_URL**
   - Ensure it points to `http://host.containers.internal:11434`.
     ```plaintext
     http://host.containers.internal:11434
     ```

Example Podman Command:
```bash
podman run -d --network slirp4netns:allow_host_loopback=true -p 3000:8080 -e OLLAMA_BASE_URL=http://host.containers.internal:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

## Summary

This document provides step-by-step instructions for troubleshooting server connectivity issues, including configuring Ollama to listen broadly, resolving Docker connection errors, addressing SSL issues with Hugging Face, and ensuring connectivity when using Podman on MacOS.

# Tags
#troubleshooting #server #connectivity #Ollama #Docker #SSL #Podman