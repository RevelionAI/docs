# Scans

## Create a Scan

`POST /v1/scans`

Requires `write` scope. Returns `202 Accepted` — the scan runs asynchronously.

### Request

```json
{
  "name": "Weekly Scan",
  "target": {"type": "url", "url": "https://app.example.com"},
  "scan_mode": "normal",
  "scan_type": "web",
  "instructions": "Focus on authentication flows",
  "compliance_standard": "soc2",
  "credentials": [
    {
      "credential_type": "username_password",
      "label": "Admin",
      "username": "admin@example.com",
      "password": "testpass123",
      "login_url": "/login"
    }
  ]
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Human-readable scan name |
| `target` | object | Yes | `{type: "url"\|"ip"\|"repo", url\|ip\|repo: "..."}` |
| `scan_mode` | string | No | `quick` (25 iter), `normal` (60 iter), `deep` (120 iter). Default: `normal` |
| `scan_type` | string | No | `web`, `network`, or `bounty`. Default: `web` |
| `instructions` | string | No | Custom instructions for the AI agent (Pro+) |
| `compliance_standard` | string | No | `soc2`, `iso27001`, `pci_dss` (Pro+) |
| `client_id` | string | No | Associate with an MSP client (MSP plan) |
| `credentials` | array | No | Up to 10 credential sets for authenticated scanning. See below. |

### Authenticated Scanning

Provide credentials to unlock authenticated testing — IDOR, privilege escalation, broken access control, and session management vulnerabilities that are invisible to unauthenticated scans.

Credentials are encrypted at rest and automatically deleted after the scan completes. They are never returned by any API endpoint.

Each credential object requires a `credential_type` and the relevant fields:

**Username / Password**

```json
{
  "credential_type": "username_password",
  "label": "Admin",
  "username": "admin@example.com",
  "password": "testpass123",
  "login_url": "/login"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `username` | string | Yes | Login username or email |
| `password` | string | Yes | Login password |
| `login_url` | string | No | Login page path (helps the agent find the login form) |
| `label` | string | No | Role label (e.g. "Admin", "Regular User") |

**Bearer Token**

```json
{
  "credential_type": "bearer_token",
  "label": "API Token",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "header_name": "Authorization"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `token` | string | Yes | The token value |
| `header_name` | string | No | Header name. Default: `Authorization` |

**Cookie**

```json
{
  "credential_type": "cookie",
  "label": "Session",
  "cookie_string": "session=abc123; csrf_token=xyz789"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `cookie_string` | string | Yes | Cookie string to inject |

**Custom Headers**

```json
{
  "credential_type": "custom_headers",
  "label": "API Key Headers",
  "headers": [
    {"name": "X-API-Key", "value": "sk_live_abc123"},
    {"name": "X-Tenant-ID", "value": "org_456"}
  ]
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `headers` | array | Yes | Array of `{name, value}` header objects |

**Multi-role testing:** Provide multiple credential sets with different privilege levels (e.g. Admin + Regular User). The agent will test each role separately and compare access to detect privilege escalation and broken access control.

## List Scans

`GET /v1/scans?limit=20&offset=0&status=completed`

Requires `read` scope.

| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | int | Max items (1-100, default 20) |
| `offset` | int | Pagination offset |
| `status` | string | Filter: `pending`, `running`, `completed`, `failed`, `cancelled` |

## Get Scan

`GET /v1/scans/{scan_id}`

Requires `read` scope.

## Cancel Scan

`POST /v1/scans/{scan_id}/cancel`

Requires `write` scope. Can cancel scans in `pending`, `running`, or `paused` state.

## List Agents

`GET /v1/scans/{scan_id}/agents?limit=50&offset=0`

Requires `read` scope. Returns the AI agents that worked on the scan.

## List Events

`GET /v1/scans/{scan_id}/events?limit=200&offset=0`

Requires `read` scope. Returns real-time scan events (agent thoughts, tool executions, status changes).
