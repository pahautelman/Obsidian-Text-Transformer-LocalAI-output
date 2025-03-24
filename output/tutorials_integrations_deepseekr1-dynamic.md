# Run DeepSeek R1 Dynamic 1.58-bit with Llama.cpp

## Key Concepts
- Running DeepSeek-R1 model on personal hardware
- Llama.cpp integration
- Model quantization and optimization
- Open WebUI setup
- Performance considerations

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/deepseekr1-dynamic](https://docs.openwebui.com/tutorials/integrations/deepseekr1-dynamic)

### Overview
This tutorial guides you through running the DeepSeek-R1 Dynamic 1.58-bit quantized model using Llama.cpp integrated with Open WebUI.

### Prerequisites and Setup

#### Hardware Requirements
- **M4 Max + 128GB RAM** (or equivalent)
- **GPU with sufficient VRAM**

#### Software Requirements
- **Llama.cpp**
- **Open WebUI**

### Step-by-Step Guide

#### Step 1: Install Llama.cpp
You can either download the prebuilt binaries or build it from source. Follow the instructions in the [Llama.cpp Build Guide](https://github.com/ggerganov/llama.cpp).

```bash
# Download prebuilt binaries or build from source
```

#### Step 2: Download the Model
Head over to UnslothAI’s Hugging Face page and download the dynamic quantized version of DeepSeek-R1. For this tutorial, we’ll use the 1.58-bit (131GB) version.

```bash
# Install Hugging Face dependencies
pip install huggingface_hub

from huggingface_hub import snapshot_download

snapshot_download(
    repo_id="unsloth/DeepSeek-R1-GGUF",
    local_dir="DeepSeek-R1-GGUF",
    allow_patterns=["*UD-IQ1_S*"]
)
```

#### Step 3: Ensure Open WebUI is Installed and Running
Follow the [Open WebUI documentation](https://docs.openwebui.com) to install and start the application.

#### Step 4: Serve the Model Using Llama.cpp

Navigate to the directory containing the `llama-server` binary:

```bash
cd [path-to-llama-cpp]/llama.cpp/build/bin
```

Start the server with the following command, adjusting parameters as needed:

```bash
./llama-server \
    --model /[your-directory]/DeepSeek-R1-GGUF/DeepSeek-R1-UD-IQ1_S/DeepSeek-R1-UD-IQ1_S-00001-of-00003.gguf \
    --port 10000 \
    --ctx-size 1024 \
    --n-gpu-layers 40
```

#### Step 5: Connect Llama.cpp to Open WebUI

1. Go to **Admin Settings** in Open WebUI.
2. Navigate to **Connections > OpenAI Connections**.
3. Add a new connection with the following details:
   - URL: `http://127.0.0.1:10000/v1` (or `http://host.docker.internal:10000/v1` when running Open WebUI in Docker)
   - API Key: `none`

### Performance Considerations
- **Performance:** Running a 131GB model on personal hardware will be slow. Expect modest inference speeds even with high-end hardware.
- **VRAM/Memory Requirements:** Ensure sufficient VRAM and system RAM for optimal performance.

## Summary
This tutorial walks you through running the DeepSeek-R1 Dynamic 1.58-bit quantized model using Llama.cpp integrated with Open WebUI. By following these steps, you can leverage powerful AI models on personal hardware, thanks to UnslothAI’s optimizations and Llama.cpp’s efficiency.

# Tags
#DeepSeekR1 #Llama.cpp #OpenWebUI #modelquantization #tutorial