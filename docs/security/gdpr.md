# GDPR

Revelion is a UK-built platform. All data processing is GDPR compliant, with user data stored in the EU and clear roles defined under the UK GDPR and EU GDPR frameworks.

## Data controller and processor

**You are the data controller.** You determine what targets are scanned, what data is generated, and who has access to it. You decide whether to retain or delete findings, share portal access with clients, or export reports.

**Revelion Limited is the data processor.** Revelion processes personal data on your behalf, under your instruction, as described in our Data Processing Agreement (DPA). A DPA is available on request for Pro, MSP, and Enterprise customers.

## Data storage location

All personal and operational data is stored in **Supabase PostgreSQL, EU West region (eu-west-1)**. No personal data is stored outside the EU or UK without your knowledge.

Ephemeral compute (agent orchestration) runs on Fly.io in the London region (LHR). Scan state processed in-memory during a scan is not persisted to any non-EU system.

## Your rights

As a data subject and data controller, you have the following rights under GDPR:

| Right | How to exercise it |
|---|---|
| Right of access | Export your data from the Revelion dashboard |
| Right to rectification | Update your profile and organisation details in Settings |
| Right to erasure | Delete your account from Settings → Account → Delete Account |
| Right to portability | Reports and findings can be exported in JSON and PDF formats |
| Right to restriction | Contact [privacy@revelion.ai](mailto:privacy@revelion.ai) |
| Right to object | Contact [privacy@revelion.ai](mailto:privacy@revelion.ai) |

Account deletion removes all associated data permanently and irreversibly, including scans, findings, reports, agent history, and billing records held by Revelion.

## Sub-processors

Revelion uses the following sub-processors. Each is contractually bound to process data only as instructed and maintains its own compliance programme.

| Sub-processor | Purpose | Region | Compliance |
|---|---|---|---|
| Supabase | Database and file storage | EU (eu-west-1) | SOC 2 Type II |
| Fly.io | Compute and agent orchestration | UK (LHR) | SOC 2 Type II |
| Anthropic | AI model inference | US | SOC 2 Type II |
| Stripe | Payment processing | EU/US | PCI DSS Level 1, SOC 2 |

!!! info "Anthropic data processing"
    Scan findings and agent reasoning are processed by Anthropic's Claude API during active scans. Anthropic's enterprise API does not use submitted data to train models. See [Anthropic's privacy policy](https://www.anthropic.com/privacy) for full details.

## Changes to sub-processors

We will notify customers of any material changes to our sub-processor list with at least 30 days notice.

## Contact

For data protection enquiries, contact [privacy@revelion.ai](mailto:privacy@revelion.ai).

## Related pages

- [Data Handling](data-handling.md) — what is stored and where
- [Security Overview](index.md) — infrastructure security
- [Legal](legal.md) — authorisation and acceptable use
