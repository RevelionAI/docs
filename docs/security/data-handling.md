# Data Handling

This page describes what data Revelion stores, where it is stored, and how it is protected.

## What is stored

| Data type | Stored | Notes |
|---|---|---|
| Scan configuration | Yes | Target, scan type, preset, VPN config reference |
| Agent decisions | Yes | LLM reasoning steps, tool calls, agent messages |
| Findings | Yes | Vulnerability details, CVSS scores, affected assets, remediation guidance |
| PDF reports | Yes | Encrypted at rest in Supabase Storage |
| Credentials and API keys | **No** | Never stored by Revelion |
| Testing traffic | **No** | Traffic flows daemon-to-target, not through Revelion servers |
| Raw HTTP request/response bodies | No | Only agent-summarised findings are persisted |

## Where data is stored

All persistent data is stored in **Supabase PostgreSQL**, hosted in the **EU West (eu-west-1)** region. This region covers Ireland and is subject to EU data protection law.

Supabase is SOC 2 Type II certified. Full details are available at [supabase.com/security](https://supabase.com/security).

Ephemeral scan state (active agent context, scan queues) is stored in **Upstash Redis** and is not persisted beyond scan completion.

## Row-level security

Every table in the Revelion database has row-level security (RLS) enforced at the PostgreSQL level. Every query — regardless of source — is automatically scoped to the authenticated user's organisation.

An application-layer bug cannot cause data from one organisation to appear in another's context. RLS is enforced before any query result is returned to the application.

## Credentials and secrets

Revelion never asks for, stores, or transmits credentials or API keys. If a scan requires authentication (e.g., testing a login form), those credentials are entered as pre-mission instructions and used only during the scan session — they are not persisted to the database.

## Report storage

PDF reports are stored in Supabase Storage, encrypted at rest. Access is controlled by storage RLS policies tied to the authenticated user's organisation. Reports are retained for:

- **Free plan**: 30 days
- **Pro and MSP plans**: 1 year
- **Enterprise**: configurable

## Deletion

Users can delete scans, findings, and reports at any time from the Revelion interface. Deletion is permanent and irreversible. Account deletion removes all associated data — see [GDPR](gdpr.md) for the right to erasure.

## Related pages

- [Security Overview](index.md) — infrastructure and architecture
- [GDPR](gdpr.md) — data protection rights and sub-processors
- [Legal](legal.md) — acceptable use
