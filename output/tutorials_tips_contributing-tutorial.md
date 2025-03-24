# Contributing Tutorials

## Key Concepts
- Forking GitHub repositories
- Enabling GitHub Actions and Pages
- Configuring environment variables
- Updating workflow files
- Drafting and submitting pull requests
- Community contributions

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/tips/contributing-tutorial](https://docs.openwebui.com/tutorials/tips/contributing-tutorial)

### Overview
This guide walks you through the process of contributing tutorials to the Open WebUI documentation. It covers setting up your environment, configuring necessary tools, and submitting your tutorial for review.

### Steps to Contribute

1. **Fork the Repository**
   - Navigate to the [Open WebUI Docs Repository](https://github.com/openwebui/docs) on GitHub.
   - Click the **Fork** button at the top-right corner to create a copy under your GitHub account.

2. **Enable GitHub Actions**
   - In your forked repository, go to the **Actions** tab.
   - Enable GitHub Actions by following the on-screen instructions if prompted.

3. **Enable GitHub Pages**
   - Go to **Settings > Pages** in your forked repository.
   - Under **Source**, select the branch you want to deploy (e.g., `main`) and the folder (e.g., `/docs`).
   - Click **Save** to enable GitHub Pages.

4. **Configure Environment Variables**
   - In your forked repository, go to **Settings > Secrets and variables > Actions > Variables**.
   - Add the following environment variables:
     - `BASE_URL`: Set to `/docs` (or your chosen base URL for the fork).
     - `SITE_URL`: Set to `https://<your-github-username>.github.io/`.

### Updating GitHub Pages Workflow and Config File

If you need to adjust deployment settings:

1. **Update `.github/workflows/gh-pages.yml`**
   ```yaml
   - name: Build
     env:
       BASE_URL: ${{ vars.BASE_URL }}
       SITE_URL: ${{ vars.SITE_URL }}
     run: npm run build
   ```

2. **Modify `docusaurus.config.ts` to Use Environment Variables**
   ```typescript
   const config: Config = {
     title: "Open WebUI",
     tagline: "ChatGPT-Style WebUI for LLMs (Formerly Ollama WebUI)",
     favicon: "images/favicon.png",
     url: process.env.SITE_URL || "https://openwebui.com",
     baseUrl: process.env.BASE_URL || "/",
     // other configurations...
   };
   ```

### Running the Workflow

- In the **Actions** tab, locate the `gh-pages` workflow.
- Trigger the workflow manually if necessary, or it may run automatically based on your setup.

### Drafting and Submitting Your Tutorial

1. **Browse to Your Forked Copy**
   - Visit `https://<your-github-username>.github.io/<BASE_URL>` to view your forked documentation.

2. **Draft Your Changes**
   - In your forked repository, navigate to the appropriate directory (e.g., `docs/tutorial/`).
   - Create a new markdown file for your tutorial or edit existing ones.
   - Ensure that your tutorial includes the unsupported warning banner:
     ```markdown
     :::warning
     This tutorial is a community contribution and is not supported by the Open WebUI team. It serves only as a demonstration on how to customize OpenWebUI for your specific use case. Want to contribute? Check out the contributing tutorial.
     :::
     ```

3. **Submit a Pull Request**
   - Once your tutorial is ready, commit your changes to your forked repository.
   - Navigate to the original [open-webui/docs repository](https://github.com/openwebui/docs).
   - Click **New Pull Request** and select your fork and branch as the source.
   - Provide a descriptive title and description for your PR.
   - Submit the pull request for review.

### Testing Locally

You can test your Docusaurus site locally with the following commands:
```bash
npm install # Install dependencies
npm run build # Build the site for production
```
This will help you catch any issues before deploying.

## Summary
Contributing tutorials to Open WebUI involves forking the repository, enabling GitHub Actions and Pages, configuring environment variables, updating workflow files, drafting your tutorial, and submitting a pull request. This process ensures that community contributions are integrated smoothly into the documentation.

# Tags
#contribution #tutorials #github #docusaurus #openwebui