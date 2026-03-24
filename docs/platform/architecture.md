# Architecture

Revelion is built on three components that run in distinct trust zones. Understanding the separation matters for network access, compliance requirements, and understanding where your data lives.

---

## Components

### Cloud Brain

The brain is Revelion's AI orchestration layer, hosted on Fly.io in London (LHR). It is responsible for:

- Running and coordinating AI agents
- Injecting skill knowledge into agent prompts
- Tracking scan state, findings, and agent conversations
- Enforcing scan budgets and credit consumption
- Generating reports on scan completion

**The brain never touches your targets directly.** It issues instructions to the daemon and receives results back. All tool execution and network traffic to targets happens in the sandbox on your machine.

### Daemon

The daemon is a lightweight Go binary that runs on your machine (or a machine on your network). It:

- Maintains a persistent WebSocket connection to the cloud brain
- Manages Docker containers (create, start, exec, destroy)
- Forwards tool output back to the brain in real time
- Handles VPN injection into sandbox containers

The daemon requires Docker to be running. It has no listening ports — it only makes outbound connections to the brain over WebSocket (`wss://`).

!!! tip
    For internal network testing, run the daemon on a machine that already has access to the target network. The sandbox container it spawns will inherit that network connectivity.

### Sandbox Container

Each scan gets a dedicated Docker container pulled from `ghcr.io/revelionai/revelion-sandbox`. The container holds the full pentesting tool stack. All scan traffic to targets originates here — from your machine, on your network, with your source IP.

The container is destroyed when the scan completes or is cancelled. Nothing persists between scans at the container level.

---

## Data Flow

```
User (browser)
    │
    ▼
app.revelion.ai  ──────────────────────────────────┐
    │                                               │
    ▼                                               │
Cloud Brain (Fly.io, LHR)                          │
    │  WebSocket (wss://)                           │
    ▼                                               │
Daemon (your machine)                              │
    │  docker exec                                  │
    ▼                                               │
Sandbox Container (Docker)                         │
    │  HTTP/TCP/UDP                                 │
    ▼                                               │
Target                                             │
                                                    │
Supabase (eu-west-1) ◄─────────────────────────────┘
  findings, events, reports, scan state
```

**Realtime updates** flow from the brain → Supabase → browser via Supabase Realtime (PostgreSQL logical replication). The Live Intel Feed, agent status, and findings panel all update without polling.

---

## Data Storage

All persistent data lives in Supabase (PostgreSQL, eu-west-1):

| Data | Table | Access |
|---|---|---|
| Scan metadata and state | `scans` | RLS — org-scoped |
| Agent conversations | `agent_messages` | RLS — org-scoped |
| Findings | `findings` | RLS — org-scoped |
| Live events | `scan_events` | RLS — scan-scoped |
| Assets and vuln tracking | `assets`, `asset_findings` | RLS — org-scoped |
| Reports (JSON/MD) | `scan_artifacts` | RLS — org-scoped |
| PDF reports | Supabase Storage | RLS — user-scoped |
| VPN configs | Supabase Storage | RLS — user-scoped |

Row-level security is enforced at the database layer. One organisation cannot read another's data regardless of application-level bugs.

!!! warning
    VPN configuration files are stored encrypted in Supabase Storage. They are only retrieved by the brain at scan start and injected directly into the sandbox container — they are never written to disk on your machine.

---

## Security Boundaries

- Brain → Daemon: authenticated via daemon token (stored in Supabase, checked on WebSocket upgrade)
- Browser → Brain API: authenticated via Supabase JWT
- Browser → Supabase: authenticated via Supabase JWT with RLS
- Sandbox → Brain: no direct connection — all communication is daemon-mediated
- Sandbox → Target: direct network, no proxying through Revelion infrastructure

---

## Deployment

- **Brain**: Fly.io, single machine by default, horizontal auto-scaling available
- **Redis**: Upstash (via Fly.io) — used for scan queuing, pub/sub, and rate limiting
- **Frontend**: Vercel, deployed at `app.revelion.ai`
- **Daemon**: Self-hosted binary, user-managed

See [Installation](../getting-started/installation.md) for daemon setup instructions.
