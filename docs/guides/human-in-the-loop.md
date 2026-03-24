# Human-in-the-Loop

Revelion can operate fully autonomously or pause at critical decision points and wait for your approval. Human-in-the-loop (HITL) mode gives you direct oversight over agent actions without stopping the mission entirely.

---

## Modes

### Automatic (Default)

The agent runs without interruption. It plans, executes tools, forms hypotheses, and reports findings end-to-end. This is the default for most missions and the recommended mode once you are familiar with how the agent behaves.

### Manual (HITL)

The agent pauses before any high-risk action and presents it to you for approval. The mission does not proceed until you respond. Use this when testing sensitive systems, learning the agent's decision-making, or when your organisation requires human sign-off before active exploitation.

!!! tip "Recommended for New Users"
    Use Manual mode for your first few scans to understand how Revelion approaches a target, which tools it selects, and why. It is the fastest way to build confidence before switching to Automatic.

---

## Toggling Modes

You can switch between Automatic and Manual at any point during a live mission from the mission detail page. The toggle takes effect immediately — if you switch to Manual while the agent is mid-task, it will pause at the next decision boundary.

---

## The Approval Panel

When Revelion is running in Manual mode and reaches a high-risk action, the Approval Panel appears. It shows:

- **Action**: What the agent wants to do (e.g., "Run SQL injection payload against /api/login")
- **Reasoning**: Why the agent has chosen this action based on prior observations
- **Expected Impact**: What the action will do to the target system (read-only probe, destructive test, etc.)
- **Risk Level**: Low / Medium / High — set by the agent based on the action type

### Approving or Denying

Click **Approve** to let the agent proceed. Click **Deny** to block the action — the agent will note the denial and select an alternative approach.

You can deny an action with an optional note explaining why. The agent incorporates your note when planning its next step.

---

## Pre-Mission Instructions

Before starting a mission, the setup form includes a free-text **Instructions** field. Use this to guide the agent's overall behaviour for the session. Examples:

```
Focus only on authentication and session management.
Do not attempt any destructive payloads.
Prioritise findings that affect user data exfiltration.
```

Instructions are injected into the agent's system context at mission start and influence all decision-making throughout the run.

---

## Operator Directives

During a live mission you can send real-time directives to the agent via the chat input on the mission detail page. Directives let you steer the mission without stopping it:

- `"Pivot to testing the file upload endpoint"`
- `"Stop testing /api/admin — it is out of scope"`
- `"Run a deeper check on the JWT implementation"`

Revelion acknowledges the directive and adjusts its plan. Directives are logged alongside agent activity in the mission timeline.

---

## Related

- [Scope Configuration](scope-configuration.md)
- [Running a Mission](../quickstart/first-mission.md)
- [Scheduled Scans](scheduled-scans.md)
