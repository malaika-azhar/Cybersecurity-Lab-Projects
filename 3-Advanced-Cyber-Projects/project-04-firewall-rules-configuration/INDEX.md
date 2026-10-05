<a id="top"></a>
<div align="center">

# 🔥 Project 04 — Index
### Firewall Rules Configuration on pfSense
**Project 04 of 18 — Advanced Cyber Projects**

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

| 🧩 Modules | 🖼️ Screenshots | 📋 Rule Configured | 📡 Receiving Side |
|:---:|:---:|:---:|:---:|
| **2** | **4** | **Remote Logging — "Everything"** | **✅ Listener Confirmed** |

</div>

<p align="center">🧩 <b>Lab:</b> pfSense Gateway (Logging Rule) ➜ Ubuntu Agent + Wazuh Manager · Indexer · Dashboard, both in Oracle VirtualBox</p>

---

## 📑 Step Index

All 4 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Confirm the firewall is up and reachable | 🔵 Module 1 | Dashboard reachable, version 2.7.2-RELEASE, before rule work began | [Exhibit 1](#ex1) |
| 2 | Configure the Remote Logging rule — scope "Everything" | 🟢 Module 2 | Rule saved, targeting `192.168.56.105` | [Exhibit 2](#ex2) |
| 3 | Check the receiving side is listening | 🟢 Module 2 | `ss` confirms an active listener on UDP 514 | [Exhibit 3](#ex3) |
| 4 | Confirm the Manager permits syslog from the firewall | 🟢 Module 2 | `allowed-ips` includes `192.168.56.1` | [Exhibit 4](#ex4) |

---

## 🔵 Module 1 — Firewall Dashboard & Baseline

Exhibit 1. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/Exhibit1_pfsense_dashboard.png"><img src="screenshots/Exhibit1_pfsense_dashboard.png" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — pfSense dashboard</b>
<br><sub>Firewall running (2.7.2-RELEASE, VirtualBox VM) before any rule is trusted</sub>
</td>
<td align="center" valign="top" width="50%">

**✅ Baseline Check**
<br><br>
Version: `2.7.2-RELEASE`
<br>
Platform: `VirtualBox VM`
<br><br>
<sub>A rule configured on top of an unhealthy gateway proves nothing — baseline health is confirmed first.</sub>

</td>
</tr>
</table>

---

## 🟢 Module 2 — Logging Rule Configuration

Exhibits 2 to 4.

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
<br><sub><code>ss</code> output confirming <code>udp UNCONN 0 0 0.0.0.0:514</code> — the Manager is listening on the syslog port</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/Exhibit4_wazuh_syslog_allowed_ips.png"><img src="screenshots/Exhibit4_wazuh_syslog_allowed_ips.png" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Wazuh syslog allowed-ips</b>
<br><sub><code>ossec.conf</code> syslog blocks on UDP 514 with <code>allowed-ips</code> <code>192.168.56.0/24</code> and <code>192.168.56.1</code> (cropped from the Week 4 report, Figure 4.1)</sub>
</td>
<td align="center" valign="top" width="50%">

**✅ Receiving-Side Check**
<br><br>
Listener: `UDP 514`
<br>
Allowed IP: `192.168.56.1`
<br><br>
<sub>An open port is not assumed to accept the firewall's traffic — the allowed source list is checked too.</sub>

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
| Firewall address permitted | `allowed-ips` — `192.168.56.1` | ✅ Confirmed |

> [!NOTE]
> Traffic-filtering allow/deny rules on the WAN/LAN interfaces are not covered by this project — it scopes specifically to the logging rule and the receiving-side check.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🔥 **[pfSense](https://www.pfsense.org)** · 🛡️ **[Wazuh](https://wazuh.com)** · 📡 **[Syslog Protocol](https://datatracker.ietf.org/doc/html/rfc5424)** · 🧭 **[Rule Pipeline](README.md#rule-pipeline)**

</div>
