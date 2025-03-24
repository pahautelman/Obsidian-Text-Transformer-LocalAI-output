# Python Code Execution

## Key Concepts
- Client-side execution of Python code in the browser
- Pyodide environment for running scripts
- Supported libraries (micropip, packaging, requests, beautifulsoup4, numpy, pandas, matplotlib, scikit-learn, scipy, regex)
- Invoking and executing Python code
- Tips for using Python code execution
- Extending supported libraries

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/code-execution/python](https://docs.openwebui.com/features/code-execution/python)

### Overview
Open WebUI enables client-side execution of Python code directly in the browser. This feature leverages Pyodide to run scripts within a chat interface, allowing Large Language Models (LLMs) to generate and execute Python code seamlessly.

#### Key Features:
- **Privacy and Flexibility:** Open WebUI mirrors PyPI packages locally, avoiding external network requests.
- **Self-contained Environment:** The frontend includes a WASM-based Python environment powered by Pyodide, requiring no additional setup or installation.

### Supported Libraries
The following libraries are supported in the Pyodide environment within Open WebUI:

| Library Name       | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| micropip           | Package manager for installing Python packages.                         |
| packaging          | Utilities for Python package management.                                  |
| requests           | HTTP library for making network requests.                                 |
| beautifulsoup4     | Library for parsing HTML and XML documents.                               |
| numpy              | Fundamental package for scientific computing with Python.                 |
| pandas             | Data manipulation and analysis library.                                   |
| matplotlib         | Plotting library for creating static, animated, and interactive visualizations.|
| scikit-learn       | Machine learning library built on NumPy, SciPy, and matplotlib.           |
| scipy              | Library used for scientific and technical computing.                      |
| regex              | Regular expression operations similar to Perl.                            |

### Invoking Python Code Execution
To execute Python code:
1. **Generate the Script:** Ask an LLM within a chat to write a Python script.
2. **Execute the Script:**
   - A "Run" button will appear at the top right-hand side of the code block.
   - Clicking this button executes the code using Pyodide.
3. **Display Results:**
   - Ensure there is at least one print statement in the code to display the result below the code block.

### Tips for Using Python Code Execution
- **Environment Awareness:** Inform the LLM that the code will run in a Pyodide environment.
- **Documentation:** Research the [Pyodide documentation](https://pyodide.org/en/stable/) to understand its capabilities and limitations.
- **Experiment:** Try different libraries and scripts to explore the possibilities of Python code execution in Open WebUI.

### Code Example
Here is an example of a simple Python script that can be executed using Pyodide:

```python
import pandas as pd

# Create a sample DataFrame
data = {'Name': ['John', 'Anna', 'Peter'], 'Age': [28, 24, 35]}
df = pd.DataFrame(data)

# Print the DataFrame
print(df)
```

This script creates a sample DataFrame using pandas and prints it below the code block within your chat.

### Extending the List of Supported Libraries
To add more libraries to the supported list:
1. **Fork the Pyodide Repository:** Create your own version of the Pyodide repository.
2. **Choose New Packages:** Select new packages from the existing list or explore high-quality packages not currently supported by Open WebUI.
3. **Integrate Packages:** Add the new packages to your forked repository to extend the capabilities.

## Summary
Open WebUI allows for client-side execution of Python code in the browser using Pyodide, supporting a range of libraries for various tasks. Users can generate and execute Python scripts directly within a chat interface, with tips and examples provided to enhance the experience. The environment is designed for ease of use and flexibility, with options to extend supported libraries by forking the Pyodide repository.

# Tags
#python #codeexecution #pyodide #webui #libraries