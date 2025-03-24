# Quick Start

## Key Concepts
- Admin creation and user registrations
- Privacy and data security
- Installation methods (Docker, Python, Kubernetes)
- Docker Compose and Podman
- Docker Swarm setup
- uv runtime manager
- Conda and venv environments
- Helm and Kustomize for Kubernetes

## Detailed Description

**Reference:** [https://docs.openwebui.com/getting-started/quick-start/](https://docs.openwebui.com/getting-started/quick-start/)

### Admin Creation and User Registrations

#### Admin Privileges
The first account created on Open WebUI gains Administrator privileges. This account controls user management and system settings.

#### User Registration Process
Subsequent sign-ups start with a **Pending** status, requiring Administrator approval for access.

### Privacy and Data Security

All data, including login details, is locally stored on your device. Open WebUI ensures strict confidentiality and no external requests for enhanced privacy and security. All models are private by default and must be explicitly shared via groups or made public.

- **Private Models:** Only accessible to the owner.
- **Group Shared Models:** Accessible to members of the specified group.
- **Public Models:** Accessible to anyone on the instance.

### Installation Methods

Choose your preferred installation method below:

#### Docker
Docker is officially supported and recommended for most users. It provides a straightforward way to run Open WebUI in a containerized environment.

##### Quick Start with Docker 🐳

1. **Pull the Open WebUI Image**
   ```sh
   docker pull ghcr.io/open-webui/open-webui:main
   ```

2. **Run the Container**
   ```sh
   docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
   ```
   - **Volume Mapping** (-v open-webui:/app/backend/data): Ensures persistent storage of your data.
   - **Port Mapping** (-p 3000:8080): Exposes the WebUI on port 3000 of your local machine.

##### Using GPU Support
For Nvidia GPU support, add `--gpus all` to the docker run command:
```sh
docker run -d -p 3000:8080 --gpus all -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:cuda
```

##### Single-User Mode (Disabling Login)
To bypass the login page for a single-user setup, set the `WEBUI_AUTH` environment variable to `False`:
```sh
docker run -d -p 3000:8080 -e WEBUI_AUTH=False -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
```

##### Advanced Configuration: Connecting to Ollama on a Different Server
To connect Open WebUI to an Ollama server located on another host, add the `OLLAMA_BASE_URL` environment variable:
```sh
docker run -d -p 3000:8080 -e OLLAMA_BASE_URL=https://example.com -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

##### Access the WebUI
After the container is running, access Open WebUI at:
```
http://localhost:3000
```

For detailed help on each Docker flag, see Docker's documentation.

##### Updating
To update your local Docker installation to the latest version, you can either use Watchtower or manually update the container.

**Option 1: Using Watchtower**
```sh
docker run --rm --volume /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --run-once open-webui
```

**Option 2: Manual Update**
1. Stop and remove the current container:
   ```sh
   docker rm -f open-webui
   ```
2. Pull the latest version:
   ```sh
   docker pull ghcr.io/open-webui/open-webui:main
   ```
3. Start the container again:
   ```sh
   docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
   ```

#### Docker Compose

Using Docker Compose simplifies the management of multi-container Docker applications.

**Example docker-compose.yml**
```yaml
version: '3'
services:
  openwebui:
    image: ghcr.io/open-webui/open-webui:main
    ports:
      - "3000:8080"
    volumes:
      - open-webui:/app/backend/data
volumes:
  open-webui:
```

**Starting the Services**
```sh
docker compose up -d
```

**Helper Script**
A useful helper script called `run-compose.sh` is included with the codebase. This script assists in choosing which Docker Compose files to include in your deployment, streamlining the setup process.

For Nvidia GPU support, change the image from `ghcr.io/open-webui/open-webui:main` to `ghcr.io/open-webui/open-webui:cuda` and add the following to your service definition in the `docker-compose.yml` file:
```yaml
deploy:
  resources:
    reservations:
      devices:
        - driver: nvidia
          count: all
          capabilities: [gpu]
```

#### Podman

Podman is a daemonless container engine for developing, managing, and running OCI Containers.

**Basic Commands**
- **Run a Container:**
  ```sh
  podman run -d --name openwebui -p 3000:8080 ghcr.io/open-webui/open-webui:main
  ```
- **List Running Containers:**
  ```sh
  podman ps
  ```

**Networking with Podman**
If networking issues arise, you may need to adjust your network settings:
```sh
--network=slirp4netns:allow_host_loopback=true
```

Refer to the Podman documentation for advanced configurations.

#### Docker Swarm

This installation method requires knowledge of Docker Swarms, as it utilizes a stack file to deploy 3 separate containers as services in a Docker Swarm. It includes isolated containers of ChromaDB, Ollama, and OpenWebUI. Additionally, there are pre-filled Environment Variables to further illustrate the setup.

**Choose the appropriate command based on your hardware setup:**

**Before Starting:**
Directories for your volumes need to be created on the host, or you can specify a custom location or volume. The current example utilizes an isolated dir `data`, which is within the same dir as the `docker-stack.yaml`.
```sh
mkdir -p data/open-webui data/chromadb data/ollama
```

**With GPU Support:**
```yaml
version: '3.9'
services:
  openWebUI:
    image: ghcr.io/open-webui/open-webui:main
    depends_on:
      - chromadb
      - ollama
    volumes:
      - ./data/open-webui:/app/backend/data
    environment:
      DATA_DIR: /app/backend/data
      OLLAMA_BASE_URLS: http://ollama:11434
      CHROMA_HTTP_PORT: 8000
      CHROMA_HTTP_HOST: chromadb
      CHROMA_TENANT: default_tenant
      VECTOR_DB: chroma
      WEBUI_NAME: Awesome ChatBot
      CORS_ALLOW_ORIGIN: "*"
      RAG_EMBEDDING_ENGINE: ollama
      RAG_EMBEDDING_MODEL: nomic-embed-text-v1.5
      RAG_EMBEDDING_MODEL_TRUST_REMOTE_CODE: "True"
    ports:
      - target: 8080
        published: 8080
        mode: overlay
    deploy:
      replicas: 1
      restart_policy:
        condition: any
        delay: 5s
        max_attempts: 3

  chromadb:
    hostname: chromadb
    image: chromadb/chroma:0.5.15
    volumes:
      - ./data/chromadb:/chroma/chroma
    environment:
      - IS_PERSISTENT=TRUE
      - ALLOW_RESET=TRUE
      - PERSIST_DIRECTORY=/chroma/chroma
    ports:
      - target: 8000
        published: 8000
        mode: overlay
    deploy:
      replicas: 1
      restart_policy:
        condition: any
        delay: 5s
        max_attempts: 3
    healthcheck:
      test: ["CMD-SHELL", "curl localhost:8000/api/v1/heartbeat || exit 1"]
      interval: 10s
      retries: 2
      start_period: 5s
      timeout: 10s

  ollama:
    image: ollama/ollama:latest
    hostname: ollama
    ports:
      - target: 11434
        published: 11434
        mode: overlay
    deploy:
      resources:
        reservations:
          generic_resources:
            - discrete_resource_spec:
                kind: "NVIDIA-GPU"
                value: 0
      replicas: 1
      restart_policy:
        condition: any
        delay: 5s
        max_attempts: 3
    volumes:
      - ./data/ollama:/root/.ollama

**Additional Requirements:**
- Ensure CUDA is Enabled, follow your OS and GPU instructions for that.
- Enable Docker GPU support, see Nvidia Container Toolkit.
- Follow the Guide here on configuring Docker Swarm to work with your GPU.
- Ensure GPU Resource is enabled in `/etc/nvidia-container-runtime/config.toml` and enable GPU resource advertising by uncommenting `swarm-resource = "DOCKER_RESOURCE_GPU"`.
- The docker daemon must be restarted after updating these files on each node.

**With CPU Support:**
Modify the Ollama Service within `docker-stack.yaml` and remove the lines for `generic_resources`:

```yaml
ollama:
  image: ollama/ollama:latest
  hostname: ollama
  ports:
    - target: 11434
      published: 11434
      mode: overlay
  deploy:
    replicas: 1
    restart_policy:
      condition: any
      delay: 5s
      max_attempts: 3
  volumes:
    - ./data/ollama:/root/.ollama
```

**Deploy Docker Stack:**
```sh
docker stack deploy -c docker-stack.yaml -d super-awesome-ai
```

#### uv Runtime Manager

The `uv` runtime manager ensures seamless Python environment management for applications like Open WebUI.

1. **Install uv**
   - macOS/Linux:
     ```sh
     curl -LsSf https://astral.sh/uv/install.sh | sh
     ```
   - Windows:
     ```sh
     powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
     ```

2. **Run Open WebUI**
   Once `uv` is installed, running Open WebUI is a breeze. Use the command below, ensuring to set the `DATA_DIR` environment variable to avoid data loss.
   - macOS/Linux:
     ```sh
     DATA_DIR=~/.open-webui uvx --python 3.11 open-webui@latest serve
     ```
   - Windows:
     ```sh
     $env:DATA_DIR="C:\open-webui\data"; uvx --python 3.11 open-webui@latest serve
     ```

#### Conda and venv Environments

**Conda Environment**
1. Create a Conda Environment:
   ```sh
   conda create -n open-webui python=3.11
   ```
2. Activate the Environment:
   ```sh
   conda activate open-webui
   ```
3. Install Open WebUI:
   ```sh
   pip install open-webui
   ```
4. Start the Server:
   ```sh
   open-webui serve
   ```

**venv Environment**
1. Create a Virtual Environment:
   ```sh
   python3 -m venv venv
   ```
2. Activate the Virtual Environment:
   - On Linux/macOS:
     ```sh
     source venv/bin/activate
     ```
   - On Windows:
     ```sh
     venv\Scripts\activate
     ```
3. Install Open WebUI:
   ```sh
   pip install open-webui
   ```
4. Start the Server:
   ```sh
   open-webui serve
   ```

#### Helm and Kustomize for Kubernetes

**Helm**
1. Add Open WebUI Helm Repository:
   ```sh
   helm repo add open-webui https://open-webui.github.io/helm-charts
   helm repo update
   ```
2. Install Open WebUI Chart:
   ```sh
   helm install openwebui open-webui/open-webui
   ```
3. Verify Installation:
   ```sh
   kubectl get pods
   ```

**Kustomize**
1. Clone the Open WebUI Manifests:
   ```sh
   git clone https://github.com/open-webui/k8s-manifests.git
   cd k8s-manifests
   ```
2. Apply the Manifests:
   ```sh
   kubectl apply -k .
   ```
3. Verify Installation:
   ```sh
   kubectl get pods
   ```

**Access the WebUI**
Set up port forwarding or load balancing to access Open WebUI from outside the cluster.

#### Pinokio.computer

For installation via Pinokio.computer, please visit their website:
```
https://pinokio.computer/
```

Support for this installation method is provided through their website.

## Summary
This guide provides a comprehensive overview of installing and running Open WebUI using various methods. Whether you prefer Docker, Python, Kubernetes, or other environments, the steps are clearly outlined to ensure a smooth setup process. For developers, additional resources and community support are available to help with contributions and troubleshooting.

# Tags
#quickstart #installation #docker #python #kubernetes #uv #conda #venv #helm #kustomize