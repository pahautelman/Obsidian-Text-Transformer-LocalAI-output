# Development Guide

## Key Concepts
- System requirements (OS, Python, Node.js)
- Local development setup
  - Cloning the repository
  - Frontend setup
  - Backend setup
- Troubleshooting common issues
  - Memory errors
  - Port conflicts
  - Hot reload problems
- Contributing to Open WebUI

## Detailed Description

**Reference:** [https://docs.openwebui.com/getting-started/advanced-topics/development](https://docs.openwebui.com/getting-started/advanced-topics/development)

### System Requirements
Before setting up your development environment, ensure you meet the following requirements:

- **Operating System:**
  - Linux (or WSL on Windows)
  - macOS

- **Python Version:** Python 3.11+

- **Node.js Version:** Node.js 22.10+

### Local Development Setup
Follow these steps to set up your local development environment for both frontend and backend components.

#### Cloning the Repository
```bash
git clone https://github.com/open-webui/open-webui.git
cd open-webui
```

#### Frontend Setup

1. **Create a .env file:**
   ```bash
   cp -RPp .env.example .env
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start the frontend server:**
   ```bash
   npm run dev
   ```
   The frontend will be available at [http://localhost:5173](http://localhost:5173).

#### Backend Setup

1. **Navigate to the backend directory:**
   ```bash
   cd backend
   ```

2. **Use Conda for environment setup:**
   ```bash
   conda create --name open-webui python=3.11
   conda activate open-webui
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt -U
   ```

4. **Start the backend server:**
   ```bash
   sh dev.sh
   ```
   The API documentation will be available at [http://localhost:8080/docs](http://localhost:8080/docs).

### Troubleshooting Common Issues

#### FATAL ERROR: Reached Heap Limit
If you encounter memory-related errors during the build, increase the Node.js heap size:

1. **Modify Dockerfile:**
   ```Dockerfile
   ENV NODE_OPTIONS=--max-old-space-size=4096
   ```

2. **Allocate at least 4 GB of RAM to Node.js.**

#### Other Issues

- **Port Conflicts:** Ensure that no other processes are using ports 8080 or 5173.
- **Hot Reload Not Working:** Verify that watch mode is enabled for both frontend and backend.

### Contributing to Open WebUI
Follow these best practices when contributing to the project:

- **Commit Changes Regularly** to track your progress.
- **Sync with the Main Branch** to avoid conflicts:
  ```bash
  git pull origin main
  ```
- **Run Tests Before Pushing:**
  ```bash
  npm run test
  ```

## Summary

This guide provides a comprehensive setup for local development of Open WebUI, covering system requirements, local development steps for both frontend and backend, troubleshooting common issues, and best practices for contributing to the project.

# Tags
#development #local-setup #troubleshooting #contributing