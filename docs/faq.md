# Frequently Asked Questions

## What makes Revelion different from vulnerability scanners?

Scanners check for known signatures. Revelion thinks. It spawns specialist AI agents that chain vulnerabilities together, adapt their approach based on what they find, and exploit weaknesses to prove they're real. Every finding comes with proof-of-concept evidence — not a theoretical risk rating.

## Does Revelion replace human pentesters?

No. It's a tool for security professionals to handle repetitive work — reconnaissance, common vulnerability testing, report generation — so they can focus on complex logic flaws and business context that require human judgment.

## Why does the daemon run locally?

The Docker agent ensures all testing traffic originates from your infrastructure. The cloud brain coordinates strategy and AI reasoning only — it never touches your targets. This means your firewall rules, VPN access, and network position are preserved.

## How much does it cost compared to traditional pentesting?

A typical external pentest costs £10,000–20,000 and takes weeks to schedule. Revelion lets you test on demand from £10. You only pay for the AI compute you use — no retainer fees, no minimum commitments.

## Is it legal?

Revelion is a penetration testing tool, like Nmap or Burp Suite. You must only test systems you own or have explicit written authorisation to test. The platform includes scope enforcement to help prevent accidental out-of-scope testing.

!!! warning "Authorisation required"
    Unauthorised testing is illegal in most jurisdictions. Always obtain written permission from the system owner before running any scan.

## What types of targets can I test?

Web applications, REST/GraphQL APIs, internal networks (via VPN tunnelling), external infrastructure, and cloud services. Both authenticated and unauthenticated testing are supported.

## How long does a scan take?

| Mode | Typical duration |
|------|-----------------|
| Quick | 15–30 minutes |
| Standard | 1–2 hours |
| Deep | Several hours (target-dependent) |

Duration depends on the target's complexity and attack surface.

## What tools does Revelion use?

Industry-standard pentesting tools including Nmap, Nuclei, SQLMap, Feroxbuster, Playwright, Subfinder, httpx, and ffuf — all running in an isolated Docker sandbox on your machine.

## Can I control what the AI does?

Yes. Human-in-the-loop mode lets you approve or deny every action before execution. You can also provide pre-mission instructions and send operator directives mid-scan to steer the agent's focus.

## How are findings scored?

Every finding is assigned a CVSS 3.1 score based on the actual exploitability and impact demonstrated. Findings include CVE references where applicable, detailed reproduction steps, and remediation guidance.

## Is my data secure?

Findings are stored in Supabase (SOC 2 Type II certified) with row-level security isolating each organisation's data. Testing traffic never passes through Revelion's servers. All data is encrypted in transit and at rest.

!!! info "Data isolation"
    Each organisation's findings, agents, and scan data are strictly isolated at the database level via row-level security policies. No cross-tenant data access is possible.

## Can I use Revelion for compliance testing?

Yes. Pro and MSP plans include 9 compliance frameworks (OWASP Top 10, PCI DSS, ISO 27001, SOC 2, NIST CSF, HIPAA, Cyber Essentials, CIS Controls, GDPR technical controls). Findings are mapped to relevant controls in the report.

## What happens if I run out of credits mid-scan?

The mission pauses automatically. Top up your credits and resume — the scan continues exactly where it left off. No work is lost.
