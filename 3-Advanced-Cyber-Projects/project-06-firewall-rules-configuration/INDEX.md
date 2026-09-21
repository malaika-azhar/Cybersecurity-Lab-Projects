<a id="top"></a>
<div align="center">

# 🔥 Project 06 — Index
### Firewall Rules Configuration on pfSense
**Project 06 of 29 — Advanced Cyber Projects**

![pfSense](https://img.shields.io/badge/Firewall-pfSense-212121?style=for-the-badge&logo=pfsense&logoColor=white)
![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005EB8?style=for-the-badge&logo=wazuh&logoColor=white)
![Logging](https://img.shields.io/badge/Rule-Logging_Enabled-F39C12?style=for-the-badge)
![Rule Direction](https://img.shields.io/badge/Focus-Rule_Direction_%26_Scope-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 📋 Rule Configured | 📡 Delivery Verified |
|:---:|:---:|:---:|:---:|
| **2** | **3** | **Remote Logging — "Everything"** | **✅ End-to-End** |

</div>

<p align="center">🧩 <b>Lab:</b> pfSense Gateway (Logging Rule) ➜ Ubuntu Agent + Wazuh Manager · Indexer · Dashboard, both in Oracle VirtualBox</p>

---

## 📑 Step Index

All 3 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Confirm firewall health on both interfaces | 🔵 Module 1 | Both WAN and LAN up before rule work began | [Exhibit 1](#ex1) |
| 2 | Configure the Remote Logging rule — scope "Everything" | 🟢 Module 2 | Rule saved, targeting `192.168.56.105` | [Exhibit 2](#ex2) |
| 3 | Verify the rule's effect on the receiving side | 🟢 Module 2 | `ss` confirms an active listener on UDP 514 | [Exhibit 3](#ex3) |

---

## 🔵 Module 1 — Firewall Dashboard & Baseline

Exhibit 1. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/Exhibit1_pfsense_firewall_rules.png"><img src="screenshots/Exhibit1_pfsense_firewall_rules.png" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — pfSense dashboard</b>
<br><sub>Firewall running (2.7.2-RELEASE), WAN and LAN interfaces both up before any rule is trusted</sub>
</td>
<td align="center" valign="top" width="50%">

**✅ Baseline Check**
<br><br>
WAN: `Up`
<br>
LAN: `Up`
<br><br>
<sub>A rule configured on top of an unhealthy gateway proves nothing — baseline health is confirmed first.</sub>

</td>
</tr>
</table>

---

## 🟢 Module 2 — Logging Rule Configuration

Exhibits 2 to 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/Exhibit2_logging_rule_config.png"><img src="screenshots/Exhibit2_logging_rule_config.png" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Logging rule config</b>
<br><sub>Remote server set to <code>192.168.56.105</code>, "Everything" selected under Remote Syslog Contents</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/Exhibit3_wazuh_udp514_listening.png"><img src="screenshots/Exhibit3_wazuh_udp514_listening.png" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Wazuh listening on UDP 514</b>
<br><sub><code>ss</code> output confirming <code>udp UNCONN 0 0 0.0.0.0:514</code> — the rule is actually delivering</sub>
</td>
</tr>
</table>

---

## 🎯 Rule Configuration Summary

| Field | Value | Status |
|:---:|---|:---:|
| Enable Remote Logging | Checked | ✅ Confirmed |
| Remote log server | `192.168.56.105` | ✅ Correct |
| Remote Syslog Contents | `Everything` | ✅ Full scope |
| Receiving-side verification | `ss` — UDP 514 UNCONN | ✅ Confirmed |

> [!NOTE]
> Traffic-filtering allow/deny rules on the WAN/LAN interfaces are addressed as a separate module — this project scopes specifically to the logging rule and its verified delivery.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🔥 **[pfSense](https://www.pfsense.org)** · 🛡️ **[Wazuh](https://wazuh.com)** · 📡 **[Syslog Protocol](https://datatracker.ietf.org/doc/html/rfc5424)** · 🧭 **[Rule Pipeline](README.md#rule-pipeline)**

</div>
