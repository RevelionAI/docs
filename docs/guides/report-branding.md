# Report Branding

Revelion generates PDF reports for every completed mission. Report branding lets you replace the default Revelion styling with your own identity — useful for delivering reports to clients under your own brand.

---

## Plan Capabilities

| Feature | Pro | MSP |
|---|---|---|
| Upload logo | Yes | Yes |
| Set text and heading colours | Yes | Yes |
| Company name in reports | No | Yes |
| Primary / accent / background colours | No | Yes |
| Custom header and footer text | No | Yes |
| Hide "Powered by Revelion" | No | Yes |
| Per-client branding overrides | No | Yes |

---

## Configuring Branding

### Pro Plan

Navigate to **Settings → Report Branding**.

- **Logo**: Upload a PNG or SVG. Recommended dimensions: 300×80px. The logo appears in the report header.
- **Text colour**: Used for body content and labels.
- **Heading colour**: Used for section titles and finding headings.

Changes apply to all reports generated after saving.

### MSP Plan — White-Label Editor

MSP accounts have access to the full White-Label Editor at **Settings → Report Branding → Open Editor**. The editor shows a live preview of the report as you make changes.

Available controls:

- **Company name** — replaces "Revelion" in report headers and footers
- **Logo** — PNG or SVG upload
- **Primary colour** — main brand colour, used for headings and accents
- **Accent colour** — secondary highlight colour
- **Background colour** — report page background
- **Header text** — custom text in the page header (e.g., "Confidential — Client Name")
- **Footer text** — custom text in the page footer (e.g., company address, legal disclaimer)
- **Powered by Revelion badge** — toggle visibility on/off

!!! tip "Live Preview"
    The White-Label Editor renders a sample report page in real-time as you adjust settings. You do not need to generate a full scan report to check how your branding looks.

---

## Per-Client Branding (MSP)

MSP accounts can override the organisation-level branding for individual clients. This lets you deliver reports with client-specific styling — for example, using the client's own colours and logo on their reports.

Configure per-client overrides in **MSP → Clients → [Client Name] → Report Branding**. Any fields left blank in the client override will fall back to the organisation-level defaults.

!!! info "Override Priority"
    Per-client branding takes full precedence over organisation branding for that client's reports. Organisation branding applies to all clients that do not have an override set.

---

## When Branding Takes Effect

Branding is applied at the time a report is generated. Saving new branding settings does not retroactively update previously generated PDFs. To regenerate a report with updated branding, open the mission and click **Regenerate Report**.

---

## Related

- [Compliance Frameworks](compliance-frameworks.md)
- [MSP Overview](../msp/overview.md)
- [Membership & Plans](../account/membership.md)
