# Open WebUI

## Key Concepts
- Extensible AI platform
- Offline operation
- LLM runners (Ollama, OpenAI-compatible APIs)
- Built-in inference engine for RAG
- Docker installation methods
- Enterprise plan features
- Community support and sponsorship

## Detailed Description

**Reference:** [https://docs.openwebui.com/](https://docs.openwebui.com/)

### Overview
Open WebUI is an extensible, feature-rich, and user-friendly self-hosted AI platform designed to operate entirely offline. It supports various LLM runners like Ollama and OpenAI-compatible APIs, with a built-in inference engine for RAG (Retrieval-Augmented Generation), making it a powerful AI deployment solution.

### Key Features
- **Extensibility:** Easily add new features and functionalities.
- **Offline Operation:** Works entirely offline, ensuring data privacy and security.
- **LLM Support:** Compatible with Ollama and OpenAI-compatible APIs.
- **RAG Inference Engine:** Built-in engine for enhanced retrieval capabilities.

### Installation Methods

#### Quick Start with Docker
Ensure WebSocket support is enabled in your network configuration. Use the following commands to run Open WebUI with Docker:

**Basic Command:**
```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

**With Nvidia GPU Support:**
```bash
docker run -d -p 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda
```

#### Open WebUI Bundled with Ollama
This method uses a single container image that bundles Open WebUI with Ollama, simplifying the setup process.

**With GPU Support:**
```bash
docker run -d -p 3000:8080 --gpus=all -v ollama:/root/.ollama -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama
```

**For CPU Only:**
```bash
docker run -d -p 3000:8080 -v ollama:/root/.ollama -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama
```

### Using the Dev Branch
The `:dev` branch contains the latest unstable features and changes. Use it at your own risk.

**Command:**
```bash
docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:dev
```

### Updating Open WebUI

#### Manual Update
Use Watchtower to update your Docker container manually:
```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --run-once open-webui
```

#### Automatic Updates
Keep your container updated automatically every 5 minutes:
```bash
docker run -d --name watchtower --restart unless-stopped -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --interval 300 open-webui
```

### Manual Installation

#### Using uv (Recommended)
The uv runtime manager ensures seamless Python environment management.

**Installation Commands:**
- **macOS/Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```
- **Windows:**
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Run Open WebUI:**
- **macOS/Linux:**
```bash
DATA_DIR=~/.open-webui uvx --python 3.11 open-webui@latest serve
```
- **Windows:**
```powershell
$env:DATA_DIR="C:\open-webui\data"; uvx --python 3.11 open-webui@latest serve
```

#### Using pip
For users installing Open WebUI with Python's package manager pip, it is strongly recommended to use Python runtime managers like uv or conda.

**Installation Commands:**
```bash
pip install open-webui
```
**Start Open WebUI:**
```bash
open-webui serve
```

**Update Open WebUI:**
```bash
pip install --upgrade open-webui
```

### Enterprise Plan
For enhanced capabilities, including custom theming and branding, SLA support, LTS versions, and more, consider getting an Enterprise Plan. Contact the sales team for details.

### Community Support
Join our vibrant community on Discord for support and to share experiences with fellow users.

### Sponsors
We are grateful for the generous support of our sponsors, whose contributions help maintain and improve the project. Thank you!

## Summary
Open WebUI is a versatile, self-hosted AI platform that supports various LLM runners and offers robust offline capabilities. It provides multiple installation methods, including Docker and manual setups, and offers an enterprise plan for additional features. The community-driven support and sponsorship ensure continuous improvement and sustainability.

# Tags
#openwebui #ai #llm #docker #offline #sponsorship