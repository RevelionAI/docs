# Compliance Frameworks

Revelion can map findings directly to the controls of nine industry-recognised compliance frameworks. When a framework is selected during mission setup, every finding is tagged to the relevant control reference — and the generated PDF report includes a dedicated compliance mapping section.

!!! tip "Pro Feature"
    Compliance framework mapping is available on **Pro** and **MSP** plans. Upgrade from the [Membership](../account/membership.md) page.

---

## Supported Frameworks

| Framework | Description |
|---|---|
| **OWASP Top 10** | The ten most critical web application security risks |
| **PCI DSS** | Payment Card Industry Data Security Standard |
| **ISO 27001** | International standard for information security management |
| **SOC 2** | Trust Services Criteria for security, availability, and confidentiality |
| **NIST CSF** | NIST Cybersecurity Framework (Identify, Protect, Detect, Respond, Recover) |
| **HIPAA** | US Health Insurance Portability and Accountability Act (technical safeguards) |
| **Cyber Essentials** | UK government-backed baseline security certification scheme |
| **CIS Controls** | Center for Internet Security Critical Security Controls |
| **GDPR (Technical)** | General Data Protection Regulation — technical and organisational measures |

---

## How It Works

### 1. Select a Framework at Mission Setup

During mission creation, expand the **Compliance** section and choose one or more frameworks from the list. You can select multiple frameworks for a single mission.

### 2. Findings Are Mapped Automatically

As Revelion discovers vulnerabilities, each finding is classified and tagged with the relevant control references from your selected frameworks. For example:

- An SQL injection finding maps to **OWASP A03:2021**, **PCI DSS 6.3.1**, and **CIS Control 16**
- A missing security header maps to **OWASP A05:2021** and **Cyber Essentials — Secure Configuration**

### 3. Review in the Report

The PDF report includes a **Compliance Mapping** section after the findings summary. It lists each selected framework, the controls assessed, and the findings that relate to each control. Controls with no associated findings are marked as not assessed (not as passed — see the note below).

---

## In the Findings Interface

On the **Vulnerabilities** page, you can filter findings by framework and control. This is useful when preparing evidence for an audit or reviewing the security posture of a specific control domain.

---

## Limitations

!!! info "Compliance Mapping vs. Formal Audit"
    Compliance mapping in Revelion demonstrates technical due diligence — it shows which controls were tested and what was found. It does not replace a formal compliance audit conducted by an accredited assessor. Frameworks such as PCI DSS, ISO 27001, and SOC 2 require audit processes, documentation reviews, and organisational controls that are outside the scope of automated penetration testing.

A control marked as "no findings" means no technical vulnerability was detected against it during the scan. It does not mean the control is fully satisfied.

---

## Related

- [Scope Configuration](scope-configuration.md)
- [Report Branding](report-branding.md)
- [Membership & Plans](../account/membership.md)
