# 🚀 Traefik One-Command Setup

**Automatically configure Traefik reverse proxy with HTTPS on any new server with a single command!**

[![YouTube Tutorial](https://img.shields.io/badge/YouTube-Watch%20Tutorial-red?style=for-the-badge&logo=youtube)](https://youtu.be/CY8nyQ_utB0)

## 📹 Watch the Video Tutorial

For a complete step-by-step guide, watch my YouTube tutorial:

**[🎥 Configure Traefik with 1 Command (30 Second Setup)](https://youtu.be/CY8nyQ_utB0)**

## Important Notice for Docker 29 Users

Docker version 29 introduces a new minimum API level which breaks older clients such as Traefik v2.x and other management tools.  
If you are running Docker 29, add the following to your Docker daemon configuration:

```bash
sudo nano /etc/docker/daemon.json
```

```
{
  "min-api-version": "1.24"
}
```

```
sudo systemctl restart docker
```
This restores compatibility so Traefik and other containers can connect to the Docker API normally.

## 🚀 Quick Start

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/softsweb/traefik-setup/main/install-traefik.sh)"
```

That's it! The script will guide you through the setup process.

## ✨ Features

- ✅ **One-command setup** - Fully automated installation
- ✅ **Automatic HTTPS** - Let's Encrypt SSL certificates
- ✅ **Temporary test page** - Auto-removes after 10 minutes
- ✅ **Docker-based** - Clean containerized setup
- ✅ **Zero configuration** - No manual config files needed

## 📋 Setup Process

When you run the command, you'll be prompted for:

1. **Email** (optional) - For Let's Encrypt certificate notifications
2. **Test Domain** (optional) - Domain/subdomain for testing

### Example Usage:
```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/softsweb/traefik-setup/main/install-traefik.sh)"
```

## 🌐 After Setup

If you provided a test domain:
- **Test Page**: `https://your-test-domain.com` (auto-removes in 10 min)
- **Traefik Ready**: For your applications with automatic HTTPS

## 📝 Prerequisites

- **Linux server** (Ubuntu/Debian recommended)
- **Docker** installed
- **Domain name** pointing to your server (for SSL)

## 🛠️ Managing Your Setup

```bash
# Check status
cd /opt/traefik
docker compose ps

# View logs
docker compose logs -f

# Restart Traefik
docker compose restart
```

## 🚀 Adding Your Applications

After Traefik is set up, you can deploy any application by adding it to the `traefik` network and using the appropriate labels. Here's an example:

```yaml
services:
  your-app-name:
    image: your-app-image:latest
    restart: unless-stopped
    networks:
      - traefik
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.your-app-name.rule=Host(`yoursubdomain.yourdomain.com`)"
      - "traefik.http.routers.your-app-name.entrypoints=websecure"
      - "traefik.http.routers.your-app-name.tls.certresolver=letsencrypt"

networks:
  traefik:
    external: true
```
### Key Points:
- Replace `your-app-name` with your actual application name
- Replace `yoursubdomain.yourdomain.com` with your actual domain
- The application must be on the `traefik` network
- SSL certificates are automatically handled by Let's Encrypt

---

## 👨‍💻 Author

**SoftsWeb**  
- 🎥 [YouTube Channel](https://youtube.com/@softsweb)  
- 🌐 [Website](https://softsweb.com)

---

**⭐ If you find this useful, please give it a star on GitHub!**

**📺 Don't forget to watch the [video tutorial](https://youtu.be/CY8nyQ_utB0) for a complete walkthrough!**


