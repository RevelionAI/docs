# Getting Started

Getting Revelion running takes three steps. You will have a live scan in under ten minutes.

```
revelion@ai $ # Step 1: account → Step 2: daemon → Step 3: mission
```

---

## Step 1 — Create Your Account

Sign up at [app.revelion.ai](https://app.revelion.ai). New accounts receive free credits automatically — no card required to start.

[→ Requirements](requirements.md) — check what you need before installing.

---

## Step 2 — Install the Daemon

The daemon is a lightweight Go binary that runs on your machine. It manages the sandbox container, executes agent tool calls locally, and maintains a secure WebSocket connection to Revelion.

Docker must be running before you start the daemon. The daemon handles pulling the sandbox image automatically.

[→ Installation guide](installation.md)

---

## Step 3 — Launch Your First Mission

With the daemon connected, you can create a mission from the dashboard. Point Revelion at a target, choose a scan mode, and the agents start immediately.

[→ First mission walkthrough](first-mission.md)

---

!!! tip "Daemon shows as online before you start"
    Once the daemon authenticates, its status appears on the [Daemons](https://app.revelion.ai/agents) page in real-time. You do not need to do anything further — Revelion will route work to it automatically when a scan starts.
