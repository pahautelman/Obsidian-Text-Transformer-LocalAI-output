# Redis Websocket Support

## Key Concepts
- Community contribution tutorial
- Integrating Redis with Open WebUI
- Prerequisites (Open WebUI instance, Redis container, Docker Compose)
- Setting up Redis for websocket support
- Configuring Open WebUI for websockets
- Verification and troubleshooting steps

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/redis](https://docs.openwebui.com/tutorials/integrations/redis)

### Overview
This tutorial, contributed by the community, demonstrates how to integrate Redis with Open WebUI for websocket support. This integration enables real-time communication and updates between clients and your application.

### Prerequisites

Before starting, ensure you have the following:
- A valid **Open WebUI instance** (version 1.0 or higher)
- A **Redis container** (using `docker.io/valkey/valkey:8.0.1-alpine` based on Redis 7.x)
- **Docker Compose** (version 2.0 or higher) installed
- A **Docker network** for communication between Open WebUI and Redis
- Basic understanding of Docker, Redis, and Open WebUI

### Setting Up Redis

To set up Redis for websocket support, create a `docker-compose.yml` file with the following configuration:

```yaml
version: '3.9'
services:
  redis:
    image: docker.io/valkey/valkey:8.0.1-alpine
    container_name: redis-valkey
    volumes:
      - redis-data:/data
    command: "valkey-server --save 30 1"
    healthcheck:
      test: "[ $$(valkey-cli ping) = 'PONG' ]"
      start_period: 5s
      interval: 1s
      timeout: 3s
      retries: 5
    restart: unless-stopped
    cap_drop:
      - ALL
    cap_add:
      - SETGID
      - SETUID
      - DAC_OVERRIDE
    logging:
      driver: "json-file"
      options:
        max-size: "1m"
        max-file: "1"
    networks:
      - openwebui-network

volumes:
  redis-data:

networks:
  openwebui-network:
    external: true
```

This configuration sets up a Redis container named `redis-valkey` with data persistence and health checks. To create the Docker network, run:

```sh
docker network create openwebui-network
```

### Configuring Open WebUI

To enable websocket support in Open WebUI, set the following environment variables for your Open WebUI instance:

```sh
ENABLE_WEBSOCKET_SUPPORT="true"
WEBSOCKET_MANAGER="redis"
WEBSOCKET_REDIS_URL="redis://redis:6379/1"
```

When running Open WebUI using Docker, connect it to the same Docker network:

```sh
docker run -d \
  --name open-webui \
  --network openwebui-network \
  -v open-webui:/app/backend/data \
  -e ENABLE_WEBSOCKET_SUPPORT="true" \
  -e WEBSOCKET_MANAGER="redis" \
  -e WEBSOCKET_REDIS_URL="redis://127.0.0.1:6379/1" \
  ghcr.io/open-webui/open-webui:main
```

Replace `127.0.0.1` with the actual IP address of your Redis container in the Docker network.

### Verification

After setting up, you should see the following log message when starting Open WebUI:

```
DEBUG:open_webui.socket.main:Using Redis to manage websockets.
```

To verify that the Redis instance is running and accepting connections, use:

```sh
docker exec -it redis-valkey redis-cli -p 6379 ping
```

This command should output `PONG`. If it fails, try:

```sh
docker exec -it redis-valkey valkey-cli -p 6379 ping
```

### Troubleshooting

If you encounter issues, refer to the following resources:
- [Redis Documentation](https://redis.io/documentation)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [sysctl Documentation](https://man7.org/linux/man-pages/man8/sysctl.8.html)

## Summary
This tutorial guides you through integrating Redis with Open WebUI for websocket support, enabling real-time communication and updates between clients and your application.

# Tags
#redis #websocket #openwebui #docker #tutorial