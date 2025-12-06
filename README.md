# AetherLabs Glance Dashboard Configuration

A unified monitoring dashboard for AetherLabs homelab infrastructure, designed to consolidate monitoring for local and remote VPS nodes distributed globally.

**Configuration patterns adopted from [kyrilltje/Glance_Dashboard](https://github.com/kyrilltje/Glance_Dashboard)**

## 🌟 Overview

This repository contains the Glance configuration for AetherLabs, a homelab infrastructure monitoring solution that brings together:

- **Local Monitoring**: Services running on-premises in the homelab environment
- **Remote VPS Monitoring**: Virtual private servers distributed across global data centers
- **Entertainment Integration**: Spotify, YouTube, Twitch, and media widgets
- **Essential Tools**: Weather, world clock, DNS statistics, and more
- **System Monitoring**: Docker containers, system resources, and service health

## 📋 Features

### Essential Widgets

| Widget | Description |
|--------|-------------|
| 🌤️ **Local Weather** | Current weather conditions and forecasts for Dhaka, Bangladesh |
| 🕐 **World Clock** | Real-time clock with Bangladesh (Asia/Dhaka +06) as primary timezone |
| 🛡️ **AdGuard DNS Stats** | DNS statistics from AdGuard Home including queries blocked |
| 💻 **System Resources** | CPU, RAM, and disk usage monitoring |
| 🎵 **Spotify Now Playing** | Currently playing music and recent listening history |
| 📺 **YouTube Videos** | Latest videos from subscribed tech channels |
| 🎮 **Twitch Streams** | Live streaming status from followed channels |
| 📈 **Markets** | Stock and cryptocurrency price tracking |
| 🧡 **Hacker News** | Top stories from Hacker News |
| 📊 **Service Monitor** | Health checks for remote VPS nodes |
| 📦 **Release Tracker** | GitHub releases for self-hosted applications |
| 📰 **RSS Feeds** | Tech news from r/selfhosted, r/homelab, and more |
| 💬 **Reddit** | Hot posts from r/selfhosted |
| 🐳 **Docker Containers** | Container status monitoring |
| 🔍 **Search** | Quick search with custom bangs |

### Infrastructure Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│                    AetherLabs Dashboard                             │
├──────────────┬─────────────────────────┬───────────────────────────┤
│ LOCAL NODE   │   ENTERTAINMENT         │ REMOTE VPS NODES          │
│              │                         │                           │
│ • Weather    │   • Spotify Now Playing │ • EU Node (Frankfurt)     │
│ • Clock      │   • YouTube Videos      │ • APAC Node (Singapore)   │
│ • AdGuard    │   • Twitch Streams      │ • NA Node (NYC)           │
│   DNS Stats  │   • Quick Bookmarks     │ • Hacker News             │
│ • System     │   • Markets             │ • Release Tracker         │
│   Resources  │                         │ • RSS Feeds               │
│              │                         │ • Reddit                  │
└──────────────┴─────────────────────────┴───────────────────────────┘
```

### Pages

The dashboard includes three pages:

1. **Home** (`/`): Main overview with local monitoring, entertainment, and remote VPS status
2. **Infrastructure** (`/infra`): Detailed monitoring with Docker containers, calendar, and search
3. **Media** (`/media`): Expanded YouTube subscriptions and Twitch streams

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Access to your local services (AdGuard Home, etc.)
- Spotify Developer account (optional, for Spotify widget)
- Docker socket access (optional, for container monitoring)

### Installation

1. **Clone this repository:**
   ```bash
   git clone https://github.com/wari-sul/glance-config-v1.git
   cd glance-config-v1
   ```

2. **Configure your settings:**
   - Edit `glance.yaml` to update:
     - Weather location (default: Dhaka, Bangladesh)
     - AdGuard Home URL and credentials
     - Spotify API credentials
     - Remote VPS monitoring URLs
     - YouTube channel IDs
     - Twitch channel names

3. **Deploy with Docker:**
   ```bash
   docker run -d \
     --name glance \
     -p 8080:8080 \
     -v $(pwd)/glance.yaml:/app/config/glance.yaml \
     -v /var/run/docker.sock:/var/run/docker.sock:ro \
     -e TZ=Asia/Dhaka \
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
         - /var/run/docker.sock:/var/run/docker.sock:ro
       environment:
         - TZ=Asia/Dhaka
       restart: unless-stopped
   ```

4. **Access the dashboard:**
   Open `http://localhost:8080` in your browser

## 🔧 Configuration

### Environment Variables

For security, use environment variables for sensitive credentials:

| Variable | Description | Required |
|----------|-------------|----------|
| `ADGUARD_URL` | AdGuard Home base URL (e.g., `http://192.168.1.100:3000`) | Yes |
| `ADGUARD_USERNAME` | AdGuard Home admin username | Yes |
| `ADGUARD_PASSWORD` | AdGuard Home admin password | Yes |
| `SPOTIFY_CLIENT_ID` | Spotify API client ID | Yes |
| `SPOTIFY_CLIENT_SECRET` | Spotify API client secret | Yes |
| `SPOTIFY_REFRESH_TOKEN` | Spotify OAuth refresh token | Yes |
| `VPS_EU_URL` | European VPS health endpoint | Yes |
| `VPS_APAC_URL` | Asia-Pacific VPS health endpoint | Yes |
| `VPS_NA_URL` | North America VPS health endpoint | Yes |
| `AUTH_SERVICE_URL` | Authentication service health endpoint | Yes |
| `ANALYTICS_URL` | Analytics API health endpoint | Yes |
| `CALENDAR_URL` | iCal/ICS calendar URL | Yes |
| `GITHUB_TOKEN` | GitHub personal access token (higher API limits) | Optional |
| `PROXMOX_API_URL` | Proxmox VE API endpoint | Optional |
| `PROXMOX_API_TOKEN` | Proxmox API token | Optional |
| `GRAFANA_DASHBOARD_URL` | Grafana dashboard iframe URL | Optional |
| `UPTIME_KUMA_URL` | Uptime Kuma instance URL | Optional |

### Widget Configuration

Detailed configuration instructions are provided as comments within `glance.yaml`. Key sections include:

- **Server Configuration**: Port, host binding
- **Theme Configuration**: Colors, contrast (dark theme with AetherLabs blue accent)
- **Widget Configuration**: Individual widget settings
- **Local Node Monitoring**: AdGuard, weather, clock, system resources
- **Entertainment & Media**: Spotify, YouTube, Twitch, Markets
- **Remote VPS Monitoring**: Service health checks
- **News & Social**: Hacker News, RSS feeds, Reddit

### Adopted from kyrilltje/Glance_Dashboard

The following widget patterns were adopted from [kyrilltje/Glance_Dashboard](https://github.com/kyrilltje/Glance_Dashboard):

- **System Info Widget**: CPU, RAM, Disk monitoring
- **Docker Containers Widget**: Container status and health
- **YouTube Videos Widget**: Subscribed channel feeds
- **Twitch Streams Widget**: Live stream monitoring
- **Markets Widget**: Stock and crypto tracking
- **Hacker News Widget**: Tech news aggregation
- **Search Widget**: Quick search with custom bangs
- **Enhanced Bookmarks**: Multi-group organization

## 📚 References

This configuration is inspired by:

- [kyrilltje/Glance_Dashboard](https://github.com/kyrilltje/Glance_Dashboard) - Primary source for widget patterns
- [r/selfhosted](https://reddit.com/r/selfhosted) community configurations
- [glanceapp/community-widgets](https://github.com/glanceapp/community-widgets)
- [Glance Documentation](https://github.com/glanceapp/glance)

## 🛠️ Troubleshooting

### Common Issues

1. **Widgets not loading**: Check network connectivity and API credentials
2. **Weather not updating**: Verify location format (default: Dhaka, Bangladesh)
3. **AdGuard stats empty**: Ensure API is enabled and credentials are correct
4. **Spotify not working**: Verify OAuth refresh token is valid
5. **Docker containers not showing**: Mount Docker socket `/var/run/docker.sock:/var/run/docker.sock:ro`
6. **YouTube/Twitch widgets empty**: Verify channel IDs/names are correct
7. **Markets widget not updating**: Yahoo Finance API has rate limits

See the detailed troubleshooting section in `glance.yaml` for more information.

## 📄 License

This configuration is provided as-is for personal use. Feel free to adapt it for your own homelab setup.

---

*Part of the AetherLabs homelab infrastructure project*
