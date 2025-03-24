# Jupyter Notebook Integration

## Key Concepts
- Jupyter Notebook integration with Open WebUI
- Docker Compose setup for services
- Configuration settings in `configs.py`
- Creating and managing CSV files, visualizations, and notebooks
- Troubleshooting tips for code execution

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/jupyter](https://docs.openwebui.com/tutorials/jupyter)

### Overview
This tutorial demonstrates how to integrate Jupyter Notebook with Open WebUI using Docker Compose. It covers the setup process, configuration steps, and practical examples of creating CSV files, visualizations, and notebooks.

> **Note:** This tutorial is a community contribution and not officially supported by the Open WebUI team. It serves as a demonstration for customizing Open WebUI for specific use cases.

### Prerequisites
- Ensure you are using version 0.5.16 or later of Open WebUI.
- Review the release notes for versions 0.5.11 and 0.5.15 for detailed improvements and changes related to Jupyter Notebook support.

### What is Jupyter Notebook?
Jupyter Notebook is an open-source web application that allows users to create and share documents containing live code, equations, visualizations, and narrative text. It is widely used in data science, scientific computing, and education for combining executable code with explanatory content.

### Step-by-Step Integration

#### Step 0: Configuration Summary
The target configuration involves setting up both Open WebUI and Jupyter Notebook services using Docker Compose. Below is the `docker-compose.yml` file for this setup:

```yaml
version: "3.8"
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:latest
    container_name: open-webui
    ports:
      - "3000:8080"
    volumes:
      - open-webui:/app/backend/data

  jupyter-notebook:
    image: jupyter/minimal-notebook:latest
    container_name: jupyter-notebook
    ports:
      - "8888:8888"
    volumes:
      - jupyter_data:/home/jovyan/work
    environment:
      - JUPYTER_ENABLE_LAB=yes
      - JUPYTER_TOKEN=123456

volumes:
  open-webui:
  jupyter_data:
```

To launch the stack, run the following command in the directory containing the `docker-compose.yml` file:

```sh
docker-compose up -d
```

Access the services at:
- Open WebUI: [http://localhost:3000](http://localhost:3000)
- Jupyter Notebook: [http://localhost:8888](http://localhost:8888)

Use the token `123456` to access Jupyter.

#### Step 1: Configure Code Execution
Configure Open WebUI's Code Execution to use Jupyter under Admin Panel -> Settings -> Code Execution. Review the latest configurations in the `configs.py` file for updates:

```python
ENABLE_CODE_INTERPRETER = True
CODE_EXECUTION_ENGINE = "jupyter"
CODE_EXECUTION_JUPYTER_URL = "http://localhost:8888"
CODE_EXECUTION_JUPYTER_AUTH = False
CODE_EXECUTION_JUPYTER_AUTH_TOKEN = "123456"
CODE_EXECUTION_JUPYTER_TIMEOUT = 30

CODE_INTERPRETER_ENGINE = "jupyter"
CODE_INTERPRETER_JUPYTER_URL = "http://localhost:8888"
CODE_INTERPRETER_JUPYTER_AUTH = False
CODE_INTERPRETER_JUPYTER_AUTH_TOKEN = "123456"
CODE_INTERPRETER_JUPYTER_TIMEOUT = 30
```

#### Step 2: Test the Connection

**Create a CSV**

Prompt:
```plaintext
Create two CSV files using fake data. The first CSV should be created using vanilla python and the second CSV should be created using the pandas library. Name the CSVs data1.csv and data2.csv.
```

**Create Visualizations**

Prompt:
```plaintext
Create several visualizations in Python using matplotlib and seaborn and save them to Jupyter.
```

**Create a Notebook**

Prompt:
```plaintext
Write Python code to read and write JSON files and save it to my notebook called notebook.ipynb.
```

### Troubleshooting Tips

- If Open WebUI does not automatically save the code or output generated within Open WebUI to your instance of Jupyter, follow this two-step workflow:
  1. Create the code artifact you want.
  2. Ask it to save it to your instance of Jupyter.

## Summary
This tutorial guides users through integrating Jupyter Notebook with Open WebUI using Docker Compose. It covers the setup process, configuration steps, and practical examples of creating CSV files, visualizations, and notebooks. The tutorial also provides troubleshooting tips for ensuring smooth code execution between the two services.

# Tags
#jupyter #openwebui #dockercompose #tutorial #integration