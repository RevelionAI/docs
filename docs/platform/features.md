# Features

A reference of what Revelion provides across the platform.

---

## AI Engine

### Multi-Agent System

Revelion runs a root agent that coordinates the overall engagement strategy and spawns specialist sub-agents in parallel. Sub-agents focus on specific domains — injection testing, authentication analysis, network reconnaissance, privilege escalation — and report findings back to the root. The system scales effort based on what it discovers.

### Real Exploitation with Proof-of-Concept

Agents do not flag potential vulnerabilities and move on. Every finding Revelion reports has been tested for exploitability. Critical and high-severity findings include working payloads, exact HTTP requests, and output confirming the exploit landed.

### Vulnerability Chaining

Revelion correlates findings across agents. An information disclosure that leaks a username, combined with a rate-limit bypass on a login endpoint, becomes a credential brute-force path. A low-severity SSRF becomes an internal network pivot. Chained findings are surfaced as separate high-impact vulnerabilities with the full attack path documented.

### Confidence-Scored Findings

Every finding carries a confidence level alongside its CVSS score:

- **Confirmed** — exploit demonstrated with proof-of-concept
- **High confidence** — strong indicators, not fully exploited
- **Informational** — worth investigating, not confirmed exploitable

---

## Operational Controls

### Live Intel Feed

Watch the engagement in real time. Every agent decision, tool execution, and discovery streams to the Live Intel Feed as it happens. No waiting for scan completion to understand what's happening.

### Human-in-the-Loop

Enable manual approval mode to require operator sign-off before agents take high-risk actions — destructive tests, aggressive brute-forcing, or exploitation attempts. Revelion pauses and waits.

!!! tip
    Human-in-the-loop is recommended for production systems where false positives or scan noise could trigger alerts or cause disruption.

### Pre-Mission Instructions

Attach operator directives to any scan before it starts. Plain text instructions that agents read and follow — "focus on the admin panel", "do not test endpoints under /legacy", "treat the `/api/v2/export` endpoint as highest priority".

### Scheduled Recurring Scans

Set scans on a cron schedule — daily, weekly, or custom intervals. Useful for continuous security posture monitoring against a live application.

---

## Findings and Vulnerability Management

### Vulnerability Management Dashboard

All findings across all scans are tracked in a central vulnerability management view. Assets are automatically created from scan targets. Findings are deduplicated across scans so you see whether a vulnerability is new, persisting, or resolved.

Track status per finding:

- Open
- In progress
- Resolved
- Accepted risk

### 9 Compliance Frameworks

Map findings to compliance requirements automatically:

- SOC 2
- ISO 27001
- PCI DSS
- HIPAA
- GDPR
- NIST CSF
- CIS Controls
- OWASP Top 10
- PTES

---

## Reporting

### PDF Reports with White-Label Branding

Professional PDF reports generated automatically on scan completion. Pro plan supports custom logo and brand colours. MSP plan supports full white-label branding including custom report headers and client-specific templates.

See [Reports](reports.md) for full format details.

---

## Connectivity

### VPN Tunnelling for Internal Networks

Attach an OpenVPN or WireGuard config to a scan. The sandbox container establishes the tunnel before scanning begins, giving Revelion access to hosts that are never exposed to the internet — internal applications, staging environments, segmented networks.

---

## MSP and Multi-Client

### MSP Multi-Client Management

Manage multiple clients under a single Revelion account. Each client has isolated findings, reports, and scan history. Per-client white-label branding lets you deliver reports under your own brand or the client's brand independently.

See [MSP Management](../msp/overview.md) for setup.
