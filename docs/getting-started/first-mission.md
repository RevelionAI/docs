# Your First Mission

A mission is a scoped penetration test run by Revelion's agent network. This page walks through creating one, monitoring it live, and reading the results.

!!! warning "Only test targets you own or have explicit permission to test"
    Revelion is a real offensive security tool. Running scans against targets without authorisation is illegal. Ensure you have written permission before launching any mission.

---

## 1. Create the Mission

From the dashboard, click **New Mission** in the sidebar or the top-right button on the Missions page.

Fill in the mission form:

**Target**
Enter the URL or IP address of the target. Examples:
- `https://app.example.com`
- `192.168.1.0/24`
- `10.0.0.5`

**Scan Mode**
Choose based on how thorough you need the assessment to be.

| Mode | Duration | Agents | Best for |
|---|---|---|---|
| Quick | ~30 min | 2 | Rapid check, known surface |
| Standard | ~1–2 hrs | 4 | Typical web or network target |
| Deep | ~3–4 hrs | 6 | Full-coverage assessment |

**Scan Type**
Select **Web** for HTTP/HTTPS targets or **Network** for IP-based targets and internal networks.

**Scope**
Define what is in and out of bounds:
- *In scope*: subdomains, paths, or IP ranges the agents are allowed to touch.
- *Out of scope*: anything explicitly excluded (e.g. `/admin`, third-party payment pages).

!!! tip "Scope matters"
    Tighter scope means faster, more focused results. Agents will not test anything outside the scope you define.

---

## 2. Launch

Click **Launch Mission**. Revelion dispatches the root agent immediately. The scan appears in your Missions list with a live status indicator.

```
revelion@ai $ # Agents are now running in the sandbox on your daemon
```

---

## 3. Monitor in Real-Time

Open the mission detail page. Four panels update live as the scan runs:

**Intel Feed**
A chronological stream of agent activity — what each agent found, what tools it called, and what it decided to investigate next.

**Terminal**
Raw tool output forwarded directly from the sandbox. See nmap results, nuclei output, HTTP responses, and exploit attempts as they happen.

**Findings**
Vulnerabilities appear here as agents discover and confirm them. Each finding has a reference ID, severity, CVSS score, and evidence.

**Agent Tree**
A live graph of all active agents, their roles, and their current status. Watch the root agent spawn sub-agents for specific tasks.

!!! tip "You do not need to stay on the page"
    Revelion continues running whether or not the browser tab is open. Come back at any time — all events are stored and the page loads the full history.

---

## 4. Reading the Results

When the scan completes, the mission status changes to **Completed**.

**Findings panel**
Every finding includes:

- **Reference** — unique ID per mission (e.g. `VLN-001`, `VLN-002`)
- **Severity** — Critical / High / Medium / Low / Informational
- **CVSS score** — industry-standard severity rating with vector string
- **Evidence** — proof-of-concept payload, screenshot, or HTTP response
- **Remediation** — concrete steps to fix the issue

**PDF Report**
Revelion generates a full PDF report automatically on completion. Download it from the mission detail page or the Reports section. The PDF includes an executive summary, all findings with evidence, and appendices.

For white-label PDF output (custom logo, colours, company name), configure branding in [Settings → Report Branding](../reports.md#white-label).

---

## 5. Retesting

After you remediate findings, create a new mission against the same target. Revelion tracks findings across missions — if a previously confirmed vulnerability no longer reproduces, it is marked as resolved in the [Vulnerability Management](../vuln-management.md) view.

---

## What's Next

- [Scan Modes](../scan-modes.md) — deep dive on Quick, Standard, and Deep
- [Findings & Reports](../reports.md) — PDF export, JSON export, white-label
- [Vulnerability Management](../vuln-management.md) — asset tracking across missions
