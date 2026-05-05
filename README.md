## 👋 Welcome to nginx-proxy-manager 🚀

Docker container for managing Nginx proxy hosts with SSL

## 📋 Description

Docker container for managing Nginx proxy hosts with SSL

## 🚀 Services

- **proxy**: jc21/nginx-proxy-manager:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/nginx-proxy-manager/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/nginx-proxy-manager" ~/.local/srv/docker/nginx-proxy-manager
cd ~/.local/srv/docker/nginx-proxy-manager
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install nginx-proxy-manager
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8080

## 📂 Volumes

- `./volumes/data/nginx-proxy-manager` - Data storage
- `./volumes/data/log/nginx-proxy-manager` - Data storage
- `./volumes/config/nginx-proxy-manager` - Data storage

## 🔍 Logging

```shell
docker compose logs -f proxy
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
