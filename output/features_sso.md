# Federated Authentication Support

## Key Concepts
- OAuth2 providers (Google, Microsoft, GitHub)
- OIDC providers
- Trusted Header authentication
- Role and group management
- Tailscale Serve integration
- Cloudflare Tunnel with Cloudflare Access
- oauth2-proxy setup
- Authentik configuration

## Detailed Description

**Reference:** [https://docs.openwebui.com/features/sso](https://docs.openwebui.com/features/sso)

### Overview
Open WebUI supports several forms of federated authentication, including OAuth2 providers like Google, Microsoft, GitHub, and OIDC providers. This document outlines the configuration and usage of these authentication methods.

### OAuth2 Providers

#### Global Configuration Options
- **ENABLE_OAUTH_SIGNUP:** Allows account creation during OAuth login.
  - `true` or `false`
- **OAUTH_MERGE_ACCOUNTS_BY_EMAIL:** Logs into an account matching the email from the OAuth provider. This is considered insecure as not all providers verify email addresses.

#### Google
To configure a Google OAuth client:
1. Follow [Google's documentation](https://developers.google.com/identity/protocols/oauth2) to create a web application.
2. Set the allowed redirect URI to `<open-webui>/oauth/google/callback`.
3. Required environment variables:
   - `GOOGLE_CLIENT_ID`
   - `GOOGLE_CLIENT_SECRET`

#### Microsoft
To configure a Microsoft OAuth client:
1. Follow [Microsoft's documentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow) to create a web application.
2. Set the allowed redirect URI to `<open-webui>/oauth/microsoft/callback`.
3. Required environment variables:
   - `MICROSOFT_CLIENT_ID`
   - `MICROSOFT_CLIENT_SECRET`
   - `MICROSOFT_CLIENT_TENANT_ID` (use `9188040d-6c67-4c5b-b112-36a304b66dad` for personal accounts)

#### GitHub
To configure a GitHub OAuth client:
1. Follow [GitHub's documentation](https://docs.github.com/en/developers/apps/building-oauth-apps) to create an OAuth App.
2. Set the allowed redirect URI to `<open-webui>/oauth/github/callback`.
3 - Required environment variables:
   - `GITHUB_CLIENT_ID`
   - `GITHUB_CLIENT_SECRET`

### OIDC Providers
Any authentication provider that supports OIDC can be configured. The email claim is required, and name and picture claims are used if available.
- Set the allowed redirect URI to `<open-webui>/oauth/oidc/callback`.
- Required environment variables:
  - `OAUTH_CLIENT_ID`
  - `OAUTH_CLIENT_SECRET`
  - `OPENID_PROVIDER_URL` (e.g., `https://accounts.google.com/.well-known/openid-configuration`)
  - `OAUTH_PROVIDER_NAME` (defaults to SSO)
  - `OAUTH_SCOPES` (defaults to `openid email profile`)

### OAuth Role Management
To manage roles using OAuth:
1. Set `ENABLE_OAUTH_ROLE_MANAGEMENT` to `true`.
2. Configure the following environment variables:
   - `OAUTH_ROLES_CLAIM`: The claim containing the roles (defaults to `roles`).
   - `OAUTH_ALLOWED_ROLES`: A comma-separated list of allowed roles.
   - `OAUTH_ADMIN_ROLES`: A comma-separated list of admin roles.

### OAuth Group Management
To manage user groups using OAuth:
1. Set `ENABLE_OAUTH_GROUP_MANAGEMENT` to `true`.
2. Configure the following environment variables:
   - `OAUTH_GROUP_CLAIM`: The claim containing the groups (defaults to `groups`).

### Trusted Header Authentication
Open WebUI can delegate authentication to an authenticating reverse proxy that passes user details in HTTP headers.

#### Generic Configuration
- Set `WEBUI_AUTH_TRUSTED_EMAIL_HEADER` to use the header value as the email address.
  - Example: `WEBUI_AUTH_TRUSTED_EMAIL_HEADER=X-User-Email`

#### Tailscale Serve
Tailscale Serve allows sharing a service within your tailnet. It sets the header `Tailscale-User-Login` with the requester's email address.

**Example Docker Compose Configuration:**
```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    volumes:
      - open-webui:/app/backend/data
    environment:
      - HOST=127.0.0.1
      - WEBUI_AUTH_TRUSTED_EMAIL_HEADER=Tailscale-User-Login
      - WEBUI_AUTH_TRUSTED_NAME_HEADER=Tailscale-User-Name
    restart: unless-stopped

  tailscale:
    image: tailscale/tailscale:latest
    environment:
      - TS_AUTH_ONCE=true
      - TS_AUTHKEY=${TS_AUTHKEY}
      - TS_EXTRA_ARGS=--advertise-tags=tag:open-webui
      - TS_SERVE_CONFIG=/config/serve.json
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_HOSTNAME=open-webui
    volumes:
      - tailscale:/var/lib/tailscale
      - ./tailscale:/config
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - net_admin
      - sys_module
    restart: unless-stopped

volumes:
  open-webui: {}
  tailscale: {}
```

#### Cloudflare Tunnel with Cloudflare Access
Cloudflare Tunnel can protect Open WebUI with SSO. The header `Cf-Access-Authenticated-User-Email` is set with the authenticated user's email address.

**Example Docker Compose Configuration:**
```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    volumes:
      - open-webui:/app/backend/data
    environment:
      - HOST=127.0.0.1
      - WEBUI_AUTH_TRUSTED_EMAIL_HEADER=Cf-Access-Authenticated-User-Email
    restart: unless-stopped

  cloudflared:
    image: cloudflare/cloudflared:latest
    environment:
      - TUNNEL_TOKEN=${TUNNEL_TOKEN}
    command: tunnel run
    restart: unless-stopped

volumes:
  open-webui: {}
```

#### oauth2-proxy
oauth2-proxy is an authenticating reverse proxy that supports social OAuth providers and OIDC.

**Example Docker Compose Configuration:**
```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    volumes:
      - open-webui:/app/backend/data
    environment:
      - HOST=127.0.0.1
      - WEBUI_AUTH_TRUSTED_EMAIL_HEADER=X-Forwarded-Email
      - WEBUI_AUTH_TRUSTED_NAME_HEADER=X-Forwarded-User
    restart: unless-stopped

  oauth2-proxy:
    image: quay.io/oauth2-proxy/oauth2-proxy:v7.6.0
    environment:
      OAUTH2_PROXY_HTTP_ADDRESS: 0.0.0.0:4180
      OAUTH2_PROXY_UPSTREAMS: http://open-webui:8080/
      OAUTH2_PROXY_PROVIDER: google
      OAUTH2_PROXY_CLIENT_ID: REPLACEME_OAUTH_CLIENT_ID
      OAUTH2_PROXY_CLIENT_SECRET: REPLACEME_OAUTH_CLIENT_ID
      OAUTH2_PROXY_EMAIL_DOMAINS: REPLACEME_ALLOWED_EMAIL_DOMAINS
      OAUTH2_PROXY_REDIRECT_URL: REPLACEME_OAUTH_CALLBACK_URL
      OAUTH2_PROXY_COOKIE_SECRET: REPLACEME_COOKIE_SECRET
      OAUTH2_PROXY_COOKIE_SECURE: "false"
    restart: unless-stopped
    ports:
      - 4180:4180/tcp

volumes:
  open-webui: {}
```

#### Authentik
To configure an Authentik OAuth client, follow the documentation to create an application and OAuth2/OpenID Provider. Set the allowed redirect URI to `<open-webui>/oauth/oidc/callback`.

**Required Environment Variables:**
- `ENABLE_OAUTH_SIGNUP`
- `OAUTH_MERGE_ACCOUNTS_BY_EMAIL`
- `OAUTH_PROVIDER_NAME`
- `OPENID_PROVIDER_URL`
- `OAUTH_CLIENT_ID`
- `OAUTH_CLIENT_SECRET`
- `OAUTH_SCOPES`
- `OPENID_REDIRECT_URI`

### Summary
Open WebUI supports various federated authentication methods, including OAuth2 providers like Google, Microsoft, and GitHub, as well as OIDC providers. Trusted Header authentication can be used with services like Tailscale Serve and Cloudflare Tunnel. Role and group management are also supported through OAuth. Detailed configurations and examples are provided for each method to ensure secure and efficient integration.

# Tags
#federatedauthentication #oauth2 #oidc #trustedheader #tailscale #cloudflare #oauth2-proxy #authelia