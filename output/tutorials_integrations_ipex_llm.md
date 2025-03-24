# Local LLM Setup with IPEX-LLM on Intel GPU

## Key Concepts
- Community contribution tutorial
- Open WebUI customization
- IPEX-LLM library for Intel GPUs
- Setting up Ollama Serve on Intel GPU
- Configuring Open WebUI to connect to Ollama

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/ipex_llm](https://docs.openwebui.com/tutorials/integrations/ipex_llm)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI for specific use cases. It focuses on setting up a local LLM with IPEX-LLM on Intel GPUs.

### Prerequisites
- **Manual Installation of Open WebUI:** This guide is verified using this setup method.
- **IPEX-LLM Library:** A PyTorch library optimized for running LLMs on Intel CPUs and GPUs, ensuring low latency.

### Setting Up Ollama Serve on Intel GPU

1. **Installation and Execution:**
   - Follow the IPEX-LLM official documentation to install and run Ollama Serve accelerated by IPEX-LLM on your Intel GPU.
   - To access Ollama from another machine, set the environment variable `OLLAMA_HOST=0.0.0.0` before running the command:
     ```bash
     OLLAMA_HOST=0.0.0.0 ollama serve
     ```

### Configuring Open WebUI

1. **Accessing Settings:**
   - Navigate to `Settings -> Connections` in the Open WebUI menu.
   - The default Ollama Base URL is set to `https://localhost:11434`.

2. **Verifying Connection:**
   - Click the Refresh button next to the textbox to check the status of the Ollama service connection.
   - If successful, you will see a message stating "Service Connection Verified."
   - If there's an issue, an error message like "WebUI could not connect to Ollama" will be displayed.

3. **Customizing URL:**
   - To use an Ollama server hosted at a different URL, update the Ollama Base URL and press Refresh to reconfirm the connection.

## Summary
This tutorial guides users through setting up Open WebUI with IPEX-LLM accelerated Ollama backend on Intel GPUs. It covers installation steps for Ollama Serve and configuring Open WebUI to connect to the Ollama service, ensuring a smooth experience even on low-cost PCs with integrated GPUs.

# Tags
#tutorial #integration #IPEX-LLM #IntelGPU #OpenWebUI