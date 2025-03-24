# Open WebUI Logging

## Key Concepts
- Browser client logging
- Application server/Backend logging
- Logging levels (CRITICAL, ERROR, WARNING, INFO, DEBUG, NOTSET)
- Global log level configuration
- Environment variables for logging control
- Docker and Docker Compose logging setup

## Detailed Description

**Reference:** [https://docs.openwebui.com/getting-started/advanced-topics/logging](https://docs.openwebui.com/getting-started/advanced-topics/logging)

### Browser Client Logging
Client-side logging is typically handled through JavaScript's `console.log()` method and can be accessed using the developer tools built into modern browsers. Here are some examples of how to access these logs in different browsers:

| Browser Engine | Browsers |
| --- | --- |
| Blink | Chrome, Chromium Edge |
| Gecko | Firefox |
| WebKit | Safari |

### Application Server/Backend Logging
Logging on the server side is a work-in-progress but can be controlled using environment variables. Python's `log()` and `print()` statements send information to the console, with the default logging level set to INFO.

- **Sensitive Data:** Ensure that sensitive data is only exposed at the DEBUG level to maintain security.
- **Logging Levels:**
  - CRITICAL
  - ERROR
  - WARNING
  - INFO
  - DEBUG
  - NOTSET

### Global Log Level Configuration
The default global log level is set to INFO but can be overridden using the `GLOBAL_LOG_LEVEL` environment variable. This variable configures all attached loggers by executing a `basicConfig` statement with the `force` argument set to True within `config.py`.

- **Force Argument:** When set to true, this removes and closes any existing handlers attached to the root logger before reconfiguring.
- **Stream:** Uses standard output (`sys.stdout`).

#### Example: Setting DEBUG Logging Level in Docker
To set the logging level to DEBUG in a Docker environment, use the following command:

```bash
--env GLOBAL_LOG_LEVEL="DEBUG"
```

For Docker Compose, add this to the `environment` section of your `docker-compose.yml` file:

```yaml
environment:
  - GLOBAL_LOG_LEVEL=DEBUG
```

### App/Backend Logging Granularity
Granular control over logging can be achieved using specific environment variables. Note that the `basicConfig force` argument is not currently used, so these settings may only affect Open-WebUI logging and not third-party modules.

| Variable | Description |
| --- | --- |
| AUDIO_LOG_LEVEL |  |
| COMFYUI_LOG_LEVEL |  |
| CONFIG_LOG_LEVEL |  |
| DB_LOG_LEVEL |  |
| IMAGES_LOG_LEVEL |  |
| MAIN_LOG_LEVEL |  |
| MODELS_LOG_LEVEL |  |
| OLLAMA_LOG_LEVEL |  |
| OPENAI_LOG_LEVEL |  |
| RAG_LOG_LEVEL |  |
| WEBHOOK_LOG_LEVEL |  |

## Summary
Open WebUI Logging provides comprehensive logging capabilities for both client and server sides. By configuring environment variables, users can control the verbosity and scope of logs, ensuring effective monitoring and debugging.

# Tags
#logging #browser #backend #Docker #debugging