# Installation

The Revelion daemon is a single binary. A one-liner installs it, authenticates with your account, and starts it automatically. The daemon handles everything else — image pulls, container lifecycle, tool execution.

---

## 1. Sign Up and Get Your Token

Create an account at [app.revelion.ai](https://app.revelion.ai) if you have not already.

Once logged in:

1. Navigate to [**Daemons**](https://app.revelion.ai/agents) in the sidebar.
2. Click **Add Daemon**.
3. Copy the authentication token shown — you will use it in the next step.

!!! warning "Token security"
    The auth token grants the daemon access to your Revelion account. Treat it like a password. Do not commit it to version control or share it.

---

## 2. Install the Daemon

The recommended approach is a single command that downloads the binary, authenticates, and starts the daemon in one step. Choose the instructions for your operating system.

### macOS / Linux (recommended one-liner)

```bash
curl -fsSL https://raw.githubusercontent.com/RevelionAI/revelion-daemon/main/scripts/install.sh | sh -s -- YOUR_API_TOKEN
```

That is it. The script downloads the correct binary for your platform and architecture (Linux/macOS, amd64/arm64), authenticates with your token, and starts the daemon automatically.

??? note "Manual steps (without token)"
    If you prefer to install first and authenticate later:

    ```bash
    curl -fsSL https://raw.githubusercontent.com/RevelionAI/revelion-daemon/main/scripts/install.sh | sh
    revelion auth YOUR_API_TOKEN
    revelion start
    ```

The install script places the `revelion` binary in `/usr/local/bin` (or `~/.local/bin` if you do not have sudo). It detects your architecture automatically (x86_64 and arm64 are both supported).

### Windows (PowerShell, recommended one-liner)

```powershell
$env:REVELION_TOKEN='YOUR_API_TOKEN'; irm https://raw.githubusercontent.com/RevelionAI/revelion-daemon/main/scripts/install.ps1 | iex
```

The token is passed via the `REVELION_TOKEN` environment variable. The script downloads the binary, authenticates, and starts the daemon automatically.

??? note "Manual steps (without token)"
    If you prefer to install first and authenticate later:

    ```powershell
    irm https://raw.githubusercontent.com/RevelionAI/revelion-daemon/main/scripts/install.ps1 | iex
    revelion auth YOUR_API_TOKEN
    revelion start
    ```

The installer places the `revelion.exe` binary in `%LOCALAPPDATA%\Revelion\bin` and adds it to your `PATH`. Open a new PowerShell window after install if the command is not found.

!!! tip "Running as a service"
    On Linux you can run the daemon as a systemd service so it starts automatically on boot. Run `revelion install-service` after authenticating to set this up.

---

## 3. Verify the Connection

After the install script finishes, open the [**Daemons**](https://app.revelion.ai/agents) page in the dashboard. Your daemon's status should change to **Online** within a few seconds.

```
revelion@ai $ revelion status
daemon: connected
platform: app.revelion.ai
sandbox: image ready
```

If the status does not update, check the [Architecture](../platform/architecture.md) page for details on daemon connectivity, or contact support on [Discord](https://discord.gg/fg6JS7Xz).

---

## What the Install Script Does

The install script:

1. Displays the Revelion ASCII art banner.
2. Detects your platform and CPU architecture.
3. Downloads the correct daemon binary from GitHub.
4. Checks for Docker and warns if it is not found.
5. If a token was provided: authenticates and starts the daemon automatically.

On first start the daemon also:

1. Registers itself under your account.
2. Checks for the sandbox Docker image (`ghcr.io/revelionai/revelion-sandbox`).
3. Pulls the image if it is not already present — this is a one-time download (~3–4 GB).
4. Opens a persistent WebSocket connection to Revelion and waits for work.

!!! tip "Pre-pull timing"
    The image pull happens in the background. The daemon registers as online immediately; it will accept scan work once the pull completes. On a fast connection the pull takes 2–3 minutes.

---

## What's Next

With the daemon online, you are ready to [run your first mission](first-mission.md).
