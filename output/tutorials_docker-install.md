# Installing Docker

## Key Concepts
- Community contribution tutorial
- Docker installation for Windows, Mac, Ubuntu, and other Linux distributions
- Setting up Docker’s apt repository
- Installing and verifying Docker Engine
- Installing and verifying Ollama

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/docker-install](https://docs.openwebui.com/tutorials/docker-install)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI for specific use cases. It is not officially supported by the Open WebUI team.

### Installation Instructions

#### For Windows and Mac Users
1. **Download Docker Desktop**
   - Visit [Docker's official website](https://www.docker.com/products/docker-desktop) to download Docker Desktop.
2. **Installation**
   - Follow the installation instructions provided on the website.
3. **Verification**
   - After installation, open Docker Desktop to ensure it is running properly.

#### For Ubuntu Users
1. **Open Terminal**
   - Open your terminal application.
2. **Set Up Docker’s APT Repository**
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
   - If using an Ubuntu derivative (e.g., Linux Mint), replace `VERSION_CODENAME` with `UBUNTU_CODENAME`.

3. **Install Docker Engine**
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

4. **Verify Installation**
```bash
sudo docker run hello-world
```
   - This command will download a test image and run it in a container, verifying that Docker is installed correctly.

#### For Other Linux Distributions
- Refer to the [official Docker documentation](https://docs.docker.com/engine/install/) for installation instructions specific to your distribution.

### Installing and Verifying Ollama

1. **Download Ollama**
   - Visit [Ollama's website](https://ollama.com/) to download the software.
2. **Verification**
   - Open a browser and navigate to `http://127.0.0.1:11434/`. Note that the port may vary based on your installation.

## Summary
This tutorial provides step-by-step instructions for installing Docker on various operating systems, including Windows, Mac, Ubuntu, and other Linux distributions. It also covers the installation and verification of Ollama, ensuring a smooth setup process for customizing Open WebUI.

# Tags
#docker #installation #tutorial #ubuntu #windows #mac #ollama