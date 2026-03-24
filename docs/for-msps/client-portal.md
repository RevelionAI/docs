# Client Portal

The client portal gives your clients direct access to their security findings, reports, and scan history — without requiring a Revelion account.

## How it works

Each client gets a unique portal URL. Access is protected by a PIN you set and share with the client. The portal is entirely self-contained: clients view only their own data and see only your branding.

Revelion is not mentioned anywhere in the portal. The experience is an extension of your service, not a third-party tool.

## What clients can view

| Section | Content |
|---|---|
| Overview | Summary of open findings, risk score, recent scan activity |
| Findings | Full finding list with severity, CVSS scores, affected assets, and remediation guidance |
| Reports | Downloadable PDF reports for all completed scans |
| Scan history | List of past scans with status and timestamps |

## Accessing the portal

Clients open the portal URL in any browser. They enter their PIN and land directly on the overview. No account creation, no email verification, no Revelion login.

The portal URL and PIN are displayed on the client management page. You control when to share them and with whom.

!!! tip "Generate portal links from the client management page"
    Open the **MSP** section, select a client, and copy the portal link from the **Client Portal** tab. Regenerate the PIN at any time to revoke access.

## Branding

The portal respects your [white-label configuration](white-label.md). If the client has a branding override configured, the portal uses that override. Your logo, colours, and company name appear throughout — clients see your brand, not Revelion's.

## Security

- Portal links are unique per client — sharing one client's link does not expose another client's data
- PINs can be regenerated at any time to revoke access
- All portal traffic is encrypted in transit
- Data is scoped at the database level via row-level security — the portal cannot retrieve data outside the client's scope

## Related pages

- [Client Management](client-management.md) — managing client records
- [White-Label](white-label.md) — configuring portal branding
- [Revelion for MSPs](index.md) — MSP overview
