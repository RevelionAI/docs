# Installation

The Revelion daemon is a single binary. Install it, authenticate it with your account token, and start it. The daemon handles everything else — image pulls, container lifecycle, tool execution.

---

## 1. Sign Up and Get Your Token

Create an account at [app.revelion.ai](https://app.revelion.ai) if you have not already.

Once logged in:

1. Navigate to **Daemons** in the sidebar.
2. Click **Add Daemon**.
3. Copy the authentication token shown — you will use it in the next step.

!!! warning "Token security"
    The auth token grants the daemon access to your Revelion account. Treat it like a password. Do not commit it to version control or share it.

---

## 2. Install the Daemon

Choose the instructions for your operating system.

### macOS / Linux

```bash
revelion@ai $ curl -fsSL https://raw.githubusercontent.com/RevelionAI/revelion-daemon/main/scripts/install.sh | bash
revelion@ai $ revelion auth YOUR_TOKEN
revelion@ai $ revelion start
```

The install script places the `revelion` binary in `/usr/local/bin` (or `~/.local/bin` if you do not have sudo). It detects your architecture automatically (x86_64 and arm64 are both supported).

### Windows (PowerShell)

```powershell
iwr -useb https://raw.githubusercontent.com/RevelionAI/revelion-daemon/main/scripts/install.ps1 | iex
revelion auth YOUR_TOKEN
revelion start
```

The installer places the `revelion.exe` binary in `%LOCALAPPDATA%\Revelion\bin` and adds it to your `PATH`. Open a new PowerShell window after install if the command is not found.

!!! tip "Running as a service"
    On Linux you can run the daemon as a systemd service so it starts automatically on boot. Run `revelion install-service` after authenticating to set this up.

---

## 3. Verify the Connection

After running `revelion start`, open the **Daemons** page in the dashboard. Your daemon's status should change to **Online** within a few seconds.

```
revelion@ai $ revelion status
daemon: connected
platform: app.revelion.ai
sandbox: image ready
```

If the status does not update, check [troubleshooting](../daemon.md#troubleshooting).

---

## What Happens on First Start

When the daemon starts for the first time, it:

1. Authenticates with your token and registers itself under your account.
2. Checks for the sandbox Docker image (`ghcr.io/revelionai/revelion-sandbox`).
3. Pulls the image if it is not already present — this is a one-time download (~3–4 GB).
4. Opens a persistent WebSocket connection to Revelion and waits for work.

!!! tip "Pre-pull timing"
    The image pull happens in the background. The daemon registers as online immediately; it will accept scan work once the pull completes. On a fast connection the pull takes 2–3 minutes.

---

## What's Next

With the daemon online, you are ready to [run your first mission](first-mission.md).
