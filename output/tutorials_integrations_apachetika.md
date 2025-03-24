# Apache Tika Extraction

## Key Concepts
- Community contribution tutorial
- Integrating Apache Tika with Open WebUI
- Prerequisites (Docker, network setup)
- Integration steps (Docker Compose, Docker Run)
- Configuration in Open WebUI Admin Panel
- Verification and troubleshooting

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/apachetika](https://docs.openwebui.com/tutorials/integrations/apachetika)

### Overview
This tutorial, contributed by the community, demonstrates how to integrate Apache Tika with Open WebUI. It is not officially supported but serves as a guide for customizing Open WebUI for specific use cases.

### Prerequisites

Before starting the integration, ensure you have:

- **Open WebUI instance** installed.
- **Docker** installed on your system.
- **Docker network** set up for Open WebUI.

### Integration Steps

#### Step 1: Run Apache Tika
You can run Apache Tika using either Docker Compose or a Docker Run command.

##### Option 1: Using Docker Compose
1. Create a `docker-compose.yml` file in the same directory as your Open WebUI instance.
2. Add the following configuration:

```yaml
services:
  tika:
    image: apache/tika:latest-full
    container_name: tika
    ports:
      - "9998:9998"
    restart: unless-stopped
```

3. Run the Docker Compose file using:

```sh
docker-compose up -d
```

##### Option 2: Using Docker Run Command

Alternatively, run Apache Tika with:

```sh
docker run -d --name tika \
  -p 9998:9998 \
  --restart unless-stopped \
  apache/tika:latest-full
```

If running in the same network as Open WebUI, use the `--network` flag.

#### Step 2: Configure Open WebUI

1. Log in to your Open WebUI instance.
2. Navigate to **Admin Panel** > **Settings**.
3. Click on the **Documents** tab.
4. Change the **Default content extraction engine** to Tika.
5. Update the context extraction engine URL to `http://tika:9998`.
6. Save the changes.

### Verification

To verify Apache Tika is working correctly:

1. Start the Apache Tika Docker container:
   ```sh
   docker run -p 9998:9998 apache/tika
   ```

2. Verify the server is running with a GET request:
   ```sh
   curl -X GET http://localhost:9998/tika
   ```
   Expected response:
   ```
   This is Tika Server. Please PUT ...
   ```

3. Test Apache Tika by sending a file for analysis:
   ```sh
   curl -T test.txt http://localhost:9998/tika
   ```
   Replace `test.txt` with the path to your file.

### Using a Script to Verify Apache Tika

A Python script can automate the verification process:

```python
import requests

def verify_tika(file_path, tika_url):
    try:
        response = requests.put(tika_url, files={'file': open(file_path, 'rb')})
        if response.status_code == 200:
            print("Apache Tika successfully analyzed the file.")
            print("Response from Apache Tika:")
            print(response.text)
        else:
            print("Error analyzing the file:")
            print(f"Status code: {response.status_code}")
            print(f"Response from Apache Tika: {response.text}")
    except Exception as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    file_path = "test.txt"
    tika_url = "http://localhost:9998/tika"
    verify_tika(file_path, tika_url)
```

#### Instructions to Run the Script

1. Ensure **Python 3.x** and the `requests` library are installed.
2. Save the script as `verify_tika.py`.
3. Open a terminal, navigate to the script directory, and run:
   ```sh
   python verify_tika.py
   ```

### Troubleshooting

- Ensure the Apache Tika service is running and accessible from Open WebUI.
- Check Docker logs for any errors related to Apache Tika.
- Verify the context extraction engine URL in Open WebUI settings.

### Benefits of Integration

Integrating Apache Tika with Open WebUI offers:

- **Improved Metadata Extraction:** Accurate data extraction from files.
- **Support for Multiple File Formats:** Handles diverse file types.
- **Enhanced Content Analysis:** Extracts valuable insights from files.

## Summary
This tutorial guides users through integrating Apache Tika with Open WebUI, enhancing metadata extraction and content analysis capabilities. The process involves setting up Docker, configuring Open WebUI, and verifying the integration using various methods.

# Tags
#apachetika #integration #docker #openwebui #metadataextraction