# Tools

The Revelion sandbox container ships with a curated set of open-source pentesting tools. Agents select tools based on the target type, findings so far, and the current phase of the engagement. You do not configure tool selection — that is handled by the AI.

---

## Available Tools

### Network and Discovery

**Nmap**
Network discovery and port scanning. Used for host discovery, service version detection, OS fingerprinting, and NSE script execution. The primary tool for network scan modes.

**httpx**
Fast HTTP probing at scale. Detects status codes, server headers, TLS details, web technologies, and response hashes across large target lists. Used heavily in reconnaissance to qualify discovered hosts before deeper testing.

**Subfinder**
Passive and active subdomain enumeration. Queries certificate transparency logs, DNS records, and public intelligence sources to discover subdomains before any active scanning begins.

### Web Application Testing

**Nuclei**
Template-based vulnerability scanning with a large community-maintained template library. Used for known CVE detection, misconfiguration checks, exposed panel detection, and exposure verification. Agents run targeted template sets rather than full scans.

**Feroxbuster**
Recursive content discovery and directory bruteforcing. Discovers hidden endpoints, admin panels, backup files, and API routes. Configured with wordlists appropriate to the detected technology stack.

**ffuf**
Web fuzzing for parameters, headers, virtual hosts, and path segments. Used for parameter discovery, filter bypass testing, and enumerating values in known parameter positions.

**Playwright**
Headless Chromium browser. Used for JavaScript-heavy applications where crawling with HTTP requests misses dynamically rendered content. Agents use Playwright to interact with login flows, single-page applications, and authenticated areas.

**Caido**
HTTP proxy for request interception and replay. Provides a structured interface for modifying and replaying requests during exploitation — particularly for session manipulation, parameter tampering, and authentication testing.

### Exploitation

**SQLMap**
Automated SQL injection detection and exploitation. Supports blind, error-based, time-based, and union-based injection across all major database backends. Used after initial injection indicators are confirmed.

!!! warning
    SQLMap in exploitation mode will issue a high volume of requests to the target. Ensure your aggression level and rate limits are set appropriately for the environment under test.

### Additional Tools

The sandbox also includes tools for:

- **Responder** — NetBIOS/LLMNR poisoning for internal network credential capture
- **mitm6** — IPv6-based man-in-the-middle for Active Directory environments
- **Ligolo-ng** — Network tunnelling and pivoting
- **Linux privilege escalation suggester** — Local enumeration for post-exploitation
- **Windows privilege escalation suggester** — Post-exploitation enumeration for Windows targets

---

## Tool Selection

Revelion's agents decide which tools to invoke based on:

- The target type (web, API, network, cloud)
- Technologies detected during reconnaissance
- Findings from earlier in the scan
- The current phase (recon vs exploitation)
- The scan mode (quick, standard, deep)

A quick web scan may only invoke httpx, Nuclei, and Feroxbuster. A deep network scan against an Active Directory environment will work through Nmap, Responder, mitm6, and privilege escalation scripts in sequence.

!!! tip
    You can steer tool focus with pre-mission instructions. For example: "This is a GraphQL API — focus on introspection, injection, and authorisation testing" will cause agents to prioritise relevant tools and skip ones that do not apply.

---

## Tool Output

Raw tool output is streamed to the Live Intel Feed as it runs. Findings extracted from tool output are written to the findings table immediately — you do not need to wait for the scan to complete to see results.

Tool output is also stored as scan artifacts and linked to the findings they produced, so the report includes the exact evidence from each tool invocation.
