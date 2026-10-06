<a id="top"></a>
<div align="center">

# 🏢 Project 10 — Index
### Enterprise Network VLAN & Inter-VLAN Routing
**Project 10 of 10 — Foundational Projects**

![Packet Tracer](https://img.shields.io/badge/Cisco-Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![VTP](https://img.shields.io/badge/VTP-Server_%2F_Client-005EB8?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 VLANs | 🖼️ Screenshots | 🔀 Routing | 🧱 Steps |
|:---:|:---:|:---:|:---:|
| **3** | **21** | **Router-on-a-Stick** | **21** |

</div>

<p align="center">🧩 <b>Lab:</b> 2× Switch 2960 + Router 2911 · VTP · DHCP · SSH · ACL</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Build the topology | 🔵 Module 1 | 2 switches, router, 5 end devices wired | [Exhibit 1](#ex1) |
| 2 | Configure VTP server (Switch1) | 🟢 Module 2 | VTP mode server, domain malaika.lab | [Exhibit 2](#ex2) |
| 3 | Configure VTP client (Switch2) | 🟢 Module 2 | VTP mode client, joined malaika.lab | [Exhibit 3](#ex3) |
| 4 | Create VLANs on Switch1 | 🟢 Module 2 | VLANs 10/20/99 created | [Exhibit 4](#ex4) |
| 5 | Verify VLAN sync | 🟢 Module 2 | Switch2 checked before trunk was up; sync seen in Exhibit 7 | [Exhibit 5](#ex5) |
| 6 | Configure Switch1 ports | 🟣 Module 3 | Access + trunk ports set | [Exhibit 6](#ex6) |
| 7 | Configure Switch2 ports | 🟣 Module 3 | Access + trunk ports set | [Exhibit 7](#ex7) |
| 8 | Shut down unused ports | 🟠 Module 4 | Switch1 unused ports disabled (VLAN 99) | [Exhibit 8](#ex8) |
| 9 | Enable port security | 🟠 Module 4 | Sticky MAC, max 1, shutdown on violation | [Exhibit 9](#ex9) |
| 10 | Configure management VLAN | 🔴 Module 5 | VLAN 99 SVI addressed (Switch1) | [Exhibit 10](#ex10) |
| 11 | Enable SSH on switches | 🔴 Module 5 | SSH v2 + RSA key configured | [Exhibit 11](#ex11) |
| 12 | Configure router subinterfaces | 🟤 Module 6 | dot1Q per VLAN | [Exhibit 12](#ex12) |
| 13 | Configure DHCP pools | 🟤 Module 6 | Pools for VLAN 10 & 20 | [Exhibit 13](#ex13) |
| 14 | Test PC DHCP | 🟤 Module 6 | PC0 leases an address | [Exhibit 14](#ex14) |
| 15 | Verify DHCP binding | 🟤 Module 6 | 2 leases per pool confirmed on router | [Exhibit 15](#ex15) |
| 16 | Pre-ACL ping test | ⚫ Module 7 | Same-VLAN and cross-VLAN pings succeed | [Exhibit 16](#ex16) |
| 17 | Configure the ACL | ⚫ Module 7 | Deny ICMP VLAN10 → VLAN20 | [Exhibit 17](#ex17) |
| 18 | Test the ACL | ⚫ Module 7 | One direction blocked, one open | [Exhibit 18](#ex18) |
| 19 | Test SSH access | 🟡 Module 8 | PC2 → both switches | [Exhibit 19](#ex19) |
| 20 | Final `show` verification | 🟡 Module 8 | VTP, STP, routes and ACL hits confirmed | [Exhibit 20](#ex20) |
| 21 | Save configuration | 🟡 Module 8 | Switch1 and router saved to startup-config | [Exhibit 21](#ex21) |

---

## 🔵 Module 1 — Topology

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/01-topology.PNG"><img src="screenshots/01-topology.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Full topology</b>
<br><sub>2 switches, router, 5 end devices wired</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 2 — VTP Configuration

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/02-vtp-server.png"><img src="screenshots/02-vtp-server.png" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — VTP server</b>
<br><sub>Switch1, domain malaika.lab, VTP v1</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/03-vtp-client.png"><img src="screenshots/03-vtp-client.png" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — VTP client</b>
<br><sub>Switch2 joined domain malaika.lab</sub>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/04-vlans-created.png"><img src="screenshots/04-vlans-created.png" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — VLANs created</b>
<br><sub>10 (Sales), 20 (IT), 99 (Management)</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/05-vtp-sync.png"><img src="screenshots/05-vtp-sync.png" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Sync check (pre-trunk)</b>
<br><sub>Switch2 before the trunk was up — VLANs not yet synced</sub>
</td>
</tr>
</table>

---

## 🟣 Module 3 — VLAN Ports & Trunks

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/06-switch1-ports.png"><img src="screenshots/06-switch1-ports.png" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Switch1 ports</b>
<br><sub>Access ports + trunks configured</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/07-switch2-ports.png"><img src="screenshots/07-switch2-ports.png" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Switch2 ports</b>
<br><sub>Access ports + trunks configured</sub>
</td>
</tr>
</table>

---

## 🟠 Module 4 — Port Hardening

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/08-unused-ports.png"><img src="screenshots/08-unused-ports.png" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Unused ports shut</b>
<br><sub>Switch1 ports disabled and parked in VLAN 99</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex9"></a>
<a href="screenshots/09-port-security.png"><img src="screenshots/09-port-security.png" width="380" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — Port security</b>
<br><sub>Switch1 Fa0/1–3: sticky MAC, max 1, shutdown</sub>
</td>
</tr>
</table>

---

## 🔴 Module 5 — Management VLAN & SSH

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex10"></a>
<a href="screenshots/10-mgmt-vlan.png"><img src="screenshots/10-mgmt-vlan.png" width="380" alt="Exhibit 10"></a>
<br><b>Exhibit 10 — Management VLAN</b>
<br><sub>Switch1 SVI 192.168.99.2/24 on VLAN 99</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex11"></a>
<a href="screenshots/11-ssh-switches.png"><img src="screenshots/11-ssh-switches.png" width="380" alt="Exhibit 11"></a>
<br><b>Exhibit 11 — SSH enabled</b>
<br><sub>RSA key + SSH v2 on VTY lines</sub>
</td>
</tr>
</table>

---

## 🟤 Module 6 — InterVLAN Routing & DHCP

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex12"></a>
<a href="screenshots/12-router-config.png"><img src="screenshots/12-router-config.png" width="380" alt="Exhibit 12"></a>
<br><b>Exhibit 12 — Subinterfaces</b>
<br><sub>dot1Q per VLAN with gateway addresses</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex13"></a>
<a href="screenshots/13-dhcp-pools.png"><img src="screenshots/13-dhcp-pools.png" width="380" alt="Exhibit 13"></a>
<br><b>Exhibit 13 — DHCP pools</b>
<br><sub>VLAN10-SALES, VLAN20-IT</sub>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex14"></a>
<a href="screenshots/14-pc-dhcp.png"><img src="screenshots/14-pc-dhcp.png" width="380" alt="Exhibit 14"></a>
<br><b>Exhibit 14 — PC DHCP lease</b>
<br><sub>PC0 receives an address</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex15"></a>
<a href="screenshots/15-dhcp-binding.png"><img src="screenshots/15-dhcp-binding.png" width="380" alt="Exhibit 15"></a>
<br><b>Exhibit 15 — Pool &amp; lease check</b>
<br><sub>2 leases per pool; tail of binding table</sub>
</td>
</tr>
</table>

---

## ⚫ Module 7 — ACL Configuration & Testing

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex16"></a>
<a href="screenshots/16-pre-acl-ping.png"><img src="screenshots/16-pre-acl-ping.png" width="380" alt="Exhibit 16"></a>
<br><b>Exhibit 16 — Pre-ACL test</b>
<br><sub>Same-VLAN and cross-VLAN pings succeed before any ACL</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex17"></a>
<a href="screenshots/17-acl-config.png"><img src="screenshots/17-acl-config.png" width="380" alt="Exhibit 17"></a>
<br><b>Exhibit 17 — ACL BLOCK-SALES-TO-IT</b>
<br><sub>Denies ICMP VLAN10 → VLAN20, inbound on Gi0/0.10</sub>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex18"></a>
<a href="screenshots/18-acl-test.png"><img src="screenshots/18-acl-test.png" width="380" alt="Exhibit 18"></a>
<br><b>Exhibit 18 — ACL tested</b>
<br><sub>One direction blocked, the other still passes</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟡 Module 8 — Final Verification & Save

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex19"></a>
<a href="screenshots/19-ssh-test.png"><img src="screenshots/19-ssh-test.png" width="380" alt="Exhibit 19"></a>
<br><b>Exhibit 19 — SSH test</b>
<br><sub>PC2 connects to both switches</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex20"></a>
<a href="screenshots/20-final-verify.png"><img src="screenshots/20-final-verify.png" width="380" alt="Exhibit 20"></a>
<br><b>Exhibit 20 — Final verification</b>
<br><sub>VTP server, STP, routes, ACL hit count</sub>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex21"></a>
<a href="screenshots/21-save-config.png"><img src="screenshots/21-save-config.png" width="380" alt="Exhibit 21"></a>
<br><b>Exhibit 21 — Config saved</b>
<br><sub>Saved on Switch1 and the router</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| VLANs synced without re-creation | `show vlan brief` on Switch2 | Modules 2–3 (Exhibit 7) | ✅ Confirmed |
| Port security active on Switch1 | `show port-security` | Module 4 | ✅ Confirmed |
| SSH reachable on both switches | `ssh` from PC2 | Modules 5, 8 | ✅ Confirmed |
| DHCP leases granted | `show ip dhcp pool` | Module 6 | ✅ Confirmed |
| ACL blocks ICMP in exactly one direction | Pre/post ping test | Module 7 | ✅ Confirmed |
| Config persisted (Switch1, router) | `copy running-config startup-config` | Module 8 | ✅ Confirmed |

> [!NOTE]
> The ACL (Module 7) is intentionally one-directional and ICMP-only — ICMP from VLAN 10 → VLAN 20 is blocked while VLAN 20 → VLAN 10 stays open, verified with a before/after ping test rather than assumed from the config alone.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🔀 **[VTP Explained](https://www.cisco.com/c/en/us/support/docs/lan-switching/vtp/98154-vtp-faq.html)** · 🔐 **[Configuring SSH on IOS](https://www.cisco.com/c/en/us/support/docs/security-vpn/secure-shell-ssh/4145-ssh.html)** · 🛡️ **[ACL Overview](https://www.cisco.com/c/en/us/support/docs/ip/access-lists/26448-ACLsamples.html)**

</div>
