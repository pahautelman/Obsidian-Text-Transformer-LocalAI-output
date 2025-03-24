# Webhook Integrations

## Key Concepts
- Overview of webhooks
- Configuring webhooks through Admin Interface
- Configuring webhooks through Environment Variables
- Verifying webhook functionality
- Troubleshooting webhook issues

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/webhooks](https://docs.openwebui.com/features/webhooks)

### Overview
Open WebUI offers a webhook feature that automatically sends notifications to a specified URL whenever new users sign up. This is achieved by providing Open WebUI with a webhook URL, which receives notifications upon the creation of new user accounts.

### Configuring Webhooks

#### Option 1: Admin Interface Configuration
To configure webhooks via the admin interface:

1. **Log in** to your Open WebUI instance as an administrator.
2. Navigate to the **Admin Panel**.
3. Click on the **Settings tab**.
4. Go to the **General section** of the settings.
5. Locate the **Webhook URL field** and enter your webhook URL.
6. Save the changes.

#### Option 2: Environment Variables Configuration
Alternatively, you can configure the webhook URL by setting the `WEBHOOK_URL` environment variable. For detailed instructions on using environment variables in Open WebUI, refer to [Environment Variable Configuration](https://docs.openwebui.com/features/webhooks).

### Verifying the Webhook

To ensure your webhook is functioning correctly:

1. Create a new user account in Open WebUI.
2. Check if you receive a notification at the specified webhook URL.

The payload format for the webhook notification is as follows:
```
New user signed up: <username>
```

For example, if a user named "Tim" signs up, the payload will be:
```
New user signed up: Tim
```

### Troubleshooting

If you encounter issues with your webhook:

- **Verify URL and Format:** Ensure the webhook URL is correct and properly formatted.
- **Service Configuration:** Confirm that the webhook service is enabled and configured correctly.
- **Logs Review:** Check Open WebUI logs for any errors related to the webhook.
- **Connection Issues:** Verify that the connection hasn't been interrupted or blocked by a firewall or proxy.
- **Server Availability:** Ensure the webhook server is available and not experiencing high latency.
- **API Key Validity:** If using an API key, verify it is valid, not expired, and not revoked.

> **Note:** The webhook feature in Open WebUI is continually evolving. Future updates will include additional features and event types.

## Summary
Webhooks in Open WebUI allow for automatic notifications upon new user sign-ups by configuring a webhook URL through the admin interface or environment variables. Verifying the setup involves creating a new user account and checking for notifications at the specified URL. Troubleshooting steps include verifying URLs, service configurations, logs, connections, server availability, and API key validity.

# Tags
#webhooks #integration #configuration #troubleshooting