# Platform Overview

Revelion is an autonomous AI penetration testing platform. It deploys a coordinated team of AI agents that think, plan, adapt, and exploit — producing the kind of findings a skilled human pentester would, at a fraction of the time and cost.

## What Revelion Is Not

Revelion is not a vulnerability scanner. Scanners enumerate known signatures. Revelion reasons about your attack surface, makes decisions, chains vulnerabilities, and exploits them to prove real-world impact.

The difference in practice:

| Vulnerability Scanner | Revelion |
|---|---|
| Matches request/response against signatures | Understands application logic and context |
| Reports potential issues | Confirms exploitability with proof-of-concept |
| Treats each finding in isolation | Chains low-severity bugs into critical impact |
| Produces a list | Produces an investigation |

## Multi-Agent Architecture

Revelion runs a root agent that coordinates strategy and spawns specialist sub-agents — each focused on a specific domain (authentication, injection, business logic, network services, etc.). Agents share findings, build on each other's work, and adapt when they hit dead ends. This parallelism means a Revelion scan covers more ground in less time than a sequential approach.

!!! tip
    Agents can be watched in real time via the Live Intel Feed. Every decision, tool call, and discovery is visible as it happens — no waiting for the scan to finish.

## Local Execution, Cloud Intelligence

The cloud brain coordinates strategy and prompt engineering. It never touches your targets directly.

A lightweight daemon runs on your machine and manages Docker containers that execute the actual tools. All scanning traffic originates from your network — your IP, your infrastructure, your rules of engagement.

This matters for:

- **Internal network testing** — connect a VPN config and Revelion reaches hosts that are never exposed to the internet
- **Compliance** — testing traffic is not routed through Revelion's servers
- **Rate limiting and WAF tuning** — your source IP, so you control how aggressive the scan is

## Supported Target Types

- Web applications
- APIs (REST, GraphQL)
- Internal networks
- Cloud infrastructure

## Where to Go Next

- [How It Works](how-it-works.md) — the four phases of a Revelion engagement
- [Architecture](architecture.md) — brain, daemon, and sandbox in detail
- [Tools](tools.md) — what's available in the execution sandbox
