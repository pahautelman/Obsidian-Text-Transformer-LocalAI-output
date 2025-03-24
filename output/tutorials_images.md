# Image Generation

## Key Concepts
- Community contributions
- Open WebUI customization
- AUTOMATIC1111 backend
- ComfyUI backend
- OpenAI DALL·E backend
- SwarmUI integration
- Image generation workflow

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/images](https://docs.openwebui.com/tutorials/images)

### Overview
This tutorial is a community contribution and demonstrates how to customize Open WebUI for specific use cases. It covers setting up image generation using three backends: AUTOMATIC1111, ComfyUI, and OpenAI DALL·E.

### AUTOMATIC1111

#### Initial Setup
1. **Install AUTOMATIC1111:**
   - Ensure AUTOMATIC1111 is installed on your system.
2. **Launch with API Access:**
   ```bash
   ./webui.sh --api --listen
   ```
3. **Docker Installation:**
   ```bash
   docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -e AUTOMATIC1111_BASE_URL=http://host.docker.internal:7860/ -e ENABLE_IMAGE_GENERATION=True -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
   ```

#### Setting Up Open WebUI with AUTOMATIC1111
1. **Navigate to Admin Panel:**
   - Go to `Admin Panel > Settings > Images`.
2. **Configure Settings:**
   - Set `Image Generation Engine` to `Default (Automatic1111)`.
   - Enter the API URL: `http://<your_automatic1111_address>:7860/`.

### ComfyUI

#### Initial Setup
1. **Download and Extract:**
   - Download ComfyUI from GitHub and extract it to your desired directory.
2. **Launch ComfyUI:**
   ```bash
   python main.py
   ```
3. **Low VRAM Systems:**
   ```bash
   python main.py --lowvram
   ```
4. **Docker Installation:**
   ```bash
   docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -e COMFYUI_BASE_URL=http://host.docker.internal:7860/ -e ENABLE_IMAGE_GENERATION=True -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
   ```

#### Setting Up Open WebUI with ComfyUI

##### Model Checkpoints
- Download FLUX.1-schnell or FLUX.1-dev from HuggingFace.
- Place the model checkpoints in both `models/checkpoints` and `models/unet` directories.

##### VAE, CLIP, T5XXL Models
- **VAE:**
  - Download `ae.safetensors`.
  - Place it in the `models/vae` directory.
- **CLIP:**
  - Download `clip_l.safetensors`.
  - Place it in the `models/clip` directory.
- **T5XXL:**
  - Download `t5xxl_fp16.safetensors` or `t5xxl_fp8_e4m3fn.safetensors`.
  - Place it in the `models/clip` directory.

##### Configuration Steps
1. **Configure Open WebUI Settings:**
   - Navigate to `Admin Panel > Settings > Images`.
   - Set `Image Generation Engine` to `ComfyUI`.
   - Enter the API URL: `http://<your_comfyui_address>:8188/`.

2. **Verify Connection and Enable Image Generation:**
   - Ensure ComfyUI is running.
   - Toggle on `Image Generation (Experimental)`.

3. **Configure ComfyUI Settings and Import Workflow:**
   - Enable developer mode in ComfyUI.
   - Export the workflow in API format.
   - Import the workflow into Open WebUI.
   - Map ComfyUI Workflow Nodes and set the default model.

### SwarmUI Integration
- Append `ComfyBackendDirect` to the ComfyUI Base URL.
- Set up SwarmUI with LAN access.
- Follow the same configuration steps as outlined for ComfyUI.

### OpenAI DALL·E

#### Initial Setup
1. **Obtain API Key:**
   - Get an API key from OpenAI.

#### Configuring Open WebUI
1. **Navigate to Admin Panel:**
   - Go to `Admin Panel > Settings > Images`.
2. **Configure Settings:**
   - Set `Image Generation Engine` to `Open AI (Dall-E)`.
   - Enter your OpenAI API key.
   - Choose the DALL·E model (DALL·E 2 or DALL·E 3).

### Using Image Generation
1. **Generate Prompt:**
   - Use a text generation model to create an image prompt.
2. **Generate Image:**
   - Click the Picture icon to generate the image.
3. **View Result:**
   - The generated image will be returned automatically in chat.

## Summary
This tutorial guides users through setting up and using image generation features in Open WebUI with three different backends: AUTOMATIC1111, ComfyUI, and OpenAI DALL·E. It includes detailed steps for installation, configuration, and integration, ensuring a seamless experience for generating images.

# Tags
#imagegeneration #openwebui #automatic1111 #comfyui #dalle