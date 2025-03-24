# SearXNG

## Key Concepts
- Setting up SearXNG with Open WebUI using Docker
- Configuration steps for SearXNG
  - Cloning repository
  - Modifying .env and docker-compose.yaml files
  - Granting permissions
  - Creating configuration files (limiter.toml, settings.yml)
  - Updating uwsgi.ini file
- Alternative setup methods
- Confirming connectivity
- GUI configuration for web search

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/web-search/searxng](https://docs.openwebui.com/tutorials/web-search/searxng)

### Overview
This tutorial guides you through setting up SearXNG, a free internet metasearch engine, with Open WebUI using Docker. The setup involves several configuration steps to ensure optimal performance and integration.

### Prerequisites
- Ensure you have Docker installed on your system.
- Basic understanding of Docker commands and file configurations.

### Step-by-Step Setup

#### 1. Clone the SearXNG Repository
First, clone the SearXNG Docker repository:
```bash
git clone https://github.com/searxng/searxng-docker.git
```
Navigate to the cloned directory:
```bash
cd searxng-docker
```

#### 2. Modify the .env File
Uncomment and set the `SEARXNG_HOSTNAME` in the `.env` file:
```env
# By default listen on https://localhost
# To change this:
# * uncomment SEARXNG_HOSTNAME, and replace <host> by the SearXNG hostname
# * uncomment LETSENCRYPT_EMAIL, and replace <email> by your email (required to create a Let's Encrypt certificate)
SEARXNG_HOSTNAME=localhost:8080
# LETSENCRYPT_EMAIL=<email>
```
#### 3. Modify the docker-compose.yaml File
Remove the localhost restriction:
```yaml
sed -i "s/127.0.0.1:8080/0.0.0.0:8080/"
```

#### 4. Grant Necessary Permissions
Allow the container to create new config files:
```bash
sudo chmod a+rwx searxng-docker/searxng
```

#### 5. Create a Non-Restrictive limiter.toml File
Create a non-restrictive `limiter.toml` file:
```toml
[botdetection.ip_limit]
link_token = false

[botdetection.ip_lists]
block_ip = []
pass_ip = []
```

#### 6. Remove the Default settings.yml File
Delete the default `settings.yml` file if it exists:
```bash
rm searxng-docker/searxng/settings.yml
```

#### 7. Create a Fresh settings.yml File
On the first run, remove `cap_drop: - ALL` from the docker-compose.yaml file for the searxng service to create `/etc/searxng/uwsgi.ini`. After the first run, re-add `cap_drop: - ALL` for security:
```yaml
docker compose up -d ; sleep 10 ; docker compose down
```

#### 8. Add Formats and Update Port Number
Add HTML and JSON formats to the `settings.yml` file:
```bash
sed -i 's/formats: \[\"html\"\/]/formats: [\"html\", \"json\"]/' searxng-docker/searxng/settings.yml
```
Generate a secret key for your SearXNG instance:
```bash
sed -i "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng-docker/searxng/settings.yml
```
For Windows users, use the following PowerShell script to generate the secret key:
```powershell
$randomBytes = New-Object byte[] 32
(New-Object Security.Cryptography.RNGCryptoServiceProvider).GetBytes($randomBytes)
$secretKey = -join ($randomBytes | ForEach-Object { "{0:x2}" -f $_ })
(Get-Content searxng-docker/searxng/settings.yml) -replace 'ultrasecretkey', $secretKey | Set-Content searxng-docker/searxng/settings.yml
```
Update the port number in the server section to match the one you set earlier (in this case, 8080):
```bash
sed -i 's/port: 8080/port: 8080/' searxng-docker/searxng/settings.yml
```
Change the `bind_address` as desired:
```bash
sed -i 's/bind_address: "0.0.0.0"/bind_address: "127.0.0.1"/' searxng-docker/searxng/settings.yml
```

#### 9. Update uwsgi.ini File
Ensure your `uwsgi.ini` file matches the following:
```ini
[uwsgi]
# Who will run the code
uid = searxng
gid = searxng

# Number of workers (usually CPU count)
workers = %k

# Number of threads per worker
threads = 4

# The right granted on the created socket
chmod-socket = 666

# Plugin to use and interpreter config
single-interpreter = true
master = true
plugin = python3
lazy-apps = true
enable-threads = 4

# Module to import
module = searx.webapp

# Virtualenv and python path
pythonpath = /usr/local/searxng
chdir = /usr/local/searxng/searx

# automatically set processes name to something meaningful
auto-procname = true

# Disable request logging for privacy
disable-logging = true
log-5xx = true

# Set the max size of a request (request-body excluded)
buffer-size = 8192

# No keep alive
add-header = Connection: close

# uwsgi serves the static files
static-map = /static=/usr/local/searxng/searx/static
static-expires = /* 86400
static-gzip-all = True
offload-threads = 4
```

### Alternative Setup
If you prefer not to modify the default configuration, create an empty `searxng-docker` folder and follow the rest of the setup instructions.

### Docker Compose Setup
Add the following environment variables to your Open WebUI docker-compose.yaml file:
```yaml
services:
  open-webui:
    environment:
      ENABLE_RAG_WEB_SEARCH: True
      RAG_WEB_SEARCH_ENGINE: "searxng"
      RAG_WEB_SEARCH_RESULT_COUNT: 3
      RAG_WEB_SEARCH_CONCURRENT_REQUESTS: 10
      SEARXNG_QUERY_URL: "http://searxng:8080/search?q=<query>"
```
Create a `.env` file for SearXNG:
```env
# SearXNG
SEARXNG_HOSTNAME=localhost:8080/
```
Add the following to SearXNG's docker-compose.yaml file:
```yaml
services:
  searxng:
    container_name: searxng
    image: searxng/searxng:latest
    ports:
      - "8080:8080"
    volumes:
      - ./searxng:/etc/searxng:rw
    env_file:
      - .env
    restart: unless-stopped
    cap_drop:
      - ALL
    cap_add:
      - CHOWN
      - SETGID
      - SETUID
      - DAC_OVERRIDE
    logging:
      driver: "json-file"
      options:
        max-size: "1m"
        max-file: "1"
```
Launch your stack with:
```bash
docker compose up -d
```

### Confirm Connectivity
Confirm connectivity to SearXNG from your Open WebUI container instance:
```bash
docker exec -it open-webui curl http://host.docker.internal:8080/search?q=this+is+a+test+query&format=json
```

### GUI Configuration
Navigate to the Admin Panel -> Settings -> Web Search and configure as follows:

- Toggle **Enable Web Search**.
- Set **Web Search Engine** to `searxng`.
- Set **SearXNG Query URL** to one of the following examples:
  - `http://searxng:8080/search?q=<query>` (using the container name and exposed port, suitable for Docker-based setups)
  - `http://host.docker.internal:8080/search?q=<query>` (using the host.docker.internal DNS name and the host port, suitable for Docker-based setups)
  - `http://<searxng.local>/search?q=<query>` (using a local domain name, suitable for local network access)
  - `https://<search.domain.com>/search?q=<query>` (using a custom domain name for a self-hosted SearXNG instance, suitable for public or private access)

### Using Web Search in a Chat
To access Web Search, click on the **+** next to the message input field. Here you can toggle Web Search On/Off.

## Summary
This tutorial provides a comprehensive guide to setting up SearXNG with Open WebUI using Docker. By following these steps, you can integrate SearXNG's metasearch capabilities into your Open WebUI environment, enabling powerful web search functionalities.

# Tags
#searxng #docker #openwebui #websearch #tutorial