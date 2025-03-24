# MermaidJS Rendering Support in Open WebUI

## Key Concepts
- MermaidJS diagrams
- Code execution in chat interface
- Visualizing complex information
- Generating and exploring ideas with LLM
- Syntax requirements for rendering
- Interacting with visualizations (zooming, copying code)

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/code-execution/mermaid](https://docs.openwebui.com/features/code-execution/mermaid)

### Overview
Open WebUI supports the rendering of visually appealing MermaidJS diagrams directly within the chat interface. This includes flowcharts, pie charts, and more. When combined with a large language model (LLM), MermaidJS becomes a powerful tool for generating and exploring new ideas.

### Using MermaidJS in Open WebUI
To generate a MermaidJS diagram, you can ask an LLM within any chat to create one. Here are some examples of prompts:

- "Create a flowchart for a simple decision-making process using Mermaid."
- "Use Mermaid to visualize a decision tree to determine whether it's suitable to go for a walk outside."

### Syntax Requirements
For the LLM’s response to be rendered correctly, it must begin with the word `mermaid` followed by the MermaidJS code. Referencing the [MermaidJS documentation](https://mermaid-js.github.io/mermaid/) ensures correct syntax and helps guide the LLM towards generating better MermaidJS code.

### Visualizing MermaidJS Code Directly in the Chat
When you request a MermaidJS visualization, the LLM generates the necessary code. Open WebUI automatically renders this visualization directly within the chat interface, provided the code uses valid MermaidJS syntax.

If the visualization does not render correctly, it usually indicates a syntax error. You will be notified of any errors once the response is fully generated. In such cases, refer to the MermaidJS documentation to identify and correct the issue.

### Interacting with Your Visualization
Once your visualization is displayed, you can:
- Zoom in and out to examine it more closely.
- Copy the original MermaidJS code used to generate the visualization by clicking the copy button at the top-right corner of the display area.

### Example
Here’s an example of a flowchart generated using MermaidJS:

```mermaid
startAncestor [ start ]
A[A] --> B[B]
B --> C[Decision]
C -->| Yes | D[D]
C -->| No | E[E]
D --> F[F]
E --> F[F]
```

Experimenting with different types of diagrams and charts can help you develop a more nuanced understanding of how to effectively leverage MermaidJS within Open WebUI. For smaller models, consider referencing the MermaidJS documentation or having it summarize the documentation into comprehensive notes or a system prompt.

## Summary
Open WebUI supports rendering MermaidJS diagrams directly in the chat interface, enhancing the visualization of complex information and ideas when paired with an LLM. By following syntax requirements and interacting with visualizations effectively, users can unlock the full potential of this powerful tool.

# Tags
#mermaidjs #visualization #codeexecution #chatinterface #llm