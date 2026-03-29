# Findings

## List Findings

`GET /v1/findings/scan/{scan_id}?severity=critical&status=open`

Requires `read` scope.

| Parameter | Type | Description |
|-----------|------|-------------|
| `severity` | string | Filter: `critical`, `high`, `medium`, `low` |
| `status` | string | Filter: `open`, `mitigated`, `accepted` |
| `limit` | int | Max items (1-100, default 50) |
| `offset` | int | Pagination offset |

### Response

```json
{
  "data": [
    {
      "id": "...",
      "scan_id": "...",
      "severity": "high",
      "finding_type": "SQL Injection",
      "target": "https://app.example.com/api/users",
      "description": "The user search endpoint is vulnerable to SQL injection...",
      "steps": "1. Navigate to /api/users?q=...",
      "impact": "Full database read access",
      "remediation": "Use parameterized queries",
      "affected_endpoints": ["/api/users"],
      "evidence_artifacts": ["screenshot_001.png"],
      "status": "open",
      "validated": true,
      "created_at": "2026-03-29T12:30:00Z"
    }
  ],
  "has_more": false,
  "limit": 50,
  "offset": 0
}
```

## Get Finding

`GET /v1/findings/{finding_id}`

Requires `read` scope.

## Update Finding

`PATCH /v1/findings/{finding_id}`

Requires `write` scope.

```json
{
  "status": "mitigated",
  "validated": true,
  "validation_evidence": "Fix deployed in PR #142, verified with re-scan"
}
```
