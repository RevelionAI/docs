# Errors

All `/v1/` API errors return a consistent JSON envelope:

```json
{
  "error": {
    "type": "not_found",
    "code": 404,
    "message": "Scan not found"
  }
}
```

## Error Types

| Code | Type | Description |
|------|------|-------------|
| `400` | `invalid_request` | Malformed request or invalid parameters |
| `401` | `authentication_error` | Missing or invalid API key |
| `402` | `payment_required` | Insufficient credits |
| `403` | `forbidden` | Key lacks required scope or IP blocked |
| `404` | `not_found` | Resource doesn't exist |
| `411` | `length_required` | `Content-Length` header required on POST/PUT/PATCH |
| `413` | `payload_too_large` | Request body exceeds 1 MB |
| `422` | `validation_error` | Request body failed validation |
| `429` | `rate_limit_exceeded` | Too many requests |
| `504` | `timeout` | Request processing timed out |

## Validation Errors

`422` responses include additional detail:

```json
{
  "error": {
    "type": "validation_error",
    "code": 422,
    "message": "value is not a valid email address",
    "param": "body.email",
    "details": [...]
  }
}
```

## Handling Errors

```python
response = requests.post(f"{BASE}/scans", headers=headers, json=data)

if response.status_code >= 400:
    error = response.json()["error"]
    if error["type"] == "rate_limit_exceeded":
        retry_after = int(response.headers["Retry-After"])
        time.sleep(retry_after)
    elif error["type"] == "payment_required":
        print("Top up credits at app.revelion.ai/membership")
    else:
        print(f"Error: {error['message']}")
```
