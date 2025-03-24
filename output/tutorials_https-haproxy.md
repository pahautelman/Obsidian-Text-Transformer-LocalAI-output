# HAProxy Configuration for Open WebUI

## Key Concepts
- HAProxy installation
- HTTPS configuration with Let's Encrypt
- HAProxy configuration basics
- SSL certificate issuance and management
- HAProxy Manager (automated deployment)

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/https-haproxy](https://docs.openwebui.com/tutorials/https-haproxy)

### Overview
This tutorial provides a community-contributed guide on configuring HAProxy for Open WebUI, focusing on setting up HTTPS using Let's Encrypt. It is not officially supported by the Open WebUI team but serves as a demonstration for customizing Open WebUI.

### Installing HAProxy and Certbot

#### For Redhat Derivatives
```bash
sudo dnf install haproxy certbot openssl -y
```

#### For Debian Derivatives
```bash
sudo apt install haproxy certbot openssl -y
```

### HAProxy Configuration Basics

The default configuration file for HAProxy is located at `/etc/haproxy/haproxy.cfg`. This file contains all the directives that determine how HAProxy operates.

#### Example Configuration
```plaintext
# Global settings
global
    log 127.0.0.1 local2 chroot /var/lib/haproxy pidfile /var/run/haproxy.pid maxconn 4000 user haproxy group haproxy daemon
    tune.ssl.default-dh-param 2048

# Default settings
defaults
    mode http log global option httplog option dontlognull option http-server-close option forwardfor except 127.0.0.0/8
    option redispatch retries 3 timeout http-request 300s timeout queue 2m timeout connect 120s timeout client 10m timeout server 10m timeout http-keep-alive 120s timeout check 10s maxconn 3000

# Frontend configuration
frontend web
    bind 0.0.0.0:80
    bind 0.0.0.0:443 ssl crt /path/to/ssl/folder/
    acl letsencrypt-acl path_beg /.well-known/acme-challenge/
    use_backend letsencrypt-backend if letsencrypt-acl

# Backend configuration for Let's Encrypt
backend letsencrypt-backend
    server letsencrypt 127.0.0.1:8688

# Backend configuration for Open WebUI Chat
backend owui_chat
    option forwardfor
    http-request add-header X-CLIENT-IP %[src]
    http-request set-header X-Forwarded-Proto https if { ssl_fc }
    server chat <ip>:3000
```

### Issuing SSL Certificates with Let's Encrypt

1. **Generate a Self-Signed Certificate**
   ```bash
   openssl req -x509 -newkey rsa:2048 -keyout /tmp/haproxy.key -out /tmp/haproxy.crt -days 3650 -nodes -subj "/CN=localhost"
   cat /tmp/haproxy.crt /tmp/haproxy.key > /etc/haproxy/certs/haproxy.pem
   ```

2. **Register with Let's Encrypt**
   ```bash
   certbot register --agree-tos --email your@email.com --non-interactive
   ```

3. **Request a Certificate**
   ```bash
   certbot certonly -n --standalone --preferred-challenges http --http-01-port-8688 -d yourdomain.com
   ```

4. **Merge Certificate and Key Files**
   ```bash
   cat /etc/letsencrypt/live/{domain}/fullchain.pem /etc/letsencrypt/live/{domain}/privkey.pem > /etc/haproxy/certs/{domain}.pem
   chmod 600 /etc/haproxy/certs/{domain}.pem
   chown haproxy:haproxy /etc/haproxy/certs/{domain}.pem
   ```

5. **Restart HAProxy**
   ```bash
   systemctl restart haproxy
   ```

### HAProxy Manager

For an easier deployment option, consider using the [HAProxy Manager](https://github.com/shadowdao/haproxy-manager). This Python script and Docker container automate the management of HAProxy configurations and Let's Encrypt SSL certificates.

## Summary
This tutorial guides users through installing and configuring HAProxy for Open WebUI with HTTPS support using Let's Encrypt. It covers installation steps, basic configuration, SSL certificate issuance, and an automated deployment option via HAProxy Manager.

# Tags
#HAProxy #OpenWebUI #HTTPS #Let'sEncrypt #tutorial