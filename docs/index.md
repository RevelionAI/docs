# Revelion

Revelion is an autonomous AI penetration testing platform. Intelligent agents perform real security assessments — reconnaissance, exploitation, and reporting — with proof-of-concept evidence for every finding.

No waiting weeks for a consultant's calendar. No static PDFs that go stale the moment they're delivered. Revelion runs continuously, produces actionable findings, and lets you retest after remediation without scheduling a full engagement.

---

## Quick Start

```
revelion@ai $ # Three steps to your first pentest
```

**1. Create an account**
Sign up at [app.revelion.ai](https://app.revelion.ai). Your account comes with free credits to run your first scan.

**2. Install the daemon**
The daemon runs on your machine, manages the sandbox container, and connects securely to the Revelion platform. [Install it now →](getting-started/installation.md)

**3. Launch a mission**
Point Revelion at a target, select a scan mode, and let the agents work. [Run your first mission →](getting-started/first-mission.md)

---

## Traditional Pentest vs Revelion

| | Traditional Pentest | Revelion |
|---|---|---|
| **Cost** | £15,000 – £30,000 | From £10 |
| **Frequency** | Yearly | 24/7, on demand |
| **Time to results** | 2–4 weeks | Hours |
| **Delivery** | Static PDF | Interactive findings dashboard |
| **Retesting** | Full price engagement | Top up credits and retest |
| **Scope changes** | Requires rebooking | Edit and relaunch in seconds |
| **Coverage** | One snapshot in time | Continuous, scheduled or ad hoc |

!!! tip "Not a replacement for everything"
    Revelion covers automated offensive testing at scale. For compliance engagements requiring a signed human report, use the generated PDF as supporting evidence alongside your human pentest.

---

## What the Agents Do

Revelion spawns a coordinated network of agents inside an isolated sandbox. Each agent has a defined role — reconnaissance, web exploitation, network scanning, privilege escalation — and they coordinate automatically to build a complete picture of the target's attack surface.

Every finding comes with:

- CVSS score
- Proof-of-concept evidence (screenshots, payloads, responses)
- Remediation guidance
- A unique reference ID (e.g. `VLN-001`)

---

## Key Sections

- [Getting Started](getting-started/index.md) — requirements, installation, first mission
- [Scan Modes](scan-modes.md) — Quick, Standard, Deep
- [Findings & Reports](reports.md) — CVSS scoring, PDF export, white-label
- [Vulnerability Management](vuln-management.md) — asset tracking, deduplication, history
- [MSP & Teams](msp.md) — multi-client workspaces, per-client branding
- [Daemon](daemon.md) — architecture, configuration, troubleshooting

---

## Community & Links

- [Discord](https://discord.gg/fg6JS7Xz) — questions, feedback, release notes
- [X / Twitter](https://x.com/revelionai) — announcements
- [LinkedIn](https://www.linkedin.com/company/revelionai) — updates
- [GitHub](https://github.com/RevelionAI) — open components and the daemon
