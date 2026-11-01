## 👋 Welcome to nginx-proxy-manager 🚀

An L4 proxy for the automated nginx

## 📋 Description

Nginx Proxy Manager is an L4 proxy with an nginx core and a management UI. It
lets you create reverse proxy, redirect, and static host definitions through a
web interface, and handles Let's Encrypt certificates for them. This stack runs
the management application backed by PostgreSQL.

## 🚀 Services

- **app**: jc21/nginx-proxy-manager:latest

### Infrastructure Components

- **db**: postgres:latest - PostgreSQL database

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/nginx-proxy-manager/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/nginx-proxy-manager" ~/.local/srv/docker/nginx-proxy-manager
cd ~/.local/srv/docker/nginx-proxy-manager
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install nginx-proxy-manager
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ORG_NAME=Nginx Proxy Manager
APP_ADMIN_EMAIL=admin@example.com
APP_ADMIN_PASS=replace-with-a-random-password
DB_USER_NAME=nginx_proxy_manager
DB_USER_PASS=replace-with-a-random-password
DB_ROOT_PASS=replace-with-a-random-password
DB_CREATE_DATABASE_NAME=nginx_proxy_manager
```

`APP_ADMIN_PASS` is only used when the database is empty, so change the
password from the admin UI after the first login.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, admin UI published on `172.17.0.1:64272` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64272
- **Default Admin**: the `APP_ADMIN_EMAIL` and `APP_ADMIN_PASS` values above

Only the management UI (container port 81) is published. This stack does not
publish the app's 80/443 listeners, so reverse proxy hosts created inside the
UI are not reachable from the host as configured. To serve those hosts, publish
80/443 yourself, or place this stack behind a front-end proxy and forward to it
over the project network.

## 📂 Volumes

- `./volumes/data/nginx-proxy-manager/data` - Application data and configuration
- `./volumes/data/nginx-proxy-manager/letsencrypt` - Let's Encrypt certificates
- `./volumes/data/db/postgres/nginx-proxy-manager` - PostgreSQL database data

## 🔐 Security

- Change the admin password immediately after first login
- Use strong secrets for all database passwords
- Configure HTTPS before adding any reverse proxy host
- Do not expose the admin UI to the public internet without a front-end proxy
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
