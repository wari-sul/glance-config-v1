# AetherLabs Glance Dashboard Configuration

A unified monitoring dashboard for AetherLabs homelab infrastructure, designed to consolidate monitoring for local and remote VPS nodes distributed globally.

## 🌟 Overview

This repository contains the Glance configuration for AetherLabs, a homelab infrastructure monitoring solution that brings together:

- **Local Monitoring**: Services running on-premises in the homelab environment
- **Remote VPS Monitoring**: Virtual private servers distributed across global data centers
- **Entertainment Integration**: Spotify now playing and media widgets
- **Essential Tools**: Weather, world clock, DNS statistics, and more

## 📋 Features

### Essential Widgets

| Widget | Description |
|--------|-------------|
| 🌤️ **Local Weather** | Current weather conditions and forecasts for your homelab location |
| 🕐 **World Clock** | Real-time clock with multiple timezone support for global VPS coordination |
| 🛡️ **AdGuard DNS Stats** | DNS statistics from AdGuard Home including queries blocked and response times |
| 🎵 **Spotify Now Playing** | Currently playing music and recent listening history |
| 📊 **Service Monitor** | Health checks for remote VPS nodes |
| 📦 **Release Tracker** | GitHub releases for self-hosted applications |
| 📰 **RSS Feeds** | Tech news from r/selfhosted and other sources |

### Infrastructure Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│                    AetherLabs Dashboard                             │
├──────────────┬─────────────────────────┬───────────────────────────┤
│ LOCAL NODE   │   ENTERTAINMENT         │ REMOTE VPS NODES          │
│              │                         │                           │
│ • Weather    │   • Spotify Now Playing │ • EU Node (Frankfurt)     │
│ • Clock      │   • Quick Bookmarks     │ • APAC Node (Singapore)   │
│ • AdGuard    │                         │ • NA Node (NYC)           │
│   DNS Stats  │                         │ • Service Health          │
│              │                         │ • Release Tracker         │
│              │                         │ • RSS Feeds               │
└──────────────┴─────────────────────────┴───────────────────────────┘
```

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Access to your local services (AdGuard Home, etc.)
- Spotify Developer account (optional, for Spotify widget)

### Installation

1. **Clone this repository:**
   ```bash
   git clone https://github.com/wari-sul/glance-config-v1.git
   cd glance-config-v1
   ```

2. **Configure your settings:**
   - Edit `glance.yaml` to update:
     - Weather location
     - AdGuard Home URL and credentials
     - Spotify API credentials
     - Remote VPS monitoring URLs
     - Timezone preferences

3. **Deploy with Docker:**
   ```bash
   docker run -d \
     --name glance \
     -p 8080:8080 \
     -v $(pwd)/glance.yaml:/app/config/glance.yaml \
     glanceapp/glance
   ```

   Or using Docker Compose, create a `docker-compose.yml`:
   ```yaml
   version: '3.8'
   services:
     glance:
       image: glanceapp/glance
       container_name: glance
       ports:
         - 8080:8080
       volumes:
         - ./glance.yaml:/app/config/glance.yaml
       environment:
         - TZ=America/Los_Angeles
       restart: unless-stopped
   ```

4. **Access the dashboard:**
   Open `http://localhost:8080` in your browser

## 🔧 Configuration

### Environment Variables

For security, use environment variables for sensitive credentials:

| Variable | Description |
|----------|-------------|
| `ADGUARD_URL` | AdGuard Home base URL |
| `ADGUARD_USERNAME` | AdGuard Home username |
| `ADGUARD_PASSWORD` | AdGuard Home password |
| `SPOTIFY_CLIENT_ID` | Spotify API client ID |
| `SPOTIFY_CLIENT_SECRET` | Spotify API client secret |
| `SPOTIFY_REFRESH_TOKEN` | Spotify OAuth refresh token |
| `GITHUB_TOKEN` | GitHub personal access token |

### Widget Configuration

Detailed configuration instructions are provided as comments within `glance.yaml`. Key sections include:

- **Server Configuration**: Port, host binding
- **Theme Configuration**: Colors, contrast
- **Widget Configuration**: Individual widget settings
- **Local Node Monitoring**: AdGuard, weather, clock
- **Remote VPS Monitoring**: Service health checks

## 📚 References

This configuration is inspired by:

- [r/selfhosted](https://reddit.com/r/selfhosted) community configurations
- [glanceapp/community-widgets](https://github.com/glanceapp/community-widgets)
- [Glance Documentation](https://github.com/glanceapp/glance)

## 🛠️ Troubleshooting

### Common Issues

1. **Widgets not loading**: Check network connectivity and API credentials
2. **Weather not updating**: Verify location format
3. **AdGuard stats empty**: Ensure API is enabled and credentials are correct
4. **Spotify not working**: Verify OAuth refresh token is valid

See the detailed troubleshooting section in `glance.yaml` for more information.

## 📄 License

This configuration is provided as-is for personal use. Feel free to adapt it for your own homelab setup.

---

*Part of the AetherLabs homelab infrastructure project*
