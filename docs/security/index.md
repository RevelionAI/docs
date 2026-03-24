# Security

Revelion is built by pentesters for pentesters. Security is not an afterthought — the platform architecture was designed from the ground up to ensure that testing infrastructure is isolated, data is protected, and access is scoped correctly at every layer.

## Infrastructure

Revelion runs on SOC 2 Type II certified infrastructure:

- **Supabase** (PostgreSQL database, file storage) — EU region (eu-west-1), SOC 2 Type II
- **Fly.io** (compute, agent orchestration) — SOC 2 Type II
- **Upstash** (Redis, ephemeral scan state) — SOC 2 compliant

All infrastructure providers are subject to ongoing compliance programmes and independent audits.

## Testing traffic never touches Revelion servers

This is the most important architectural decision in Revelion. When an agent executes a scan, all network traffic flows **from your daemon directly to the target**. The daemon runs on your machine or your infrastructure. Revelion's cloud servers orchestrate the agents — they do not proxy, relay, or inspect the actual testing traffic.

The practical effect: your target's network never communicates with Revelion's servers. Only findings, metadata, and agent decisions are transmitted.

## Database security

Every table in the Revelion database has row-level security (RLS) enabled. No query — from the frontend, the API, or internal tooling — can retrieve a row that does not belong to the authenticated user's organisation.

RLS is enforced at the PostgreSQL level. It cannot be bypassed by application-layer bugs.

## Encryption

- All data in transit is encrypted with TLS 1.2+
- Data at rest is encrypted by Supabase Storage and PostgreSQL
- API keys and credentials are never stored by Revelion (see [Data Handling](data-handling.md))

## Responsible disclosure

If you discover a security vulnerability in Revelion, please report it to [security@revelion.ai](mailto:security@revelion.ai). We operate a responsible disclosure programme and will respond within 48 hours.

## Related pages

- [Data Handling](data-handling.md) — what is stored and where
- [GDPR](gdpr.md) — data protection and compliance
- [Legal](legal.md) — authorisation requirements and acceptable use
