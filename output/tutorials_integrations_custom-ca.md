# Setting up with Custom CA Store

## Key Concepts
- Community contribution tutorial
- SSL certificate verification error
- Custom CA store setup for Docker and local development
- Environment variables (REQUESTS_CA_BUNDLE, SSL_CERT_FILE)
- Dockerfile modifications for custom certificates

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/integrations/custom-ca](https://docs.openwebui.com/tutorials/integrations/custom-ca)

### Overview
This tutorial demonstrates how to customize Open WebUI by setting up a custom Certificate Authority (CA) store. It is a community-contributed guide and not officially supported by the Open WebUI team.

### Troubleshooting SSL Errors

If you encounter an `[SSL: CERTIFICATE_VERIFY_FAILED]` error when running OI, it likely indicates that your network intercepts HTTPS traffic (common in corporate environments).

#### Fixing the Error
To resolve this issue, add the new certificate to Open WebUI's truststore.

### Docker Setup

For pre-built Docker images, follow these steps:

1. **Mount the Certificate Store**
   - Use the following command-line option when running Docker:
     ```bash
     --volume=/etc/ssl/certs/ca-certificates.crt:/etc/ssl/certs/ca-certificates.crt:ro
     ```
   - This mounts the certificate store from your host machine into the container as read-only.

2. **Force Python to Use the System Truststore**
   - Set the environment variable:
     ```bash
     REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
     ```
   - If `REQUESTS_CA_BUNDLE` does not work, try setting `SSL_CERT_FILE` with the same value.

#### Example compose.yaml

Here is an example `compose.yaml` file contributed by @KizzyCode:
```yaml
services:
  openwebui:
    image: ghcr.io/open-webui/open-webui:main
    volumes:
      - /var/containers/openwebui:/app/backend/data:rw
      - /etc/containers/openwebui/compusrv.crt:/etc/ssl/certs/ca-certificates.crt:ro
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    environment:
      - WEBUI_NAME=compusrv
      - ENABLE_SIGNUP=False
      - ENABLE_COMMUNITY_SHARING=False
      - WEBUI_SESSION_COOKIE_SAME_SITE=strict
      - WEBUI_SESSION_COOKIE_SECURE=True
      - ENABLE_OLLAMA_API=False
      - REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
```

### Local Development

For local development, you can add certificates during the build process by modifying the Dockerfile.

#### Modifying the Dockerfile

1. **Frontend (Build Stage)**
   ```Dockerfile
   COPY package.json package-lock.json <YourRootCert>.crt ./ENV NODE_EXTRA_CA_CERTS=/app/<YourRootCert>.crtRUN npm ci
   ```

2. **Backend (Base Stage)**
   ```Dockerfile
   COPY <CorporateSSL.crt> /usr/local/share/ca-certificates/RUN update-ca-certificatesENV PIP_CERT=/etc/ssl/certs/ca-certificates.crt \ REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
   ```

## Summary

This tutorial guides users through setting up a custom CA store for Open WebUI, addressing SSL certificate verification errors in both Docker and local development environments. By following the steps outlined, users can ensure secure communication even on networks that intercept HTTPS traffic.

# Tags
#customCA #SSL #Docker #tutorial #certificates