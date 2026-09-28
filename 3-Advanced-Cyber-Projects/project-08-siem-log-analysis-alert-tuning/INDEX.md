<a id="top"></a>
<div align="center">

# 📊 Project 11 — Index
### SIEM Log Analysis & Alert Tuning
**Project 08 of 29 — Blue Team Internship Portfolio**

![Wazuh](https://img.shields.io/badge/Wazuh_Threat_Hunting-3AAFDA?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux_auth.log-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Windows](https://img.shields.io/badge/Windows_Event_IDs-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![CSV](https://img.shields.io/badge/CSV_Export-217346?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Log Sources | 🖼️ Screenshots | 🎯 Event IDs | 📄 Findings |
|:---:|:---:|:---:|:---:|
| **2** | **5** | **3** | **5** |

</div>

<p align="center">🧩 <b>Sources:</b> Real Ubuntu <code>auth.log</code> ➜ simulated Windows Security events via <code>logger</code> ➜ one correlated CSV</p>

---

## 📑 Step Index

All 5 steps of the project, with the screenshot that shows each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Generate real SSH authentication failures | 🔵 Module 1 | Rule 5710 fires on invalid-user login attempt | [Exhibit 1](#ex1) |
| 2 | Inject simulated Windows Security events | 🟠 Module 2 | Event IDs 4625, 4720, 4672 streamed via `logger` | [Exhibit 2](#ex2) |
| 3 | Restart the Wazuh Manager to sync the pipeline | 🟠 Module 2 | Service restarted, decoder ready | [Exhibit 3](#ex3) |
| 4 | Confirm decoder parsing with Ruleset Test | 🟢 Module 3 | JSON decoder correctly parses simulated fields | [Exhibit 4](#ex4) |
| 5 | Export the correlated alerts to CSV | 🟢 Module 3 | `download.csv` opened and verified in Notepad | [Exhibit 5](#ex5) |

---

## 🔵 Module 1 — Baseline Log Generation

Exhibit 1. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-ssh-manual-log-generation.PNG"><img src="screenshots/ss-01-ssh-manual-log-generation.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Manual SSH log generation</b>
<br><sub>Real authentication-failure attempts on the Ubuntu agent</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠 Module 2 — Simulated Windows Telemetry

Exhibits 2 to 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-logger-event-injection.PNG"><img src="screenshots/ss-02-logger-event-injection.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Logger event injection</b>
<br><sub>Simulated Windows Security events streamed for pipeline testing</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-wazuh-manager-pipeline-sync.PNG"><img src="screenshots/ss-03-wazuh-manager-pipeline-sync.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Pipeline sync</b>
<br><sub><code>wazuh-manager</code> restarted to sync the analysis pipeline</sub>
</td>
</tr>
</table>

---

## 🟢 Module 3 — Correlation & Reporting

Exhibits 4 to 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-ruleset-test-decoder-trace.PNG"><img src="screenshots/ss-04-ruleset-test-decoder-trace.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Decoder trace</b>
<br><sub>Ruleset Test tool confirms correct JSON field parsing</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-csv-export-notepad.PNG"><img src="screenshots/ss-05-csv-export-notepad.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — CSV export</b>
<br><sub>Correlated alerts exported and reviewed in Notepad</sub>
</td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Real SSH failure logged and triaged | `auth.log`, Rule 5710 | Module 1 | ✅ Confirmed |
| Unrelated service crash correctly de-prioritized | `syslog`, Rule 40700 | Module 1 | ✅ Confirmed |
| Simulated Windows events injected | `logger` | Module 2 | ✅ Confirmed |
| Decoder parses simulated fields correctly | Ruleset Test tool | Module 3 | ✅ Confirmed |
| 5-event timeline correlated across sources | Manual timeline build | Module 3 | ✅ Confirmed |
| CSV export produced and readable | `download.csv` in Notepad | Module 3 | ✅ Confirmed |
| Live Windows detection | — | — | ❌ Not applicable — no Windows agent in this lab |

> [!NOTE]
> Every Windows-side finding in this project is simulated via `logger` injection, not a live detection — this is stated wherever that data is used, both here and in the README.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh Ruleset Test](https://documentation.wazuh.com/current/user-manual/ruleset/testing.html)** · 🪟 **[Windows Security Event IDs](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/basic-audit-logon-events)** · 🧭 **[Troubleshooting Pipeline](README.md#troubleshooting-pipeline)**

</div>
