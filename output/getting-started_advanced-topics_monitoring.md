# Monitoring Open WebUI

## Key Concepts
- Basic health checks
- Model connectivity verification
- Deep health checks (response testing)
- Uptime Kuma configuration
- API key setup for monitoring

## Detailed Description

**Reference:** [https://docs.openwebui.com/getting-started/advanced-topics/monitoring](https://docs.openwebui.com/getting-started/advanced-topics/monitoring)

### Basic Health Check Endpoint
Open WebUI provides a basic health check endpoint to verify the service's availability:

- **Endpoint:** `/health`
  - **Status Code:** `200 OK` indicates the service is running.
  - **Usage:**
    ```bash
    curl https://your-open-webuiinstance/health
    ```
  - **Verification:**
    - Web server responsiveness
    - Application status
    - Basic database connectivity

### Using Uptime Kuma for Health Checks
Uptime Kuma is a self-hosted uptime monitoring tool. Configure it as follows:

1. **Add New Monitor**
   - **Monitor Type:** HTTP(s)
   - **Name:** Open WebUI
   - **URL:** `http://your-open-webuiinstance:8080/health`
   - **Monitoring Interval:** 60 seconds (or preferred interval)
   - **Retry Count:** 3

### Model Connectivity Verification
To ensure Open WebUI can connect to and list configured models, monitor the `/api/models` endpoint:

- **Endpoint:** `/api/models`
  - **Authentication Required:**
    ```bash
    curl -H "Authorization: Bearer YOUR_API_KEY" https://your-open-webuiinstance/api/models
    ```

#### Authentication Setup

1. **Enable API Keys**
   - Go to Admin Settings > General.
   - Enable the "Enable API Key" setting.
   - Save changes.

2. **Generate API Key**
   - Go to Settings > Account in Open WebUI.
   - Generate a new API key specifically for monitoring.
   - Copy the API key for use in Uptime Kuma.

#### Using Uptime Kuma for Model Connectivity
Configure a new monitor in Uptime Kuma:

- **Monitor Type:** HTTP(s) - JSON Query
  - **Name:** Open WebUI Model Connectivity
  - **URL:** `http://your-open-webuiinstance:8080/api/models`
  - **Method:** GET
  - **Expected Status Code:** 200
  - **JSON Query:**
    ```json
    $count(data[*]) > 0
    ```
  - **Expected Value:** true
  - **Monitoring Interval:** 300 seconds (5 minutes recommended)
  - **Authentication:**
    ```json
    { "Authorization": "Bearer YOUR_API_KEY" }
    ```

### Alternative JSON Queries

- Check for at least one model by a specific provider:
  ```json
  $count(data[owned_by='ollama']) > 1
  ```
- Verify if a specific model exists:
  ```json
  $exists(data[id='gpt-4o'])
  ```
- Ensure multiple models exist:
  ```json
  $count(data[id in ['gpt-4o', 'gpt-4o-mini']]) = 2
  ```

### Model Response Testing
To ensure models can process requests, monitor the `/api/chat/completions` endpoint:

```bash
curl -X POST https://your-open-webuiinstance/api/chat/completions \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{ "messages": [{"role": "user", "content": "Respond with the word HEALTHY"}], "model": "llama3.1", "temperature": 0 }'
```

## Summary
Monitoring Open WebUI involves checking service availability, model connectivity, and response testing. Use tools like Uptime Kuma for automated monitoring and ensure API keys are properly configured for secure access.

# Tags
#monitoring #healthchecks #uptimekuma #api #modelconnectivity