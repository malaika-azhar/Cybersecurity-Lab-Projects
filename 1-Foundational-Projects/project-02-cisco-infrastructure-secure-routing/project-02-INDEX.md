<a id="top"></a>
<div align="center">

# 🌐 Project 02 — Index
### Cisco Infrastructure & Secure Routing
**Project 02 of 10 — Foundational Projects**

![Cisco](https://img.shields.io/badge/Cisco_Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![ACL](https://img.shields.io/badge/ACL-Host--Specific_Block-943126?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🔒 ACL Rule Lines | 🎯 Hosts Tested |
|:---:|:---:|:---:|:---:|
| **8** | **7** | **2** | **1** |

</div>

<p align="center">🧩 <b>Lab:</b> Router 2911 + Switch 2960 + 3 PCs · Cisco Packet Tracer</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Open the workspace | 🔵 Module 1 | Blank Packet Tracer workspace ready | [Exhibit 1](#ex1) |
| 2 | Design the topology | 🔵 Module 2 | Router, switch, 3 PCs cabled; link lights red | [Exhibit 2](#ex2) |
| 3 | Configure router interface | 🟠 Module 3 | Gig0/0 activated, routing table verified | [Exhibit 3](#ex3) |
| 4 | Assign static IPs | 🟠 Module 4 | PC0/PC1/PC2 addressed on 192.168.1.0/24 | [Exhibit 4](#ex4) |
| 5 | Test baseline connectivity | 🟢 Module 5 | PC0 → router, 4/4 replies | [Exhibit 5](#ex5) |
| 6 | Deploy the ACL | 🔴 Module 6 | `deny host 192.168.1.30` + `permit any` | [Exhibit 6](#ex6) |
| 7 | Test PC1 (not named in the ACL) | 🟢 Module 7 | PC1 → router succeeds (allowed) | [Exhibit 7](#ex7) |
| 8 | PC2 under the ACL | 🔴 Module 8 | Denied by `deny host 192.168.1.30` (by rule) | [Exhibit 6](#ex6) |

---

## 🔵 Module 1–2 — Build the Topology

Exhibits 1 to 2.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/1_Cisco_Packet_Tracer_Workspace.PNG"><img src="screenshots/1_Cisco_Packet_Tracer_Workspace.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Blank workspace</b>
<br><sub>Packet Tracer opened, ready to place devices</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/2_Network_Topology_Design.PNG"><img src="screenshots/2_Network_Topology_Design.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Topology cabled</b>
<br><sub>Router, switch, 3 PCs connected; link lights still red</sub>
</td>
</tr>
</table>

---

## 🟠 Module 3–4 — Router & Addressing

Exhibits 3 to 4.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/3_Router_IP_and_Routing_Table.PNG"><img src="screenshots/3_Router_IP_and_Routing_Table.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Interface activated</b>
<br><sub><code>no shutdown</code> run; routing table confirmed</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/4_PC_IP_Configuration.PNG"><img src="screenshots/4_PC_IP_Configuration.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Static IPs assigned</b>
<br><sub>PC0, PC1, PC2 addressed on 192.168.1.0/24</sub>
</td>
</tr>
</table>

---

## 🟢 Module 5 — Baseline Test

Exhibit 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/5_Ping_Success_Test.PNG"><img src="screenshots/5_Ping_Success_Test.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Pre-firewall connectivity</b>
<br><sub>PC0 → router, 4/4 replies before any ACL</sub>
</td>
<td></td>
</tr>
</table>

---

## 🔴 Module 6 — Deploy the ACL

Exhibit 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/6_Router_First_Firewall_Rules.PNG"><img src="screenshots/6_Router_First_Firewall_Rules.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — ACL deployed</b>
<br><sub><code>deny host 192.168.1.30</code> + <code>permit any</code></sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 7–8 — Check the ACL Scope

Exhibit 7.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/7_PC1_Firewall_Bypass_Ping_Success.PNG"><img src="screenshots/7_PC1_Firewall_Bypass_Ping_Success.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — PC1 allowed</b>
<br><sub>PC1 is not named in the rule, so it gets through</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Interface activated | `no shutdown`, `show ip route` | Module 3 | ✅ Confirmed |
| Static IPs assigned | Desktop → IP Configuration | Module 4 | ✅ Confirmed |
| Baseline connectivity | `ping` from PC0 | Module 5 | ✅ Confirmed |
| Non-target host still allowed | `ping` from PC1 | Module 7 | ✅ Confirmed (allowed) |
| Target host blocked | Follows from the deny rule | Module 8 | ✅ By rule (Exhibit 6) |

> [!NOTE]
> PC1 (allowed) shows the ACL does not affect unnamed hosts. PC2's block is explained from the rule.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🌐 **[Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)** · 🔒 **[Cisco ACL Guide](https://www.cisco.com/c/en/us/support/docs/security/ios-firewall/23602-confaccesslists.html)**

</div>
