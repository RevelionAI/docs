# Scheduled Scans

Scheduled scans let you run Revelion automatically on a recurring basis without manual intervention. Use them to track your attack surface over time, catch regressions after deployments, or maintain continuous security coverage.

!!! tip "Pro Feature"
    Scheduled scans are available on **Pro** and **MSP** plans. Upgrade from the [Membership](../pricing/index.md) page.

---

## Plan Limits

| Plan | Max Schedules |
|---|---|
| Free | Not available |
| Pro | 5 |
| MSP | 50 |

---

## Creating a Schedule

Navigate to **Schedules** in the sidebar and click **New Schedule**.

Configure the following:

### Target
Enter the URL, IP address, or CIDR range to test. This follows the same rules as a manual mission — see [Scope Configuration](scope-configuration.md) for accepted target types.

### Scan Mode
Choose **Quick**, **Standard**, or **Deep**. Most recurring schedules use Standard for balanced coverage. Quick is suitable for daily runs where speed matters more than depth.

### Schedule

Pick from the preset options or enter a custom cron expression:

| Preset | Cron |
|---|---|
| Daily | `0 2 * * *` |
| Weekly (Monday) | `0 2 * * 1` |
| Monthly (1st) | `0 2 1 * *` |
| Custom | Any valid cron expression |

All schedules run in UTC. Use a custom cron expression if you need a specific local time.

### Optional: VPN Config
Attach a VPN config for internal network targets. See [VPN Tunnelling](vpn-tunnelling.md).

---

## Viewing Results

Each scheduled scan creates a mission entry on the **Missions** page, identical to a manually started scan. Results, findings, and PDF reports are all generated and stored the same way.

The notification bell in the top-right corner alerts you when a scheduled scan completes. Click the notification to jump directly to the mission results.

---

## Pausing and Deleting Schedules

From the **Schedules** page:

- **Pause** — stops future runs without deleting the schedule. Resume it at any time.
- **Delete** — permanently removes the schedule. Existing mission results are not affected.

Pausing a schedule does not interrupt any currently running mission triggered by that schedule.

---

## Credit Consumption

Scheduled scans consume credits from your organisation's balance the same way manual scans do. Make sure your balance is sufficient before setting up high-frequency schedules.

!!! warning "Credit Exhaustion"
    If your credit balance is too low when a scheduled scan triggers, the mission will be skipped and you will receive a notification. Top up your credits to resume normal scheduling.

---

## Related

- [Scope Configuration](scope-configuration.md)
- [VPN Tunnelling](vpn-tunnelling.md)
- [Pricing & Credits](../pricing/index.md)
