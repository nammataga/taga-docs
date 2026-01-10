# TAGA Deployment Documentation

## Server Architecture Diagram

```mermaid
graph TB
    subgraph "Server Box"
        direction TB
        Nginx[Nginx<br>Reverse Proxy<br>Ports 80/443]
        CertBot[CertBot<br>SSL/TLS Management]
        Node[Node.js Application<br>Port 3000]
        
        Nginx -- "Proxies dynamic requests" --> Node
        CertBot -- "Auto‑renews certificates" --> Nginx
        Nginx -- "Serves directly" --> Static[Static Files]
    end
    
    Client[Web Clients] -- "HTTPS/HTTP" --> Nginx
    Client -- "Certificate validation" --> CertBot
    
    style Server fill:#f5f5f5,stroke:#333,stroke-width:2px
    style Nginx fill:#d4edda,stroke:#155724
    style CertBot fill:#fff3cd,stroke:#856404
    style Node fill:#d1ecf1,stroke:#0c5460
    style Client fill:#d6d8db,stroke:#383d41
    style Static fill:#f8d7da,stroke:#721c24
```

## Components

### Nginx
- **Role**: Reverse proxy and web server
- **Ports**: Listens on 80 (HTTP) and 443 (HTTPS)
- **Functions**:
  - Terminates SSL/TLS connections
  - Serves static assets directly
  - Proxies API and dynamic requests to Node.js
  - Load balancing (if multiple Node instances)
  - Rate limiting and security headers

### CertBot (Let's Encrypt)
- **Role**: Automated SSL certificate management
- **Functions**:
  - Obtains free TLS certificates
  - Auto‑renews certificates before expiry
  - Updates Nginx configuration automatically
  - Supports wildcard certificates if needed

### Node.js Application
- **Role**: Main web application server
- **Port**: Typically runs on 3000 (or other non‑privileged port)
- **Functions**:
  - Handles business logic and API endpoints
  - Renders dynamic pages
  - Connects to databases and external services

## Deployment Commands

The following aliases are available for managing the deployment:

```
sshtagaadmin='ssh admin-taga@31.97.62.187'
sshtagadev='ssh dev-taga@31.97.62.187'
sshtagasys='ssh sys-taga@31.97.62.187'
taga-admin='ssh admin-taga@taga-prod'
taga-cloudflare='firefox -P "ravi" https://dash.cloudflare.com &'
taga-dev='ssh dev@taga-prod'
taga-domain='firefox -P "ravi" https://www.godaddy.com &'
taga-github='firefox -P "ravi" https://www.github.com/nammataga &'
taga-host='firefox -P "ravi" https://hpanel.hostinger.com/vps/992688/overview &'
taga-info='cat secret | grep taga'
taga-root='ssh root@taga-prod'
taga-sys='ssh sys-taga@taga-prod'
taga-vm='ssh ravi@vm-taga'
tagaApi='cd ~/code/github/nammataga/prod/taga-api'
tagaUi='cd ~/code/github/nammataga/prod/taga-ui'
```

## Typical Deployment Flow

1. **Code Deployment**:
   ```bash
   git pull origin main
   npm install
   npm run build
   ```

2. **Process Management** (using PM2):
   ```bash
   pm2 restart app-name
   ```

3. **Nginx Configuration**:
   - Located at `/etc/nginx/sites-available/`
   - Test with `sudo nginx -t`
   - Reload with `sudo systemctl reload nginx`

4. **SSL Certificate Renewal**:
   ```bash
   sudo certbot renew --dry-run
   sudo certbot renew
   ```

## Monitoring

- Check Nginx status: `sudo systemctl status nginx`
- Check Node.js process: `pm2 status`
- View logs: `pm2 logs` or `sudo journalctl -u nginx`
