# Rate Limits

API access requires a **Pro** or **MSP** subscription. Free tier accounts cannot create API keys or access `/v1/` endpoints.

Requests are rate-limited per API key, with limits based on your plan.

## Limits by Plan

| Plan | Read | Write | Critical |
|------|------|-------|----------|

| Pro | 300/min | 60/min | 20/min |
| MSP | 600/min | 120/min | 40/min |
| Enterprise | 1,000/min | 300/min | 100/min |

**Tier classification:**

- **Read:** All `GET` requests
- **Write:** `POST`, `PUT`, `PATCH`, `DELETE` requests
- **Critical:** Scan creation, report regeneration, key management

## Response Headers

Every response includes rate limit headers:

```
X-RateLimit-Limit: 300
X-RateLimit-Remaining: 299
X-RateLimit-Reset: 1711700460
Retry-After: 45
```

| Header | Description |
|--------|-------------|
| `X-RateLimit-Limit` | Maximum requests per window |
| `X-RateLimit-Remaining` | Requests remaining |
| `X-RateLimit-Reset` | Unix timestamp when window resets |
| `Retry-After` | Seconds to wait (only on `429`) |

## Other Headers

| Header | Description |
|--------|-------------|
| `X-Request-Id` | Unique request ID for support/debugging |
| `Revelion-Api-Version` | API version date (`2026-03-29`) |
| `Idempotent-Replayed` | `true` if returning cached idempotent response |

## Handling 429s

```python
import time

def api_call_with_retry(url, headers, max_retries=3):
    for attempt in range(max_retries):
        response = requests.get(url, headers=headers)
        if response.status_code == 429:
            retry_after = int(response.headers.get("Retry-After", 60))
            time.sleep(retry_after)
            continue
        return response
    raise Exception("Rate limited after max retries")
```
