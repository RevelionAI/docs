# Authentication

## API Keys

All API requests require a Bearer token. API keys are prefixed with `rvn_live_` and scoped to your organization.

```bash
curl https://api.revelion.ai/v1/scans \
  -H "Authorization: Bearer rvn_live_a3f2bc1..."
```

### Creating Keys

Create API keys in the Revelion dashboard under **Settings > API Keys**, or via the management API:

```bash
curl -X POST https://api.revelion.ai/api/keys \
  -H "Authorization: Bearer YOUR_SUPABASE_JWT" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "CI/CD Pipeline",
    "scopes": ["read", "write"],
    "expires_at": "2027-03-29T00:00:00Z"
  }'
```

!!! warning "One-Time Display"
    The full API key is shown **only once** when created. Store it securely — it cannot be retrieved again.

### Scopes

| Scope | Permissions |
|-------|-------------|
| `read` | View scans, findings, assets, reports, usage |
| `write` | Create scans, update findings, manage assets (includes `read`) |
| `admin` | Manage API keys, webhooks, org settings (includes `read` + `write`) |

### Key Rotation

Rotate a key atomically — the old key is revoked and a new one created in a single transaction:

```bash
curl -X POST https://api.revelion.ai/api/keys/{key_id}/rotate \
  -H "Authorization: Bearer YOUR_SUPABASE_JWT"
```

### IP Allowlisting

Restrict API key usage to specific IP ranges (up to 20 CIDRs):

```json
{
  "name": "Production Only",
  "scopes": ["read", "write"],
  "ip_allowlist": ["203.0.113.0/24", "198.51.100.42/32"]
}
```

### Security Best Practices

- Store keys in environment variables or a secrets manager — never in code
- Use the minimum required scopes
- Set expiration dates for CI/CD keys
- Rotate keys immediately if compromised
- Use IP allowlisting for production keys

## Error Responses

| Status | Meaning |
|--------|---------|
| `401` | Missing or invalid API key |
| `403` | Key lacks required scope, or IP not in allowlist |
| `402` | Insufficient credits |
