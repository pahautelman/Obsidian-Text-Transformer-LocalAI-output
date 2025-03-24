# HTTPS using Nginx

## Key Concepts
- Secure communication with HTTPS
- Nginx as a reverse proxy
- Self-signed certificates
- Let's Encrypt certificates
- Windows setup without Docker

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/https-nginx](https://docs.openwebui.com/tutorials/https-nginx)

### Overview
This tutorial demonstrates how to set up HTTPS using Nginx as a reverse proxy for Open WebUI. It covers three methods: self-signed certificates, Let's Encrypt certificates, and a Windows-specific setup without Docker.

### Self-Signed Certificates

Self-signed certificates are suitable for development or internal use where trust is not critical.

#### Steps
1. **Create Directories:**
   ```bash
   mkdir -p conf.d ssl
   ```

2. **Create Nginx Configuration File:**
   ```nginx
   server {
       listen 443 ssl;
       server_name your_domain_or_IP;
       ssl_certificate /etc/nginx/ssl/nginx.crt;
       ssl_certificate_key /etc/nginx/ssl/nginx.key;
       ssl_protocols TLSv1.2 TLSv1.3;

       location / {
           proxy_pass http://host.docker.internal:3000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
           proxy_buffering off;
       }
   }
   ```

3. **Generate Self-Signed SSL Certificates:**
   ```bash
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
   -keyout ssl/nginx.key -out ssl/nginx.crt -subj "/CN=your_domain_or_IP"
   ```

4. **Update Docker Compose Configuration:**
   ```yaml
   services:
     nginx:
       image: nginx:alpine
       ports:
         - "443:443"
       volumes:
         - ./conf.d:/etc/nginx/conf.d
         - ./ssl:/etc/nginx/ssl
       depends_on:
         - open-webui
   ```

5. **Start Nginx Service:**
   ```bash
   docker compose up -d nginx
   ```

6. **Access the WebUI:**
   ```
   https://your_domain_or_IP
   ```

### Let's Encrypt Certificates

Let's Encrypt provides free, trusted SSL certificates ideal for production environments.

#### Prerequisites
- Certbot installed on your system.
- DNS records properly configured to point to your server.

#### Steps
1. **Create Directories:**
   ```bash
   mkdir -p conf.d ssl
   ```

2. **Create Nginx Configuration File:**
   ```nginx
   server {
       listen 80;
       server_name your_domain_or_IP;

       location / {
           proxy_pass http://host.docker.internal:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection "upgrade";
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
           proxy_buffering off;
       }
   }
   ```

3. **Simplified Let's Encrypt Script:**
   ```bash
   #!/bin/bash
   DOMAIN="your_domain_or_IP"
   EMAIL="your_email@example.com"

   if ! command -v certbot &> /dev/null; then
       echo "Certbot not found. Installing..."
       sudo apt-get update
       sudo apt-get install -y certbot python3-certbot-nginx
   fi

   sudo certbot --nginx -d "$DOMAIN" --non-interactive --agree-tos -m "$EMAIL"
   sudo systemctl reload nginx
   echo "Let's Encrypt SSL certificate has been installed and Nginx reloaded."
   ```

4. **Make the Script Executable:**
   ```bash
   chmod +x enable_letsencrypt.sh
   ```

5. **Update Docker Compose Configuration:**
   ```yaml
   services:
     nginx:
       image: nginx:alpine
       ports:
         - "80:80"
         - "443:443"
       volumes:
         - ./conf.d:/etc/nginx/conf.d
         - ./ssl:/etc/nginx/ssl
       depends_on:
         - open-webui
   ```

6. **Start Nginx Service:**
   ```bash
   docker compose up -d nginx
   ```

7. **Run the Let's Encrypt Script:**
   ```bash
   ./enable_letsencrypt.sh
   ```

8. **Access the WebUI:**
   ```
   https://your_domain_or_IP
   ```

### Windows Setup without Docker

For basic internal/development installations, you can use Nginx and a self-signed certificate to proxy Open WebUI to HTTPS.

#### Steps
1. **Install OpenSSL:**
   - Download precompiled binaries from the Shining Light Productions (SLP) website.
   - Alternatively, use Chocolatey:
     ```bash
     choco install openssl -y
     ```

2. **Verify Installation:**
   ```bash
   openssl version
   ```

3. **Install Nginx:**
   - Download from nginx.org or use a package manager like Chocolatey.

4. **Generate Certificate:**
   ```bash
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
   -keyout nginx.key -out nginx.crt
   ```

5. **Configure Nginx:**
   Edit `C:\nginx\conf\nginx.conf`:
   ```nginx
   server {
       listen 443 ssl;
       server_name your_LAN_IP;

       ssl_certificate C:\\nginx\\nginx.crt;
       ssl_certificate_key C:\\nginx\\nginx.key;
       ssl_protocols TLSv1.2 TLSv1.3;

       location / {
           proxy_pass http://localhost:8080;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection $connection_upgrade;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
           proxy_buffering off;
       }
   }
   ```

6. **Run Nginx:**
   ```bash
   nginx -t
   nginx
   ```

7. **Access the WebUI:**
   ```
   https://your_LAN_IP
   ```

## Summary

This tutorial provides three methods to set up HTTPS for Open WebUI using Nginx: self-signed certificates, Let's Encrypt certificates, and a Windows-specific setup without Docker. Each method ensures secure communication between users and the Open WebUI.

# Tags
#https #nginx #ssl #certificates #tutorial