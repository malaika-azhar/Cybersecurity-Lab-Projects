<a id="top"></a>
<div align="center">

# 🕵️ Project 19 — Index
### Insider Threat Detection System
**Project 19 of 29 — Advanced Cyber Projects**

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005EB8?style=for-the-badge&logo=wazuh&logoColor=white)
![Kali](https://img.shields.io/badge/Red_Team-Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![CyberChef](https://img.shields.io/badge/Forensics-CyberChef-1A1A1A?style=for-the-badge)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-T1565.001_%7C_T1027-C8102E?style=for-the-badge)
![NIST 800-61](https://img.shields.io/badge/Framework-NIST_SP_800--61-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 📜 Custom Rules | 🎯 MITRE Techniques |
|:---:|:---:|:---:|:---:|
| **2** | **5** | **1 verified** | **2** |

</div>

<p align="center">🧩 <b>Lab:</b> Kali (Red Team attack chain) ➜ Wazuh FIM + Audit Logs ➜ CyberChef Decode ➜ Custom Detection Rule</p>

---

## 📑 Step Index

All 6 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Stage, obfuscate, exfiltrate, delete | 🔵 Module 1 | Full attack chain executed on the monitored host | Commands (see README) |
| 2 | Confirm creation/obfuscation via FIM | 🔵 Module 1 | Rule 550 fired on both staged files | [Exhibit 1](#ex1) |
| 3 | Diagnose the deletion-rule gap | 🔵 Module 1 | Compensating evidence found via sudo audit (rule 5402) | [Exhibit 2](#ex2) |
| 4 | Decode the captured exfiltration payload | 🟢 Module 2 | Exact client data recovered via CyberChef | [Exhibit 3](#ex3) |
| 5 | Engineer the custom detection rule | 🟢 Module 2 | Rule 100050 deployed, MITRE T1027 tagged | [Exhibit 4](#ex4) |
| 6 | Verify the rule live-fires | 🟢 Module 2 | Confirmed firing on a re-run of the attack | [Exhibit 5](#ex5) |

---

## 🔵 Module 1 — Attack Simulation & FIM Threat Hunting

Exhibits 1 to 2. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/Exhibit1_fim_creation_alerts.png"><img src="screenshots/Exhibit1_fim_creation_alerts.png" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — FIM creation alerts</b>
<br><sub>Rule 550 confirming both staged files, SHA1 hash and mtime captured</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/Exhibit2_sudo_audit_deletion_log.png"><img src="screenshots/Exhibit2_sudo_audit_deletion_log.png" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Compensating deletion evidence</b>
<br><sub>Sudo audit rule 5402 confirming <code>rm -f</code> when the dedicated FIM rule didn't fire</sub>
</td>
</tr>
</table>

---

## 🟢 Module 2 — Forensic Decoding & Detection Engineering

Exhibits 3 to 5.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex3"></a>
<a href="screenshots/Exhibit3_cyberchef_base64_decode.png"><img src="screenshots/Exhibit3_cyberchef_base64_decode.png" width="280" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — CyberChef decode</b>
<br><sub>Exact exfiltrated content recovered from the captured payload</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex4"></a>
<a href="screenshots/Exhibit4_custom_rule_100050_xml.png"><img src="screenshots/Exhibit4_custom_rule_100050_xml.png" width="280" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Custom rule 100050</b>
<br><sub>Chained on parent rule 550, Level 10, MITRE T1027</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex5"></a>
<a href="screenshots/Exhibit5_rule_100050_live_fire.png"><img src="screenshots/Exhibit5_rule_100050_live_fire.png" width="280" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Live-fire verified</b>
<br><sub>Rule 100050 confirmed firing on a re-run of the attack</sub>
</td>
</tr>
</table>

---

## 🎯 Rules and MITRE ATT&CK

| Rule / Stage | Detects | Technique | Tactic | Status |
|:---:|---|---|---|:---:|
| Staging & obfuscation | Data staged for exfiltration | [T1565.001](https://attack.mitre.org/techniques/T1565/001/) | Impact | ✅ Detected natively |
| `100050` | `.b64` file in staging directory | [T1027](https://attack.mitre.org/techniques/T1027/) | Defense Evasion | ✅ Tested & firing |

> [!NOTE]
> The dedicated FIM deletion rule did not fire despite correct configuration — this gap is documented, not hidden, and compensated for via the sudo command-execution audit trail. Full diagnosis in the README.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🕵️ **[Wazuh](https://wazuh.com)** · 🔓 **[CyberChef](https://gchq.github.io/CyberChef/)** · 🎯 **[MITRE ATT&CK](https://attack.mitre.org)** · 📘 **[NIST SP 800-61](https://csrc.nist.gov/pubs/sp/800/61/r2/final)**

</div>
