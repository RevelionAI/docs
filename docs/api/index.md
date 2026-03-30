# API Reference

Revelion provides a RESTful API for programmatic access to scanning, findings, assets, and reports. Use it to integrate automated pentesting into your CI/CD pipelines, build custom dashboards, or connect with third-party security tools.

!!! note "Plan Requirement"
    API access requires a **Pro** or **MSP** subscription. [Upgrade your plan](https://app.revelion.ai/settings?section=membership) to get started.

## Base URL

```
https://api.revelion.ai/v1
```

## Quick Start

Get scanning in under 5 minutes:

### 1. Create an API Key

In the Revelion dashboard, go to **Settings > API Keys** and create a new key with `read` and `write` scopes. Copy the key immediately — it's shown only once.

### 2. Start a Scan

```bash
curl -X POST https://api.revelion.ai/v1/scans \
  -H "Authorization: Bearer rvn_live_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Example Scan",
    "target": {"type": "url", "url": "https://example.com"},
    "scan_mode": "quick"
  }'
```

Response:
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "status": "pending",
  "name": "Example Scan",
  "target": {"type": "url", "url": "https://example.com"},
  "scan_mode": "quick",
  "created_at": "2026-03-29T12:00:00Z"
}
```

### 3. Check Status

```bash
curl https://api.revelion.ai/v1/scans/550e8400-e29b-41d4-a716-446655440000 \
  -H "Authorization: Bearer rvn_live_your_key_here"
```

### 4. Get Findings

```bash
curl https://api.revelion.ai/v1/findings/scan/550e8400-e29b-41d4-a716-446655440000 \
  -H "Authorization: Bearer rvn_live_your_key_here"
```

## Response Format

All list endpoints return paginated responses:

```json
{
  "data": [...],
  "has_more": true,
  "limit": 20,
  "offset": 0
}
```

## SDK Examples

=== "Python"

    ```python
    import requests

    API_KEY = "rvn_live_your_key_here"
    BASE = "https://api.revelion.ai/v1"
    headers = {"Authorization": f"Bearer {API_KEY}"}

    # Create scan
    scan = requests.post(f"{BASE}/scans", headers=headers, json={
        "name": "API Scan",
        "target": {"type": "url", "url": "https://example.com"},
        "scan_mode": "normal",
    }).json()

    # Poll until complete
    import time
    while True:
        status = requests.get(f"{BASE}/scans/{scan['id']}", headers=headers).json()
        if status["status"] in ("completed", "failed"):
            break
        time.sleep(30)

    # Get findings
    findings = requests.get(f"{BASE}/findings/scan/{scan['id']}", headers=headers).json()
    for f in findings["data"]:
        print(f"{f['severity']}: {f['finding_type']} — {f['target']}")
    ```

=== "TypeScript"

    ```typescript
    const API_KEY = "rvn_live_your_key_here";
    const BASE = "https://api.revelion.ai/v1";
    const headers = { Authorization: `Bearer ${API_KEY}` };

    // Create scan
    const scan = await fetch(`${BASE}/scans`, {
      method: "POST",
      headers: { ...headers, "Content-Type": "application/json" },
      body: JSON.stringify({
        name: "API Scan",
        target: { type: "url", url: "https://example.com" },
        scan_mode: "normal",
      }),
    }).then(r => r.json());

    // Poll until complete
    let status = "pending";
    while (!["completed", "failed"].includes(status)) {
      await new Promise(r => setTimeout(r, 30000));
      const res = await fetch(`${BASE}/scans/${scan.id}`, { headers }).then(r => r.json());
      status = res.status;
    }

    // Get findings
    const findings = await fetch(`${BASE}/findings/scan/${scan.id}`, { headers }).then(r => r.json());
    findings.data.forEach(f => console.log(`${f.severity}: ${f.finding_type}`));
    ```

=== "curl"

    ```bash
    # Create scan
    SCAN_ID=$(curl -s -X POST "$BASE/scans" \
      -H "Authorization: Bearer $API_KEY" \
      -H "Content-Type: application/json" \
      -d '{"name":"Scan","target":{"type":"url","url":"https://example.com"},"scan_mode":"quick"}' \
      | jq -r '.id')

    # Wait for completion
    while [ "$(curl -s "$BASE/scans/$SCAN_ID" -H "Authorization: Bearer $API_KEY" | jq -r '.status')" != "completed" ]; do
      sleep 30
    done

    # Get findings
    curl -s "$BASE/findings/scan/$SCAN_ID" -H "Authorization: Bearer $API_KEY" | jq '.data[]'
    ```

## Interactive Explorer

The full API specification is available as an interactive explorer at:

- **Swagger UI:** [api.revelion.ai/docs](https://api.revelion.ai/docs)
- **ReDoc:** [api.revelion.ai/redoc](https://api.revelion.ai/redoc)
