# LibreTranslate Integration

## Key Concepts
- LibreTranslate overview
- Setting up LibreTranslate in Docker
  - Creating a docker-compose file
  - Creating a stack.env file
  - Running the Docker Compose file
- Configuring the integration in Open WebUI
  - Available integrations
  - Supported languages
- Troubleshooting tips
- Benefits of integration

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/libre-translate](https://docs.openwebui.com/tutorials/integrations/libre-translate)

### Overview
LibreTranslate is a free and open-source machine translation API that supports multiple languages. Unlike proprietary services, LibreTranslate relies on the open-source Argos Translate library for its translation engine.

### Setting up LibreTranslate in Docker

#### Step 1: Create a Docker Compose File
Create a new file named `docker-compose.yml` with the following configuration:

```yaml
services:
  libretranslate:
    container_name: libretranslate
    image: libretranslate/libretranslate:v1.6.0
    restart: unless-stopped
    ports:
      - "5000:5000"
    env_file:
      - stack.env
    volumes:
      - libretranslate_api_keys:/app/db
      - libretranslate_models:/home/libretranslate/.local:rw
    tty: true
    stdin_open: true
    healthcheck:
      test: ['CMD-SHELL', './venv/bin/python scripts/healthcheck.py']
volumes:
  libretranslate_models:
  libretranslate_api_keys:
```

#### Step 2: Create a stack.env File
Create a new file named `stack.env` in the same directory with the following configuration:

```env
LT_DEBUG="false"
LT_UPDATE_MODELS="true"
LT_SSL="false"
LT_SUGGESTIONS="false"
LT_METRICS="false"
LT_HOST="0.0.0.0"
LT_API_KEYS="false"
LT_THREADS="12"
LT_FRONTEND_TIMEOUT="2000"
```

#### Step 3: Run the Docker Compose File
Execute the following command to start the LibreTranslate service in detached mode:

```sh
docker-compose up -d
```

### Configuring the Integration in Open WebUI

Once LibreTranslate is running, configure the integration within Open WebUI. Available integrations include:

- **LibreTranslate Filter Function**
- **LibreTranslate Action Function**
- **MultiLanguage LibreTranslate Action Function**
- **LibreTranslate Filter Pipeline**

Choose the integration that best fits your needs and follow the provided instructions for configuration.

#### Supported Languages
The LibreTranslate pipeline and function support a wide range of languages, including but not limited to:

- Albanian
- Arabic
- Azerbaijani
- Bengali
- Bulgarian
- Catalan (Valencian)
- Chinese
- Czech
- Danish
- Dutch
- English
- Flemish
- Esperanto
- Estonian
- Finnish
- French
- German
- Greek
- Hebrew
- Hindi
- Hungarian
- Indonesian
- Irish
- Italian
- Japanese
- Korean
- Latvian
- Lithuanian
- Malay
- Persian
- Polish
- Portuguese
- Romanian (Moldavian, Moldovan)
- Russian
- Slovak
- Slovenian
- Spanish (Castilian)
- Swedish
- Tagalog
- Thai
- Turkish
- Ukrainian
- Urdu

### Troubleshooting
Ensure the LibreTranslate service is running and accessible. Verify the Docker configuration and check the LibreTranslate logs for any errors.

### Benefits of Integration
Integrating LibreTranslate with Open WebUI offers several advantages:

- **Machine Translation:** Supports a wide range of languages.
- **Text Analysis:** Improves text analysis and processing capabilities.
- **Enhanced Functionality:** Provides better functionality for language-related tasks.

## Summary

This tutorial guides you through setting up LibreTranslate in Docker and integrating it with Open WebUI. By following the steps, you can leverage LibreTranslate's machine translation capabilities to enhance your Open WebUI instance.

# Tags
#libretranslate #integration #docker #openwebui #machine-translation