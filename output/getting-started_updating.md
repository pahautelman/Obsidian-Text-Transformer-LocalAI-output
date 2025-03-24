# Updating Open WebUI

## Key Concepts
- Manual update process for Docker containers
- Using Watchtower for automated updates
- Persistent data in Docker volumes
- Setting environment variables (WEBUI_SECRET_KEY)

## Detailed Description

**Reference:** [https://docs.openwebui.com/getting-started/updating](https://docs.openwebui.com/getting-started/updating)

### Manual Update Process

To update your local Docker installation of Open WebUI to the latest version, follow these steps:

1. **Stop and Remove Current Container**
   - Stop the running container and remove it without deleting the data stored in the Docker volume.
     ```bash
     docker rm -f open-webui
     ```

2. **Pull Latest Docker Image**
   - Update the Docker image to the latest version.
     ```bash
     docker pull ghcr.io/open-webui/open-webui:main
     ```

3. **Remove Existing Data (Optional)**
   - Remove existing data in the Docker volume if you want a clean slate. This step is not recommended unless necessary, as it will delete all chat histories and other data.
     ```bash
     docker volume rm open-webui
     ```

4. **Start Container with Updated Image**
   - Start the container again with the updated image and existing volume attached. For Nvidia GPU support, add `--gpus all` to the Docker run command.
     ```bash
     docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
     ```

### Persistent Data in Docker Volumes

Data is stored in a Docker volume named `open-webui`. The path to the volume is not directly accessible, but you can inspect it with:
```bash
docker volume inspect open-webui
```
This command will show details of the volume, including the mountpoint.

- **On Windows 10 + WSL 2:**
  - Docker volumes are located at `\\wsl$\docker-desktop\mnt\docker-desktop-disk\data\docker\volumes`.

### Automatically Updating Open WebUI with Watchtower

Watchtower can automate the update process for Open WebUI. Here are three options:

1. **One-time Update**
   - Run Watchtower as a one-time update to stop the current container, pull the latest image, and start a new container.
     ```bash
     docker run --rm --volume /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --run-once open-webui
     ```

2. **Running Watchtower as a Separate Container**
   - Run Watchtower as a separate container to watch and update your Open WebUI container.
     ```bash
     docker run -d --name watchtower \
       --volume /var/run/docker.sock:/var/run/docker.sock \
       containrrr/watchtower -i 300 open-webui
     ```
   This will start Watchtower in detached mode, watching your Open WebUI container for updates every 5 minutes.

3. **Integrating Watchtower with a docker-compose.yml File**
   - Integrate Watchtower with your `docker-compose.yml` file to automate updates.
     ```yaml
     version: '3'
     services:
       open-webui:
         image: ghcr.io/open-webui/open-webui:main
         ports:
           - "3000:8080"
         volumes:
           - open-webui:/app/backend/data
       watchtower:
         image: containrrr/watchtower
         volumes:
           - /var/run/docker.sock:/var/run/docker.sock
         command: --interval 300 open-webui
         depends_on:
           - open-webui
     volumes:
       open-webui:
     ```

### Setting Environment Variables

To ensure consistent authentication sessions after updates, set the `WEBUI_SECRET_KEY` environment variable.

- **Docker Run Command:**
  ```bash
  docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui -e WEBUI_SECRET_KEY=your_secret_key ghcr.io/open-webui/open-webui:main
  ```

- **docker-compose.yml:**
  ```yaml
  version: '3'
  services:
    open-webui:
      image: ghcr.io/open-webui/open-webui:main
      ports:
        - "3000:8080"
      volumes:
        - open-webui:/app/backend/data
      environment:
        - WEBUI_SECRET_KEY=your_secret_key
  volumes:
    open-webui:
  ```

## Summary

Updating Open WebUI involves either a manual process or using Watchtower for automated updates. The manual update includes stopping and removing the current container, pulling the latest Docker image, optionally removing existing data, and starting the container again. Watchtower can automate this process with options for one-time updates, running as a separate container, or integrating with `docker-compose.yml`. Persistent data is stored in Docker volumes, and setting the `WEBUI_SECRET_KEY` environment variable ensures consistent authentication sessions.

# Tags
#updating #Docker #Watchtower #OpenWebUI #environment variables