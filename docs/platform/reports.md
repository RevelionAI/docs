# Reports

Revelion generates a full report automatically when a scan completes. No manual compilation, no copy-pasting from a tool output. The report is ready to share the moment the scan finishes.

---

## Formats

Reports are available in three formats:

| Format | Use Case |
|---|---|
| PDF | Client delivery, executive review, compliance audit |
| JSON | API access, custom tooling, SIEM integration |
| Markdown | Internal wikis, Git-tracked documentation, developer review |

All three formats are generated simultaneously on scan completion. You can download any format from the Reports page or from the individual Mission detail page.

---

## PDF Report Structure

The PDF report is structured for both technical and non-technical readers.

**Executive Summary**
High-level risk posture, total findings by severity, most critical issues, and recommended immediate actions. Written in plain language for non-technical stakeholders.

**Methodology**
Scope definition, target types tested, tools used, scan duration, and aggression level. Provides context for auditors and reviewers.

**Findings**
Each finding includes:

- Title and severity classification
- CVSS v3.1 score with vector string
- Confidence level (confirmed, high confidence, informational)
- Affected asset and endpoint
- Description of the vulnerability and how it works
- Proof-of-concept — exact HTTP requests, responses, payloads, and output
- Remediation steps — specific and actionable, not generic advice
- Compliance mapping (if applicable)

**Appendices**
Raw tool output, full request/response logs, and supplementary technical evidence linked from findings.

---

## White-Label Branding

PDF reports support custom branding for client delivery.

| Plan | Branding Capabilities |
|---|---|
| Pro | Custom logo, primary and accent colours |
| MSP | Full white-label — logo, colours, report header, custom footer, per-client overrides |

!!! tip
    MSP users can set default branding at the organisation level and override it per client. This lets you deliver reports branded as the client's own security team or under your MSP brand depending on the engagement.

Branding is configured in **Settings → Report Branding**. MSP per-client branding is configured in **MSP → Clients → [Client] → Branding**.

---

## Compliance Mapping

Findings can be mapped to compliance framework requirements. Revelion supports:

- SOC 2 (Security, Availability, Confidentiality)
- ISO 27001
- PCI DSS
- HIPAA
- GDPR
- NIST CSF
- CIS Controls
- OWASP Top 10
- PTES

Compliance mapping is included in both the PDF report and the JSON export, making it straightforward to feed findings into a GRC tool or audit evidence package.

---

## Accessing Reports

**From the Reports page**: Lists all generated reports across all scans with filter by date, severity, and status.

**From a Mission**: Navigate to the mission detail page → Reports tab → download any format.

**Via API**: Reports are accessible through the Revelion API if you need to pull them programmatically into another system.

!!! tip
    If a scan ran but the report is missing or stale, use the **Regenerate Report** option on the Mission detail page. This re-runs the report generator against the current findings without re-running the scan.

---

## Report Retention

Reports are stored in Supabase Storage with row-level security. Only members of your organisation can access your reports. Reports are retained indefinitely — there is no automatic deletion.
