# Improve Performance with Dedicated Task Models

## Key Concepts
- Automated features in Open-WebUI (title generation, tag creation, autocomplete, search query generation)
- Impact of background tasks on performance
- Optimizing task model for better responsiveness
- Configuring a dedicated task model
- Disabling unnecessary automation features

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/tips/improve-performance-local](https://docs.openwebui.com/tutorials/tips/improve-performance-local)

### Automated Features and Performance Impact
Open-WebUI includes several automated features to enhance user experience:
- **Title Generation**
- **Tag Creation**
- **Autocomplete** (triggers on every keystroke)
- **Search Query Generation**

These features can generate multiple simultaneous requests, impacting performance on systems with limited resources. For example, continuous calls from the autocomplete feature can significantly delay responses on devices with limited memory or processing power.

### Why Does Open-WebUI Feel Slow?
By default, Open-WebUI has several background tasks that can make it feel slow:
- **Title Generation**
- **Tag Generation**
- **Autocomplete Generation** (triggers on every keystroke)
- **Search Query Generation**

Each of these features makes asynchronous requests to your model. For instance, continuous calls from the autocomplete feature can significantly delay responses on devices with limited memory or processing power.

### Optimizing Task Model Performance
To optimize performance, follow these steps:

#### Step 1: Access the Admin Panel
1. Open Open-WebUI in your browser.
2. Navigate to the **Admin Panel**.
3. Click on **Settings** in the sidebar.

#### Step 2: Configure the Task Model
Go to **Interface > Set Task Model**. Choose one of the following options based on your needs:

- **Lightweight Local Model (Recommended)**
  - Select a compact model such as Llama 3.2 3B or Qwen2.5 3B.
  - These models offer rapid responses while consuming minimal system resources.

- **Hosted API Endpoint (For Maximum Speed)**
  - Connect to a hosted API service to handle task processing.
  - This can be very cheap. For example, OpenRouter offers Llama and Qwen models at less than 1.5 cents per million input tokens.

- **Disable Unnecessary Automation**
  - If certain automated features are not required, disable them to reduce extraneous background calls—especially features like autocomplete.

#### Step 3: Save Your Changes and Test
1. Save the new configuration.
2. Interact with your chat interface and observe the responsiveness.
3. If necessary, adjust by further disabling unused automation features or experimenting with different task models.

### Recommended Setup for Local Models
Implementing these recommendations can greatly improve the responsiveness of Open-WebUI while allowing your local models to efficiently handle chat interactions.

### Additional Tips
- **Monitor System Resources:** Use your operating system’s tools (such as Activity Monitor on macOS or Task Manager on Windows) to keep an eye on resource usage.
- **Reduce Parallel Model Calls:** Limiting background automation prevents simultaneous requests from overwhelming your LLM.
- **Experiment with Configurations:** Test different lightweight models or hosted endpoints to find the optimal balance between speed and functionality.
- **Stay Updated:** Regular updates to Open-WebUI often include performance improvements and bug fixes, so keep your software current.

## Summary
To improve the performance of Open-WebUI on local systems, configure a dedicated task model or disable unnecessary automation features. This ensures that your primary chat functionality remains responsive and efficient, even on devices with limited resources.

# Tags
#performance #optimization #taskmodel #automation #localmodels