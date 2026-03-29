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
  "compliance_standard": "soc2"
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

### Idempotency

Pass an `Idempotency-Key` header to prevent duplicate scans on retry:

```bash
curl -X POST /v1/scans \
  -H "Idempotency-Key: my-unique-key-123" \
  ...
```

If the same key is sent within 24 hours, the original scan is returned with an `Idempotent-Replayed: true` header.

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
