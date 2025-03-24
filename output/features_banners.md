# Customizable Banners

## Key Concepts
- Overview of customizable banners
- Configuring banners through admin panel
- Configuring banners through environment variables
- Banner options and settings
- FAQ on banner configuration

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/banners](https://docs.openwebui.com/features/banners)

### Overview
Open WebUI offers a feature that allows administrators to create customizable banners with persistent configurations stored in the `config.json` file. These banners can be customized with various options, including content, background color (info, warning, error, or success), and dismissibility. Banners are only accessible to logged-in users, ensuring the confidentiality of sensitive information.

### Configuring Banners through the Admin Panel
To configure banners via the admin panel, follow these steps:

1. **Log in** as an administrator.
2. Navigate to **Admin Panel -> Settings -> Interface**.
3. Locate the **Banners** option above **Default Prompt Suggestions**.
4. Click on the **+ icon** to add a new banner.
5. Select the **banner type** and set the desired text.
6. Choose whether the banner is dismissible or not.
7. Optionally, set a timestamp for the banner.
8. Press **Save** at the bottom of the page.

### Configuring Banners through Environment Variables
Alternatively, you can configure banners using environment variables by setting the `WEBUI_BANNERS` variable with a list of dictionaries in the following format:

```json
[
  {
    "id": "string",
    "type": "string [info, success, warning, error]",
    "title": "string",
    "content": "string",
    "dismissible": False,
    "timestamp": 1000
  }
]
```

For more details on configuring environment variables in Open WebUI, refer to the **Environment Variable Configuration** documentation.

### Environment Variable Description

- `WEBUI_BANNERS`
  - Type: List of dictionaries
  - Default: []
  - Description: List of banners to show to users.

### Banner Options

| Option       | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| **id**       | Unique identifier for the banner.                                         |
| **type**     | Background color of the banner (info, success, warning, error).            |
| **title**    | Title of the banner.                                                      |
| **content**  | Content of the banner.                                                    |
| **dismissible** | Whether the banner is dismissible or not.                               |
| **timestamp** | Timestamp for the banner (optional).                                      |

### FAQ

- **Can I configure banners through the admin panel?**
  - Yes, navigate to Admin Panel -> Settings -> Interface and click on the + icon to add a new banner.

- **Can I configure banners through environment variables?**
  - Yes, set the `WEBUI_BANNERS` environment variable with a list of dictionaries.

- **What is the format for the WEBUI_BANNERS environment variable?**
  - The format is a list of dictionaries with keys: id, type, title, content, dismissible, and timestamp.

- **Can I make banners dismissible?**
  - Yes, set the `dismissible` key to True in the banner configuration or toggle dismissibility within the UI.

## Summary
Open WebUI allows administrators to create customizable banners that can be configured through the admin panel or environment variables. These banners offer various options for content, background color, and dismissibility, ensuring a tailored user experience while maintaining confidentiality for logged-in users.

# Tags
#banners #customization #adminpanel #environmentvariables