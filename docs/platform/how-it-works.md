# How It Works

A Revelion engagement runs in four phases. Each phase feeds directly into the next — scope defines what gets mapped, reconnaissance shapes exploitation, exploitation produces the evidence that goes into the report.

---

## Phase 1: Define Scope

Before a scan starts, you define the rules of engagement:

- **Target** — URL, IP range, domain, or CIDR block
- **Target type** — web application, API, network, cloud
- **Boundaries** — in-scope paths, hosts, or subnets
- **Exclusions** — hosts or endpoints to avoid entirely
- **Aggression level** — controls scan depth, request rate, and exploitation risk tolerance
- **Pre-mission instructions** — free-text operator directives (e.g. "focus on authentication", "do not test the payment endpoint")

!!! warning
    Always ensure you have written authorisation to test the target. Revelion is a real exploitation platform — not a passive scanner. It will attempt to exploit vulnerabilities it finds.

Scans can be run immediately or scheduled on a recurring basis. See [Scheduled Scans](../getting-started/scheduled-scans.md) for setup.

---

## Phase 2: AI Reconnaissance

The root agent begins by mapping the attack surface. It spawns specialist sub-agents and delegates work:

- **Technology fingerprinting** — web frameworks, server software, cloud services, CMS platforms
- **Endpoint discovery** — directory bruteforcing, parameter enumeration, API route discovery
- **Subdomain enumeration** — passive and active DNS reconnaissance
- **Service discovery** — for network targets: open ports, running services, version banners
- **Authentication surface** — login endpoints, OAuth flows, token handling patterns

Agents share discoveries through a shared context. A subdomain found by one agent immediately becomes a target for others. The surface grows as scanning progresses rather than being fixed at the start.

!!! tip
    The Live Intel Feed shows agent spawning, tool calls, and discoveries in real time. You can watch the attack surface being constructed without waiting for a completed report.

---

## Phase 3: Automated Exploitation

Revelion does not stop at detection. Once a potential vulnerability is identified, it attempts to confirm exploitability with working proof-of-concept evidence.

Exploitation capabilities include:

- SQL injection with data extraction
- Server-side template injection with RCE confirmation
- Authentication bypass and privilege escalation
- Subdomain takeover
- Business logic abuse
- SSRF with internal network pivoting
- Chaining low-severity findings into high-impact attack paths

**Example finding — Remote Code Execution via Template Injection (CVSS 9.8)**

An agent discovers `/artist.php` accepts user input reflected in a Twig template context. It confirms injection with a safe expression evaluation (`{{7*7}}`), then escalates to OS command execution via `{{['id']|filter('system')}}`. The finding is recorded with the full request/response chain, the injected payload, and the command output as proof-of-concept evidence.

When an exploitation path hits a dead end, agents adapt — trying alternative payloads, pivoting to a different vulnerability class, or flagging the finding as unconfirmed for manual review.

---

## Phase 4: Actionable Report

On scan completion, Revelion generates a full report automatically. Every finding includes:

- **CVSS score** — calculated from attack vector, complexity, privileges required, and impact
- **Confidence level** — confirmed exploit, strong indicator, or informational
- **Proof-of-concept** — exact requests, responses, and payloads
- **Remediation steps** — specific, actionable guidance (not generic advice)
- **Technical deep-dive** — how the vulnerability works and why it exists
- **Executive summary** — non-technical overview of risk exposure

Reports are available as PDF, JSON, and Markdown. PDF reports support white-label branding for client delivery.

See [Reports](reports.md) for format details and download options.

---

## Scan Modes

| Mode | Max Iterations | Depth | Use Case |
|---|---|---|---|
| Quick | 25 | Shallow | Rapid surface check, known targets |
| Standard | 60 | Moderate | Default for most engagements |
| Deep | 120 | Full | Thorough testing, production audits |

Network scans run equivalent modes with adjusted tool selection and higher iteration budgets for service enumeration.
