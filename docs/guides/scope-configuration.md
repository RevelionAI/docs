# Scope Configuration

Scope configuration tells Revelion exactly what to test and what to leave alone. A well-defined scope keeps the agent focused, prevents unintended actions against out-of-bounds systems, and ensures your results are relevant.

---

## Target Types

Revelion accepts four target types when creating a mission:

| Type | Example | Notes |
|---|---|---|
| Web Application | `https://app.example.com` | Full URL including scheme |
| API Endpoint | `https://api.example.com/v2` | REST or GraphQL base path |
| IP Address | `192.168.1.10` | Single host |
| Network CIDR | `10.0.0.0/24` | Requires Network scan mode |

Enter one primary target per mission. For broader coverage across multiple targets, create separate missions or use the [Scheduled Scans](scheduled-scans.md) feature to run them automatically.

---

## Scope Boundaries

### In Scope

Everything reachable from the primary target is considered in scope by default. This includes:

- Subdomains discovered during reconnaissance (web mode)
- Open ports and services on the target host (network mode)
- Linked pages and API routes crawled from the entry point

### Out of Scope

You can restrict what Revelion tests by defining exclusion patterns. Common use cases:

- Exclude third-party services embedded in your app (payment processors, analytics)
- Protect production databases or admin interfaces during a dev-environment test
- Limit testing to specific paths or IP ranges

---

## Exclusion Patterns

Exclusions are entered as path patterns or IP expressions during mission setup.

**Path exclusions** (web mode):

```
/admin/*
/api/internal/*
/health
```

**Host/IP exclusions** (network mode):

```
192.168.1.1
10.0.0.50-10.0.0.60
```

Patterns support `*` as a wildcard. Paths are matched against the full URL after the hostname. IP ranges use dash notation.

!!! warning "Legal Responsibility"
    Only test systems you own or have **written authorisation** to test. Revelion is a powerful autonomous agent — running it against systems without permission may violate computer misuse laws in your jurisdiction. Always obtain explicit written consent from the system owner before starting a mission.

---

## Aggression Levels

Revelion offers three scan modes that control depth, duration, and the intensity of testing activity:

### Quick
- Duration: ~10–20 minutes
- Lightweight reconnaissance and passive analysis
- Minimal active exploitation attempts
- Suitable for rapid triage or CI/CD integration

### Standard
- Duration: ~30–60 minutes
- Full reconnaissance, active vulnerability testing, and exploitation attempts
- Balanced coverage without exhaustive brute-force

### Deep
- Duration: ~2–4 hours
- Exhaustive testing across all discovered attack surface
- Aggressive payload delivery, chained exploitation, and post-exploitation steps
- Recommended for pre-release or compliance-driven assessments

!!! info "Credit Usage"
    Deeper scan modes consume significantly more credits. Check your credit balance before starting a Deep scan. See the [Billing](../account/billing.md) page for credit details.

---

## Related

- [Running a Mission](../quickstart/first-mission.md)
- [Scheduled Scans](scheduled-scans.md)
- [VPN Tunnelling](vpn-tunnelling.md)
