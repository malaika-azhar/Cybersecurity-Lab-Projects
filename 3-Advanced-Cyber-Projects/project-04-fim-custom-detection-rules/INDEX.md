<a id="top"></a>
<div align="center">

# 🛡️ Project 04 — Index
### Wazuh File Integrity Monitoring & Custom Detection Rules
**Project 04 of 29 — Advanced Cyber Projects**

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005EB8?style=for-the-badge&logo=wazuh&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Endpoint-Ubuntu_Server-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-T1136.001_%7C_T1110.001-C8102E?style=for-the-badge)
![Detection Engineering](https://img.shields.io/badge/Focus-Detection_Engineering-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step, screenshot and rule in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 📜 Custom Rules | 🎯 MITRE Techniques |
|:---:|:---:|:---:|:---:|
| **2** | **8** | **2 tested + 1 drafted** | **2** |

</div>

<p align="center">🧩 <b>Lab:</b> Ubuntu Server (Wazuh Agent v4.14.6) ➜ Wazuh Manager · Indexer · Dashboard, both in Oracle VirtualBox</p>

---

## 📑 Step Index

All 9 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Enable real-time syscheck on `/etc` and `/var/log` | 🔵 Module 1 | Real-time on `/etc`, notification-only on `/var/log` | [Exhibit 1](#ex1) |
| 2 | Restart the agent and confirm it is Active | 🔵 Module 1 | `ubuntu-agent` shows Active | [Exhibit 2](#ex2) |
| 3 | Create, modify and delete a test file in `/etc` | 🔵 Module 1 | 3 file events generated | Commands (see README) |
| 4 | Confirm the 3 FIM events on the dashboard | 🔵 Module 1 | Rules 554 added, 550 modified, 553 deleted | [Exhibit 3](#ex3) |
| 5 | Write the custom rule set in `local_rules.xml` | 🟢 Module 2 | 3 rules saved (2 tested, 1 drafted) | [Exhibit 4](#ex4) |
| 6 | Trigger Rule 100001 with `adduser` | 🟢 Module 2 | Test user `cyberster_test_user` created | [Exhibit 5](#ex5) |
| 7 | Confirm Rule 100001 fires on the dashboard | 🟢 Module 2 | Rule 100001 fired, Level 10 | [Exhibit 7](#ex7) |
| 8 | Trigger Rule 100002 with an SSH failure burst | 🟢 Module 2 | Repeated SSH login failures generated | [Exhibit 6](#ex6) |
| 9 | Confirm Rule 100002 fires on the dashboard | 🟢 Module 2 | Rule 100002 fired, Level 12 | [Exhibit 8](#ex8) |

---

## 🔵 Module 1 — File Integrity Monitoring

Exhibits 1 to 3. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex1"></a>
<a href="screenshots/Exhibit1_FIM_syscheck_config.png"><img src="screenshots/Exhibit1_FIM_syscheck_config.png" width="280" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Syscheck config</b>
<br><sub>Active syscheck block inside <code>ossec.conf</code> on the Linux agent</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex2"></a>
<a href="screenshots/Exhibit2_agent_active_status.png"><img src="screenshots/Exhibit2_agent_active_status.png" width="280" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Agent Active</b>
<br><sub><code>ubuntu-agent</code> reporting Active on the Wazuh Dashboard after the restart</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex3"></a>
<a href="screenshots/Exhibit3_FIM_all_alerts.png"><img src="screenshots/Exhibit3_FIM_all_alerts.png" width="280" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — FIM alerts</b>
<br><sub>Added (554), modified (550) and deleted (553) events for the test file</sub>
</td>
</tr>
</table>

---

## 🟢 Module 2 — Custom Detection Rules

Exhibits 4 to 8.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex4"></a>
<a href="screenshots/Exhibit4_custom_rules_xml.png"><img src="screenshots/Exhibit4_custom_rules_xml.png" width="280" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Custom rules XML</b>
<br><sub>Rules 100001, 100002 and 100003 in <code>local_rules.xml</code></sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex5"></a>
<a href="screenshots/Exhibit5_adduser_command.png"><img src="screenshots/Exhibit5_adduser_command.png" width="280" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — adduser command</b>
<br><sub><code>adduser cyberster_test_user</code> run on the Ubuntu endpoint</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex6"></a>
<a href="screenshots/Exhibit6_ssh_bruteforce_trigger.png"><img src="screenshots/Exhibit6_ssh_bruteforce_trigger.png" width="280" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — SSH failure burst</b>
<br><sub>SSH loop producing repeated "Permission denied" failures</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex7"></a>
<a href="screenshots/Exhibit7_rule100001_alert.png"><img src="screenshots/Exhibit7_rule100001_alert.png" width="280" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Rule 100001 alert</b>
<br><sub>Level 10 alert in Threat Hunting. Alerts recorded under agent <code>wazuh-server</code></sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex8"></a>
<a href="screenshots/Exhibit8_rule100002_alert.png"><img src="screenshots/Exhibit8_rule100002_alert.png" width="280" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Rule 100002 alert</b>
<br><sub>Level 12 alert in Threat Hunting on the SSH failure burst</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Rules and MITRE ATT&CK

| Rule | Detects | Technique | Tactic | Level | Status |
|:---:|---|---|---|:---:|:---:|
| `100001` | Local user account creation | [T1136.001](https://attack.mitre.org/techniques/T1136/001/) | Persistence | 10 | ✅ Tested & firing |
| `100002` | SSH brute-force | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) | Credential Access | 12 | ✅ Tested & firing |
| `100003` | External USB storage insertion | [T1200](https://attack.mitre.org/techniques/T1200/) | Initial Access | 7 | ⏳ Drafted, untested |

> [!NOTE]
> Rule 100003 is written but untested because the lab had no Windows agent.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh](https://wazuh.com)** · 🐧 **[Ubuntu](https://ubuntu.com)** · 🎯 **[MITRE ATT&CK](https://attack.mitre.org)** · 🔍 **[Detection Engineering](README.md#detection-pipeline)**

</div>
