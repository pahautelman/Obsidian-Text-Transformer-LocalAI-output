# Langfuse Integration with OpenWebUI

## Key Concepts
- Langfuse integration
- Monitoring and debugging
- Application traces
- Usage patterns
- Cost data by user and model
- Replay sessions to debug issues
- Evaluations
- Pipelines in OpenWebUi
- Quick Start Guide for integration

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/langfuse](https://docs.openwebui.com/tutorials/integrations/langfuse)

### Overview
Langfuse offers open-source observability and evaluations for OpenWebUI. By integrating Langfuse, you can trace application data to develop, monitor, and improve the use of OpenWebUI.

### Key Features

- **Application Traces:** Track detailed interactions within your application.
- **Usage Patterns:** Analyze how users interact with your system.
- **Cost Data:** Monitor costs associated with different users and models.
- **Replay Sessions:** Debug issues by replaying user sessions.
- **Evaluations:** Assess the performance and effectiveness of your integrations.

### Pipelines in OpenWebUi
Pipelines is an UI-agnostic framework for OpenAI API plugins. It allows you to inject plugins that intercept, process, and forward user prompts to the final LLM, providing enhanced control and customization of prompt handling.

### Integration Steps

#### Step 1: Setup OpenWebUI
Ensure OpenWebUI is running by following the [OpenWebUI documentation](https://docs.openwebui.com).

#### Step 2: Set Up Pipelines
Launch Pipelines using Docker with the following command:
```bash
docker run -p 9099:9099 --add-host=host.docker.internal:host-gateway -v pipelines:/app/pipelines --name pipelines --restart always ghcr.io/open-webui/pipelines:main
```

#### Step 3: Connecting OpenWebUI with Pipelines
In the Admin Settings, create a new connection of type OpenAI API with the following details:
- **URL:** `http://host.docker.internal:9099`
- **Password:** `0p3n-w3bu!`

#### Step 4: Adding the Langfuse Filter Pipeline
1. Navigate to Admin Settings -> Pipelines.
2. Add the Langfuse Filter Pipeline, specifying that Pipelines is listening on `http://host.docker.internal:9099`.
3. Install the Langfuse Filter Pipeline using the following GitHub URL:
   ```
   https://github.com/open-webui/pipelines/blob/main/examples/filters/langfuse_filter_pipeline.py
   ```

4. Add your Langfuse API keys. If you haven't signed up yet, create an account on [Langfuse](https://langfuse.com) to get your API keys.

#### Step 5: Viewing Traces in Langfuse
Interact with your OpenWebUI application and view the traces in Langfuse. You can see detailed interactions and usage patterns directly in the Langfuse UI.

### Additional Resources

For a comprehensive guide on OpenWebUI Pipelines, visit this [post](https://docs.openwebui.com/tutorials/integrations/langfuse).

## Summary
Integrating Langfuse with OpenWebUI enables real-time monitoring and analysis of message interactions. By following the quick start guide, you can set up Langfuse to trace application data, analyze usage patterns, monitor costs, replay sessions for debugging, and evaluate performance.

# Tags
#langfuse #integration #monitoring #debugging #pipelines #openwebui