<a id="top"></a>
<div align="center">

# 🛡️ Project 20 — Index
### Windows Brute Force Detection with Wazuh
**Project 20 of 20 — Blue Team Defense Projects**

![Azure](https://img.shields.io/badge/Azure_VM-Ubuntu_24.04.5-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Windows](https://img.shields.io/badge/Windows_10_Pro-Endpoint-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh-4.9.2-3AAFDA?style=for-the-badge)
![MITRE](https://img.shields.io/badge/MITRE-T1110_Brute_Force-B03A2E?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots |
|:---:|:---:|
| **3** | **25** |

</div>

<p align="center">🧩 <b>Lab:</b> Azure Ubuntu VM · Wazuh 4.9.2 SIEM · Windows 10 Pro agent · 12 alerts detected</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Reach the server over SSH | 🔵 Module 1 | Key-less SSH refused with <code>Permission denied (publickey)</code> | [Exhibit 1](#ex1) |
| 2 | Log in with the key file | 🔵 Module 1 | Login with the key file succeeds | [Exhibit 2](#ex2) |
| 3 | Installer finds an existing install | 🔵 Module 1 | "Already installed"; services active (running), restarted | [Exhibit 3](#ex3) |
| 4 | Credentials archive missing, password tool rejected, overwrite chosen | 🔵 Module 1 | Policy rejected the password; overwrite reinstall started | [Exhibit 4](#ex4) |
| 5 | First reinstall fails at Filebeat | 🔵 Module 1 | Filebeat error, installation cleaned up | [Exhibit 5](#ex5) |
| 6 | Second reinstall completes | 🔵 Module 1 | Installer finished at 17:21:36 UTC | [Exhibit 6](#ex6) |
| 7 | Dashboard login attempt rejected | 🔵 Module 1 | Login refused; credentials re-read next | [Exhibit 7](#ex7) |
| 8 | Read the credentials from the install archive | 🔵 Module 1 | Passwords read with <code>tar</code> and <code>grep</code> | [Exhibit 8](#ex8) |
| 9 | Install the Windows agent | 🟠 Module 2 | Install command run; service already started | [Exhibit 9](#ex9) |
| 10 | Confirm the manager ports are reachable | 🟠 Module 2 | Ports 1514 and 1515 reachable | [Exhibit 10](#ex10) |
| 11 | Diagnose why the agent will not register | 🟠 Module 2 | Agent newer than the 4.9.2 manager | [Exhibit 11](#ex11) |
| 12 | Uninstall the mismatched agent | 🟠 Module 2 | Mismatched agent removed | [Exhibit 12](#ex12) |
| 13 | Clean up and reinstall a matching version | 🟠 Module 2 | Matching agent version installed | [Exhibit 13](#ex13) |
| 14 | Start the service | 🟠 Module 2 | Service running, log still being created | [Exhibit 14](#ex14) |
| 15 | Verify the agent files are back | 🟠 Module 2 | Agent directory repopulated | [Exhibit 15](#ex15) |
| 16 | Confirm the agent is active in the dashboard | 🟠 Module 2 | Agent shows active in Endpoints | [Exhibit 16](#ex16) |
| 17 | Check the agent log and create a test account | 🔴 Module 3 | Agent online; test account created | [Exhibit 17](#ex17) |
| 18 | Simulate the brute force | 🔴 Module 3 | Failed logons generated on the endpoint | [Exhibit 18](#ex18) |
| 19 | Find the agent's events in Discover | 🔴 Module 3 | 514 hits (mixed events, not the alert count) | [Exhibit 19](#ex19) |
| 20 | Filter to high-severity alerts | 🔴 Module 3 | 12 hits, event 4625 in <code>_source</code> | [Exhibit 20](#ex20) |
| 21 | Add columns and save the search | 🔴 Module 3 | Columns added and search saved | [Exhibit 21](#ex21) |
| 22 | Widen the window to 24 hours | 🔴 Module 3 | Same 12 hits over 24 hours | [Exhibit 22](#ex22) |
| 23 | Generate the CSV report | 🔴 Module 3 | CSV generated at 18:51:23 UTC | [Exhibit 23](#ex23) |
| 24 | Inspect the query | 🔴 Module 3 | Request statistics captured; JSON saved | [Exhibit 24](#ex24) |
| 25 | Dashboard overview, last 24 hours | 🔴 Module 3 | 12 medium alerts match the level-10 alerts | [Exhibit 25](#ex25) |

---

## 🔵 Module 1 — Wazuh Server Deployment

Exhibits 1 to 8.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-ssh-publickey-denied.PNG"><img src="screenshots/ss-01-ssh-publickey-denied.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — SSH permission denied</b>
<br><sub>Key-less SSH refused (publickey)</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-ssh-key-login-success.PNG"><img src="screenshots/ss-02-ssh-key-login-success.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — SSH key login</b>
<br><sub>Ubuntu 24.04.5 LTS on <code>lab-server</code></sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-installer-already-installed-services-active.PNG"><img src="screenshots/ss-03-installer-already-installed-services-active.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Existing install found</b>
<br><sub>Installer stops; 3 services active, restarted</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-passwords-tool-rejected-overwrite-reinstall.PNG"><img src="screenshots/ss-04-passwords-tool-rejected-overwrite-reinstall.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Password tool and overwrite</b>
<br><sub>Weak password rejected; <code>-a -o</code> started</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-first-reinstall-filebeat-error.PNG"><img src="screenshots/ss-05-first-reinstall-filebeat-error.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — First reinstall fails</b>
<br><sub><code>filebeat could not be started</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/ss-06-wazuh-install-finished.PNG"><img src="screenshots/ss-06-wazuh-install-finished.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Second reinstall completes</b>
<br><sub><code>Installation finished</code> (credentials redacted)</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/ss-07-dashboard-login-rejected.PNG"><img src="screenshots/ss-07-dashboard-login-rejected.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Dashboard login rejected</b>
<br><sub><code>Invalid username or password</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/ss-08-credentials-read-from-archive.PNG"><img src="screenshots/ss-08-credentials-read-from-archive.PNG" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Credentials from archive</b>
<br><sub><code>admin</code> and <code>anomalyadmin</code> (redacted)</sub>
</td>
</tr>
</table>

---

## 🟠 Module 2 — Windows Agent Enrollment

Exhibits 9 to 16.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex9"></a>
<a href="screenshots/ss-09-agent-install-service-started.PNG"><img src="screenshots/ss-09-agent-install-service-started.PNG" width="380" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — Agent install on Windows</b>
<br><sub>MSI 4.9.2, manager IP and agent name set</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex10"></a>
<a href="screenshots/ss-10-manager-ports-1514-1515-reachable.PNG"><img src="screenshots/ss-10-manager-ports-1514-1515-reachable.PNG" width="380" alt="Exhibit 10"></a>
<br><b>Exhibit 10 — Manager ports reachable</b>
<br><sub>1514 and 1515: <code>TcpTestSucceeded : True</code></sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex11"></a>
<a href="screenshots/ss-11-agent-version-mismatch-error.PNG"><img src="screenshots/ss-11-agent-version-mismatch-error.PNG" width="380" alt="Exhibit 11"></a>
<br><b>Exhibit 11 — Version mismatch error</b>
<br><sub>Agent version must be lower or equal to manager</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex12"></a>
<a href="screenshots/ss-12-agent-uninstall.PNG"><img src="screenshots/ss-12-agent-uninstall.PNG" width="380" alt="Exhibit 12"></a>
<br><b>Exhibit 12 — Agent uninstall</b>
<br><sub><code>Win32_Product</code> uninstall, <code>ReturnValue : 0</code></sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex13"></a>
<a href="screenshots/ss-13-agent-folder-removed-reinstall-492.PNG"><img src="screenshots/ss-13-agent-folder-removed-reinstall-492.PNG" width="380" alt="Exhibit 13"></a>
<br><b>Exhibit 13 — Clean reinstall</b>
<br><sub>Folder removed, agent 4.9.2 installed</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex14"></a>
<a href="screenshots/ss-14-service-started-after-reinstall.PNG"><img src="screenshots/ss-14-service-started-after-reinstall.PNG" width="380" alt="Exhibit 14"></a>
<br><b>Exhibit 14 — Service started</b>
<br><sub><code>WazuhSvc</code> started; log not created yet</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex15"></a>
<a href="screenshots/ss-15-agent-directory-listing.PNG"><img src="screenshots/ss-15-agent-directory-listing.PNG" width="380" alt="Exhibit 15"></a>
<br><b>Exhibit 15 — Agent files present</b>
<br><sub><code>ossec.conf</code>, <code>ossec.log</code>, <code>client.keys</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex16"></a>
<a href="screenshots/ss-16-endpoints-agent-active.PNG"><img src="screenshots/ss-16-endpoints-agent-active.PNG" width="380" alt="Exhibit 16"></a>
<br><b>Exhibit 16 — Agent active</b>
<br><sub><code>001 malaika-win01</code>, v4.9.2, active</sub>
</td>
</tr>
</table>

---

## 🔴 Module 3 — Brute Force Simulation and Detection

Exhibits 17 to 25.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex17"></a>
<a href="screenshots/ss-17-agent-log-connected-test-user-created.PNG"><img src="screenshots/ss-17-agent-log-connected-test-user-created.PNG" width="380" alt="Exhibit 17"></a>
<br><b>Exhibit 17 — Agent log and test user</b>
<br><sub>Agent online; <code>wazuhtest</code> created (redacted)</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex18"></a>
<a href="screenshots/ss-18-failed-logon-loop-simulation.PNG"><img src="screenshots/ss-18-failed-logon-loop-simulation.PNG" width="380" alt="Exhibit 18"></a>
<br><b>Exhibit 18 — Brute force simulation</b>
<br><sub><code>net use</code> loop with wrong passwords (redacted)</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex19"></a>
<a href="screenshots/ss-19-discover-agent-events-514-hits.PNG"><img src="screenshots/ss-19-discover-agent-events-514-hits.PNG" width="380" alt="Exhibit 19"></a>
<br><b>Exhibit 19 — Agent events in Discover</b>
<br><sub>514 hits: all agent events, last 24 hours</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex20"></a>
<a href="screenshots/ss-20-discover-high-severity-12-hits-raw.PNG"><img src="screenshots/ss-20-discover-high-severity-12-hits-raw.PNG" width="380" alt="Exhibit 20"></a>
<br><b>Exhibit 20 — High-severity filter</b>
<br><sub><code>rule.level &gt;= 10</code>: 12 hits</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex21"></a>
<a href="screenshots/ss-21-saved-search-columns-30min.PNG"><img src="screenshots/ss-21-saved-search-columns-30min.PNG" width="380" alt="Exhibit 21"></a>
<br><b>Exhibit 21 — Saved search with columns</b>
<br><sub><code>High-Severity-Windows-BruteForce</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex22"></a>
<a href="screenshots/ss-22-saved-search-24h-12-hits.PNG"><img src="screenshots/ss-22-saved-search-24h-12-hits.PNG" width="380" alt="Exhibit 22"></a>
<br><b>Exhibit 22 — 24-hour window</b>
<br><sub>12 hits, 30-minute buckets</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex23"></a>
<a href="screenshots/ss-23-reporting-generate-csv.PNG"><img src="screenshots/ss-23-reporting-generate-csv.PNG" width="380" alt="Exhibit 23"></a>
<br><b>Exhibit 23 — Generate CSV report</b>
<br><sub>Reporting menu: CSV and XLSX</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex24"></a>
<a href="screenshots/ss-24-inspect-request-statistics.PNG"><img src="screenshots/ss-24-inspect-request-statistics.PNG" width="380" alt="Exhibit 24"></a>
<br><b>Exhibit 24 — Inspect request</b>
<br><sub>12 hits, <code>wazuh-alerts-*</code>, 26 ms</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex25"></a>
<a href="screenshots/ss-25-overview-last-24h-alerts.PNG"><img src="screenshots/ss-25-overview-last-24h-alerts.PNG" width="380" alt="Exhibit 25"></a>
<br><b>Exhibit 25 — Overview, last 24 hours</b>
<br><sub>0 critical, 0 high, 12 medium, 18 low</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Wazuh services running | `systemctl status` | Module 1 | ✅ Confirmed |
| Fresh install completes | Installer log | Module 1 | ✅ Confirmed |
| Manager ports reachable | `Test-NetConnection` 1514 / 1515 | Module 2 | ✅ Confirmed |
| Agent registered and active | Endpoints page | Module 2 | ✅ Confirmed |
| Brute force detected | Discover, `rule.level >= 10` | Module 3 | ✅ 12 alerts (rule 60204, T1110) |
| Evidence exported | Reporting CSV + Inspect JSON | Module 3 | ✅ Confirmed |

> [!NOTE]
> The simulated attack ran on the endpoint itself, so the source IP is `127.0.0.1`. Passwords visible in the original captures are blacked out in Exhibits 4, 6, 8, 17 and 18. Dashboard times are UTC+5; exports and server logs are UTC.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh](https://wazuh.com)** · ☁️ **[Microsoft Azure](https://azure.microsoft.com)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)**

</div>
