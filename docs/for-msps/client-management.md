# Client Management

The MSP plan supports up to 25 client accounts, each with independent targets, scan history, vulnerability tracking, and report branding.

## Adding clients

Navigate to the **MSP** section and click **New Client**. Each client record stores:

- **Name** — displayed in reports and the client portal
- **Contact information** — primary contact name and email
- **Associated targets** — domains, IP ranges, and CIDR blocks scoped to that client

Clients are isolated from one another. A scan attributed to one client cannot surface in another client's portal or reports.

## Associating scans with clients

When creating a new scan, select the client from the client dropdown. Revelion automatically attributes findings, reports, and scan history to that client. The association is permanent — scans cannot be reassigned after creation.

## Vulnerability management per client

Every client has its own vulnerability management view. Findings are tracked as assets and asset findings, with status transitions (open → in_progress → resolved → accepted_risk) maintained independently per client.

This means you can deliver a persistent vulnerability backlog to each client, track remediation over time, and demonstrate security improvement across engagements.

!!! info "Vulnerability history"
    Status changes are recorded automatically. When a finding moves from `open` to `resolved`, Revelion logs the transition with a timestamp — useful for compliance evidence and client reporting.

## Per-client branding overrides

Each client supports a branding override that takes precedence over your default white-label configuration. Set a different logo, colour scheme, or footer text per client to match their brand expectations.

See [White-Label](white-label.md) for configuration details.

## Removing clients

Clients can be deleted from the client settings page. Deleting a client does not delete associated scans, findings, or reports — those remain in your account and are accessible from the main scan and report views.

## Related pages

- [Client Portal](client-portal.md) — sharing results with clients
- [White-Label](white-label.md) — branding per client
- [Revelion for MSPs](index.md) — MSP overview
