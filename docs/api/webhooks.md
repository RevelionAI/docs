# Webhooks

Receive real-time notifications when scans complete, findings are discovered, or reports are generated.

## Setup

### 1. Create a Webhook

=== "macOS / Linux"

    ```bash
    curl -X POST https://api.revelion.ai/api/webhooks -H "Authorization: Bearer YOUR_JWT" -H "Content-Type: application/json" -d '{"url":"https://your-server.com/webhooks/revelion","events":["scan.completed","finding.created"],"description":"Production webhook"}'
    ```

=== "Windows (cmd / PowerShell)"

    ```bash
    curl -X POST https://api.revelion.ai/api/webhooks -H "Authorization: Bearer YOUR_JWT" -H "Content-Type: application/json" -d "{\"url\":\"https://your-server.com/webhooks/revelion\",\"events\":[\"scan.completed\",\"finding.created\"],\"description\":\"Production webhook\"}"
    ```

!!! warning "One-Time Secret"
    The signing secret (`whsec_rv_...`) is shown only once. Store it securely.

### 2. Verify Signatures

Every webhook includes an `X-Revelion-Signature` header:

```
X-Revelion-Signature: t=1711700400,v1=5257a869e7ecb...
```

=== "Python"

    ```python
    import hmac
    import hashlib
    import time

    def verify_webhook(payload: bytes, signature_header: str, secret: str) -> bool:
        parts = dict(p.split("=", 1) for p in signature_header.split(","))
        timestamp = int(parts["t"])
        expected_sig = parts["v1"]

        # Reject if older than 5 minutes (replay protection)
        if abs(time.time() - timestamp) > 300:
            return False

        message = f"{timestamp}.{payload.decode()}"
        computed = hmac.new(
            secret.encode(), message.encode(), hashlib.sha256
        ).hexdigest()

        return hmac.compare_digest(computed, expected_sig)
    ```

=== "Node.js"

    ```javascript
    const crypto = require("crypto");

    function verifyWebhook(payload, signatureHeader, secret) {
      const parts = Object.fromEntries(
        signatureHeader.split(",").map(p => p.split("=", 2))
      );
      const timestamp = parseInt(parts.t);
      const expectedSig = parts.v1;

      // Reject if older than 5 minutes
      if (Math.abs(Date.now() / 1000 - timestamp) > 300) return false;

      const message = `${timestamp}.${payload}`;
      const computed = crypto
        .createHmac("sha256", secret)
        .update(message)
        .digest("hex");

      return crypto.timingSafeEqual(
        Buffer.from(computed), Buffer.from(expectedSig)
      );
    }
    ```

## Event Types

| Event | Trigger |
|-------|---------|
| `scan.created` | Scan submitted via API |
| `scan.started` | Scan execution begins |
| `scan.completed` | Scan finished successfully |
| `scan.failed` | Scan encountered an error |
| `scan.cancelled` | Scan cancelled by user |
| `finding.created` | New vulnerability discovered |
| `report.generated` | PDF/JSON report ready |

## Event Payload

```json
{
  "id": "evt_550e8400_scan.completed_1711700400123_a3f2",
  "type": "scan.completed",
  "api_version": "2026-03-29",
  "created_at": "2026-03-29T12:00:00Z",
  "data": {
    "scan_id": "550e8400-e29b-41d4-a716-446655440000",
    "status": "completed",
    "findings_count": 12
  }
}
```

## Retry Policy

Failed deliveries are retried with exponential backoff:

| Attempt | Delay |
|---------|-------|
| 1 | Immediate |
| 2 | 1 minute |
| 3 | 5 minutes |
| 4 | 30 minutes |
| 5 | 2 hours |
| 6 | 12 hours |
| 7 | 24 hours |

After 7 failed attempts, the delivery is marked as `exhausted`.

## Circuit Breaker

If a webhook endpoint fails 10 consecutive deliveries, it is automatically disabled. Re-enable it from the dashboard or via `PATCH /api/webhooks/{id}` with `{"active": true}`.

## Testing

Send a test event to verify your endpoint:

```bash
curl -X POST https://api.revelion.ai/api/webhooks/{id}/test -H "Authorization: Bearer YOUR_JWT"
```
