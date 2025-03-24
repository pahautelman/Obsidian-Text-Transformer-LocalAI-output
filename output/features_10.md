# Administration

## Key Concepts
- Super Admin Assignment
- Granular User Permissions
- Multi-User Management
- Admin Panel
- Active Users Indicator
- Default Sign-Up Role
- Prevent New Sign-Ups
- Prevent Chat Deletion
- Webhook Integration
- Configurable Notification Banners
- Model Whitelisting
- Admin Control for Community Sharing
- Trusted Email Authentication
- Backend Reverse Proxy Support
- Authentication
- Optional Authentication
- Advanced API Security
- Administrator Updates
- User Group Management
- Group-Based Access Control
- Granular User Permissions
- LDAP Authentication
- Customizable OpenAI Connections
- Ollama API Key Management
- Connection Management
- Intuitive Model Workspace
- API Key Authentication
- Unified Model Reset
- Flexible Model Access Control
- Configurable API Key Authentication Restrictions

## Detailed Description

### Super Admin Assignment
Automatically assigns the first sign-up as a super admin with an unchangeable role that cannot be modified by anyone else, not even other admins.

### Granular User Permissions
Restrict user actions and access with customizable role-based permissions, ensuring that only authorized individuals can perform specific tasks.

### Multi-User Management
Intuitive admin panel with pagination allows you to seamlessly manage multiple users, streamlining user administration and simplifying user life-cycle management.

### Admin Panel
The user management system is designed to streamline the on-boarding and management of users, offering the option to add users directly or in bulk via CSV import.

### Active Users Indicator
Monitor the number of active users and which models are being utilized by whom to assist in gauging when performance may be impacted due to a high number of users.

### Default Sign-Up Role
Specify the default role for new sign-ups to pending, user, or admin, providing flexibility in managing user permissions and access levels for new users.

### Prevent New Sign-Ups
Enable the option to disable new user sign-ups, restricting access to the platform and maintaining a fixed number of users.

### Prevent Chat Deletion
Ability for admins to toggle a setting that prevents all users from deleting their chat messages, ensuring that all chat messages are retained for audit or compliance purposes.

### Webhook Integration
Subscribe to new user sign-up events via webhook (compatible with Discord, Google Chat, Slack and Microsoft Teams), providing real-time notifications and automation capabilities.

### Configurable Notification Banners
Admins can create customizable banners with persistence in config.json, featuring options for content, background color (info, warning, error, or success), and dismissibility. Banners are accessible only to logged-in users, ensuring the confidentiality of sensitive information.

### Model Whitelisting
Enhance security and access control by allowing admins to whitelist models for users with the user role, ensuring that only authorized models can be accessed.

### Admin Control for Community Sharing
Admins can enable or disable community sharing for all users via a toggle in the Admin Panel > Settings menu. This toggle allows admins to manage accessibility and privacy, ensuring a secure environment. Admins have the option of enabling or disabling the Share on Community button for all users, which allows them to control community engagement and collaboration.

### Trusted Email Authentication
Optionally authenticate using a trusted email header, adding an extra layer of security and authentication to protect your Open WebUI instance.

### Backend Reverse Proxy Support
Bolster security through direct communication between Open WebUI's backend and Ollama. This key feature eliminates the need to expose Ollama over the local area network (LAN). Requests made to the /ollama/api route from Open WebUI are seamlessly redirected to Ollama from the backend, enhancing overall system security and providing an additional layer of protection.

### Authentication
Please note that Open WebUI does not natively support federated authentication schemes such as SSO, OAuth, SAML, or OIDC. However, it can be configured to delegate authentication to an authenticating reverse proxy, effectively achieving a Single Sign-On (SSO) experience. This setup allows you to centralize user authentication and management, enhancing security and user convenience. By integrating Open WebUI with an authenticating reverse proxy, you can leverage existing authentication systems and streamline user access to Open WebUI.

### Optional Authentication
Enjoy the flexibility of disabling authentication by setting WEBUI_AUTH to False. This is an ideal solution for fresh installations without existing users or can be useful for demonstration purposes.

### Advanced API Security
Block API users based on customized model filters, enhancing security and control over API access.

### Administrator Updates
Ensure administrators stay informed with immediate update notifications upon login, keeping them up-to-date on the latest changes and system statuses.

### User Group Management
Create and manage user groups for seamless organization and control.

### Group-Based Access Control
Set granular access to models, knowledge, prompts, and tools based on user groups, allowing for more controlled and secure environments.

### Granular User Permissions
Easily manage workspace permissions, including file uploads, deletions, edits, and temporary chats, as well as model, knowledge, prompt, and tool creation.

### LDAP Authentication
Enhance security and scalability with LDAP support for user management.

### Customizable OpenAI Connections
Enjoy smooth operation with custom OpenAI setups, including prefix ID support and explicit model ID support for APIs.

### Ollama API Key Management
Manage Ollama credentials, including prefix ID support, for secure and efficient operation.

### Connection Management
Easily enable or disable individual OpenAI and Ollama connections as needed.

### Intuitive Model Workspace
Manage models across users and groups with a redesigned and user-friendly interface.

### API Key Authentication
Tighten security by easily enabling or disabling API key authentication.

### Unified Model Reset
Reset and remove all models from the Admin Settings with a one-click option.

### Flexible Model Access Control
Easily bypass model access controls for user roles when not required, using the 'BYPASS_MODEL_ACCESS_CONTROL' environment variable, simplifying workflows in trusted environments.

### Configurable API Key Authentication Restrictions
Flexibly configure endpoint restrictions for API key authentication, now off by default for a smoother setup in trusted environments.

## Summary
Open WebUI offers comprehensive administrative tools, including user management, permissions, security features, and integration capabilities. These tools ensure that administrators can efficiently manage the platform, maintain security, and enhance user interactions.

# Tags
#administration #userpermissions #security #integration