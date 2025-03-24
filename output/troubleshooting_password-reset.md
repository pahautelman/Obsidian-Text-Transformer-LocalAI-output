# Resetting Your Admin Password 🗝️

## Key Concepts
- Resetting admin password
- Docker deployments
- Local installations
- Generating bcrypt hash
- Updating passwords in Docker and local environments
- Completely resetting Open WebUI data

## Detailed Description

**Reference:** [https://docs.openwebui.com/troubleshooting/password-reset](https://docs.openwebui.com/troubleshooting/password-reset)

### Resetting Admin Password for Docker Deployments 🐳

#### Step 1: Generate a New Password Hash 🔐
To reset your admin password, first generate a bcrypt hash of your new password. Use the following command on your local machine:

```bash
htpasswd -bnBC 10 "" your-new-password | tr -d ':\n'
```

**Note:** Handle special characters carefully. Replace any `$` in the hash with `\\$`.

#### Step 2: Update the Password in Docker 🔄

Update the password in your Docker deployment using the generated bcrypt hash:

```bash
docker run --rm -v open-webui:/data alpine/socat EXEC:"bash -c 'apk add sqlite && echo UPDATE auth SET password='\''HASH'\'' WHERE email='\''admin@example.com'\''; | sqlite3 /data/webui.db'", STDIO
```

**Alternative Method:**

If the above command doesn't work, try this alternative:

1. Run Alpine Linux connected to the Open WebUI volume:
   ```bash
   docker run -it --rm -v open-webui:/path/to/data alpine
   ```

2. Install necessary packages and generate the bcrypt hash:
   ```bash
   apk add apache2-utils sqlite
   htpasswd -bnBC 10 "" your-new-password | tr -d ':'
   ```

3. Update the password in the database:
   ```bash
   sqlite3 /path/to/data/webui.db "UPDATE auth SET password='HASH' WHERE email='admin@example.com';"
   ```

### Resetting Admin Password for Local Installations 💻

#### Step 1: Generate a New Password Hash 🔐

Generate a bcrypt hash of your new password using the following command:

```bash
htpasswd -bnBC 10 "" your-new-password | tr -d ':\n'
```

#### Step 2: Update the Password Locally 🔄

Navigate to the `open-webui` directory and update the password:

```bash
sqlite3 backend/data/webui.db "UPDATE auth SET password='HASH' WHERE email='admin@example.com';"
```

### Completely Resetting Open WebUI Data

If you want to reset all data, including user accounts and settings, follow these steps:

#### Step 1: Locate `webui.db`

Activate your virtual environment (if applicable) and open a Python shell. Run the following code to find `webui.db`:

```python
import os
import open_webui

print("Open WebUI is installed at:", open_webui.__file__)
db_path = os.path.join(os.path.dirname(open_webui.__file__), "data", "webui.db")
print("Potential path to webui.db:", db_path)

if os.path.exists(db_path):
    print("webui.db found at:", db_path)
else:
    print("webui.db not found at:", db_path)
```

#### Step 2: Delete `webui.db`

Once located, delete the file using a command similar to:

```bash
rm -rf /path/to/your/python/environment/lib/pythonX.X/site-packages/open_webui/data/webui.db
```

**Warning:** Deleting `webui.db` will remove all stored data. Proceed with caution.

## Summary

To reset your admin password for Open WebUI, generate a bcrypt hash of your new password and update it in the appropriate environment (Docker or local). For a complete reset, locate and delete the `webui.db` file.

# Tags
#passwordreset #docker #localinstallation #bcrypt #troubleshooting