# Requirements

Before installing the Revelion daemon, confirm your machine meets the following requirements.

---

## Software

### Docker

The daemon manages a Docker container for each scan. Docker must be installed and running before the daemon starts.

| Platform | Required version | Install guide |
|---|---|---|
| Windows | Docker Desktop 4.0+ | [docs.docker.com](https://docs.docker.com/desktop/install/windows-install/) |
| macOS | Docker Desktop 4.0+ | [docs.docker.com](https://docs.docker.com/desktop/install/mac-install/) |
| Linux | Docker Engine 20.10+ | [docs.docker.com](https://docs.docker.com/engine/install/) |

!!! warning "Docker Desktop vs Docker Engine"
    On Windows and macOS, Docker Desktop is the standard installation. On Linux, Docker Engine (without Desktop) is sufficient and preferred for server environments.

### Web Browser

Access the Revelion dashboard from any modern browser. Chromium-based browsers (Chrome, Edge, Brave) and Firefox are fully supported. Safari is supported but not the primary test target.

---

## Hardware

The sandbox image contains a full offensive security toolset. Allocate enough resources for it to run comfortably alongside your normal workload.

| Resource | Minimum | Recommended |
|---|---|---|
| RAM | 4 GB free | 8 GB+ free |
| Disk space | 10 GB free | 20 GB+ free |
| CPU | 2 cores | 4+ cores |

!!! tip "Disk space"
    The sandbox image (`ghcr.io/revelionai/revelion-sandbox`) is pulled once and reused across all scans. The 10 GB requirement covers the image itself. Individual scan containers are ephemeral and removed after each scan completes.

---

## Operating System

| OS | Supported versions |
|---|---|
| Windows | Windows 10 (version 2004+), Windows 11 |
| macOS | macOS 12 Monterey and later |
| Linux (Ubuntu) | Ubuntu 20.04 LTS and later |
| Linux (other) | Any distro running Docker Engine 20.10+ |

---

## Network

The daemon requires outbound internet access to reach the Revelion platform over WebSocket (WSS, port 443). No inbound ports are required.

Scan targets must be reachable from your machine. For internal network testing, run the daemon on a machine that has access to the target network. For VPN-gated targets, attach a VPN config when creating the mission.

!!! warning "Firewalls and proxies"
    Corporate proxies that perform TLS inspection may interfere with the WebSocket connection. If the daemon fails to connect, check that `brain.revelion.ai` is excluded from inspection.

---

## What's Next

Once requirements are met, proceed to [installation](installation.md).
