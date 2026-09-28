<a id="top"></a>
<div align="center">

# 🔓 Project 08 — Index
### SSH BruteForce Detection Lab
**Project 06 of 29 — Blue Team Internship Portfolio**

![Wazuh](https://img.shields.io/badge/Wazuh_Rules_Engine-3AAFDA?style=for-the-badge)
![Ubuntu](https://img.shields.io/badge/Ubuntu_Server-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-000000?style=for-the-badge&logo=openssh&logoColor=white)
![MITRE](https://img.shields.io/badge/MITRE_ATT%26CK-C6501F?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Custom Rules | 🖼️ Screenshots | 🎯 MITRE Techniques | 🔁 Corrections Made |
|:---:|:---:|:---:|:---:|
| **2** | **5** | **2** | **1** |

</div>

<p align="center">🧩 <b>Lab:</b> Wazuh Manager + Ubuntu agent · custom rules in <code>local_rules.xml</code></p>

---

## 📑 Step Index

All 5 steps of the project, with the screenshot that shows each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Author both rules in `local_rules.xml` | 🔵 Module 1 | Rule 100001 (Level 10) and Rule 100002 (Level 12) saved | [Exhibit 1](#ex1) |
| 2 | Provision a new local user | 🟠 Module 2 | `adduser lab_test_user` run on the Ubuntu agent | [Exhibit 2](#ex2) |
| 3 | Run the SSH brute-force loop | 🟠 Module 2 | 10 rapid `Permission denied` failures generated | [Exhibit 3](#ex3) |
| 4 | Confirm Rule 100001 fired | 🟢 Module 3 | Threat Hunting shows Rule 100001 on the new-user event | [Exhibit 4](#ex4) |
| 5 | Confirm Rule 100002 fired (after correction) | 🟢 Module 3 | Base pattern fixed 5716 → 5710; Rule 100002 fires | [Exhibit 5](#ex5) |

---

## 🔵 Module 1 — Custom Rule Authoring

Exhibit 1. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-custom-rules-local-rules-xml.PNG"><img src="screenshots/ss-01-custom-rules-local-rules-xml.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Custom rules saved</b>
<br><sub><code>local_rules.xml</code> rule block saved on the Wazuh Manager via <code>nano</code></sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠 Module 2 — Attack Simulation

Exhibits 2 to 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-new-user-creation-command.PNG"><img src="screenshots/ss-02-new-user-creation-command.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — New user creation</b>
<br><sub><code>adduser lab_test_user</code> executed on the Ubuntu agent</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-ssh-bruteforce-loop-trigger.PNG"><img src="screenshots/ss-03-ssh-bruteforce-loop-trigger.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — SSH brute-force loop</b>
<br><sub>Repeated <code>Permission denied</code> failures generated</sub>
</td>
</tr>
</table>

---

## 🟢 Module 3 — Detection Verification

Exhibits 4 to 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-alert-new-user-creation-firing.PNG"><img src="screenshots/ss-04-alert-new-user-creation-firing.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Rule 100001 firing</b>
<br><sub>Threat Hunting panel, Level 10, new-user event</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-alert-ssh-bruteforce-firing.PNG"><img src="screenshots/ss-05-alert-ssh-bruteforce-firing.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Rule 100002 firing</b>
<br><sub>Threat Hunting panel, Level 12, SSH brute-force burst</sub>
</td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Rule 100001 written and loaded | `local_rules.xml`, `nano` | Module 1 | ✅ Confirmed |
| Rule 100002 written and loaded | `local_rules.xml`, `nano` | Module 1 | ✅ Confirmed |
| Real new-user event generated | `adduser` | Module 2 | ✅ Confirmed |
| Real SSH failure burst generated | bash SSH loop | Module 2 | ✅ Confirmed |
| Rule 100001 fired on dashboard | Threat Hunting panel | Module 3 | ✅ Confirmed |
| Rule 100002 fired on dashboard | Threat Hunting panel, `wazuh-logtest` | Module 3 | ✅ Confirmed (after correcting 5716 → 5710) |
| Rule 100003 (Windows USB) validated | — | — | ❌ Not tested — no Windows agent |

> [!NOTE]
> Rule 100002's base pattern was corrected mid-build using `wazuh-logtest` against the real raw log, before being confirmed on the dashboard — this is documented as a correction, not hidden as if it worked the first time.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh Rules Docs](https://documentation.wazuh.com/current/user-manual/ruleset/index.html)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)** · 🧭 **[Troubleshooting Pipeline](README.md#troubleshooting-pipeline)**

</div>
