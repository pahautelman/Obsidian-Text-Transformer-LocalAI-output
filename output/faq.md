# FAQ

## Key Concepts
- Docker usage and benefits
- Customizing logo and branding
- Data privacy and security
- Networking within Docker containers
- Updating Open WebUI
- Managing Docker volumes
- GPU support in Docker
- Speech-to-Text (STT) and Text-to-Speech (TTS)
- HTTPS support
- Troubleshooting common issues

## Detailed Description

**Reference:** [https://docs.openwebui.com/faq](https://docs.openwebui.com/faq)

### Why Docker?

Docker is central to the project's design for several reasons:
- **Consistency**: Ensures that the environment remains consistent across different deployments.
- **Isolation**: Isolates dependencies, reducing compatibility issues.
- **Simplicity**: Simplifies deployment processes.

> **Note:** While Docker might not be everyone’s preference, it is fundamental to the project's operational efficiency. Community-driven alternatives are available for those seeking different deployment methods.

### Customizing Logo and Branding

To customize the logo and branding:
- **Enterprise License**: Required for customization.
- **Contact Sales**: For more details, contact sales@openwebui.com.

### Data Privacy and Security

Sign-up is required to enhance security:
- **Local Storage**: All data remains on your server; nothing is collected by Open WebUI.
- **Privacy Assurance**: Your data stays within your device, ensuring complete control over your information.

### Networking Within Docker Containers

**Connecting to Host Services**:
- Use `host.docker.internal` instead of `localhost` inside the container to connect to host services.

**Making Host Services Accessible**:
- Configure services to listen on all network interfaces using `0.0.0.0` instead of `127.0.0.1`.

### Updating Open WebUI

Updating involves:
1. **Pulling the New Image**: Use `docker pull ghcr.io/open-webui/open-webui:main`.
2. **Removing Old Container**: Without deleting the volume.
3. **Creating a New Container**: With the updated image and existing volume.

> **Important:** This process updates the application while preserving your data.

### Managing Docker Volumes

**Data Preservation**:
- Docker volumes persist data outside of container lifecycles.
- Ensure you do not delete the volume with commands like `docker volume rm`.

### GPU Support in Docker

GPU support varies by platform:
- **Supported**: Docker for Windows and Docker Engine on Linux.
- **Not Supported**: Docker Desktop for Linux and MacOS.

### Speech-to-Text (STT) and Text-to-Speech (TTS)

These services require HTTPS to function correctly due to browser security measures. Ensure your deployment is accessible over HTTPS.

### HTTPS Support

Open WebUI does not include built-in HTTPS support to allow for greater flexibility and customization. Users are encouraged to implement HTTPS termination based on their specific needs.

### Troubleshooting Common Issues

**SSL Errors**:
- Use a HuggingFace mirror like `hf-mirror.com` and specify it in the Docker run command with `-e HF_ENDPOINT=https://hf-mirror.com/`.

**Login Issues**:
- Ensure Docker volumes are correctly mounted to persist data.
- Recover admin account using the Resetting the Admin Password guide if needed.

## Summary
The FAQ covers a range of topics from Docker usage and customization options to troubleshooting common issues. It emphasizes the importance of using Docker for consistency and isolation, provides solutions for networking within containers, and offers guidance on updating Open WebUI while preserving data. Additionally, it addresses concerns about data privacy, GPU support, and HTTPS configuration.

# Tags
#FAQ #Docker #customization #data-privacy #networking #updates #troubleshooting