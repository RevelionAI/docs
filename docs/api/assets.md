# Assets

## Create Asset

`POST /v1/assets`

Requires `write` scope.

```json
{
  "name": "Production API",
  "asset_type": "web_app",
  "target": {"type": "url", "url": "https://api.example.com"},
  "environment": "production",
  "criticality": "high",
  "tags": ["api", "customer-facing"]
}
```

| Field | Type | Values |
|-------|------|--------|
| `asset_type` | string | `web_app`, `network_host`, `ip_range`, `api_endpoint`, `source_code` |
| `environment` | string | `production`, `staging`, `development` |
| `criticality` | string | `critical`, `high`, `medium`, `low` |

## List Assets

`GET /v1/assets?asset_type=web_app&criticality=high&limit=50`

Requires `read` scope.

## Get Asset

`GET /v1/assets/{asset_id}`

## Asset Findings

`GET /v1/assets/{asset_id}/findings?severity=critical&status=open`

## Asset Scan History

`GET /v1/assets/{asset_id}/scans?limit=20`
