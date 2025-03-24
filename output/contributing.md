# Contributing

## Key Concepts
- Code contribution guidelines
- Documentation and tutorials
- Translations and internationalization
- Reporting issues
- Docker deployment support

## Detailed Description

**Reference:** [https://docs.openwebui.com/contributing](https://docs.openwebui.com/contributing)

### Welcome to Contributors!
Your interest in contributing to Open WebUI is greatly appreciated. This document guides you through the process, ensuring your contributions enhance the project effectively.

### Code Contribution Guidelines
We welcome pull requests! Before submitting one:

1. **Open a Discussion:**
   - Share your ideas and get feedback from the community.
2. **Follow Coding Standards:**
   - Adhere to the project's coding standards.
3. **Include Tests:**
   - Write tests for new features to ensure reliability.
4. **Update Documentation:**
   - Keep documentation up-to-date with your changes.
5. **Write Clear Commit Messages:**
   - Use descriptive commit messages for better traceability.

### Code PR Best Practices
- **Atomic PRs:** Keep pull requests small and focused on a single objective.
  - This helps in easier code review and limits the chances of introducing unrelated issues.
- **Follow Existing Code Convention:** Ensure your code aligns with the project's coding standards.
- **Avoid Additional External Dependencies:**
  - Do not include additional external dependencies without prior discussion.
- **Framework Agnostic Approach:**
  - Implement functionalities on our own whenever possible rather than relying on external frameworks or libraries.

### Documentation & Tutorials
Help make Open WebUI more accessible by:
- Improving documentation.
- Writing tutorials.
- Creating guides on setting up and optimizing the web UI.

### Translations and Internationalization
Make Open WebUI available to a wider audience by adding new translations. Follow these steps:

1. **Create a New Directory:**
   - In `src/lib/i18n/locales`, create a directory with the appropriate language code (e.g., `es-ES` for Spanish).
2. **Copy Translation Files:**
   - Copy the American English translation files from the `en-US` directory to your new directory.
3. **Update String Values:**
   - Update the string values in JSON format according to your language, preserving the structure of the JSON object.
4. **Add Language Code:**
   - Add the language code and its respective title to `languages.json`.

### Questions & Feedback
Got questions or feedback? Join our Discord community or open an issue.

### Reporting Issues
If you notice something off or have an idea:
1. **Check Existing Issues:**
   - See if it's already been reported or suggested.
2. **Open a New Issue:**
   - Follow the provided issue templates to ensure all necessary details are included.
3. **Template Compliance:**
   - Failure to follow the template may result in your issue being closed without further consideration.

### Scope of Support
We support Docker deployment, but familiarity with Docker is assumed. For advanced configurations like setting up reverse proxies for HTTPS, foundational knowledge is required.

## Summary

Contributing to Open WebUI involves following specific guidelines for code contributions, documentation improvements, translations, and issue reporting. Adhering to these practices ensures that your contributions are effective and beneficial to the project.

# Tags
#contributing #code #documentation #translations #issues