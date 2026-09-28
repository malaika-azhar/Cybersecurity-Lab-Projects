<a id="top"></a>
<div align="center">

# 🦈 Project 13 — Index
### Network Traffic Analysis (Wireshark)
**Project 10 of 29 — Blue Team Internship Portfolio**

![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![ARP](https://img.shields.io/badge/ARP-C6501F?style=for-the-badge)
![DNS](https://img.shields.io/badge/DNS-2EA043?style=for-the-badge)
![HTTP/TLS](https://img.shields.io/badge/HTTP_%2F_TLS-4A3FA6?style=for-the-badge)
![ICMP](https://img.shields.io/badge/ICMP-8E44AD?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Protocols | 🖼️ Screenshots | 🔌 Ports Documented | 📶 OSI Layers Traced |
|:---:|:---:|:---:|:---:|
| **5** | **6** | **7** | **4** |

</div>

<p align="center">🧩 <b>Capture:</b> Laptop on Wi-Fi ➜ Wireshark, live traffic + one deliberately generated protocol (ICMP)</p>

---

## 📑 Step Index

All 6 steps of the project, with the screenshot that shows each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Diagram the planned lab topology | 🔵 Module 1 | Three-VM, dual-adapter design mapped | [Exhibit 1](#ex1) |
| 2 | Capture ARP | 🟠 Module 2 | Router resolves a known IP to a MAC address | [Exhibit 2](#ex2) |
| 3 | Capture DNS | 🟠 Module 2 | Standard query resolved via CNAME to an IP | [Exhibit 3](#ex3) |
| 4 | Capture HTTP | 🟠 Module 2 | Plain-text GET fetching a Certificate Revocation List | [Exhibit 4](#ex4) |
| 5 | Capture HTTPS/TLS | 🟠 Module 2 | TLSv1.2 Application Data between known hosts | [Exhibit 5](#ex5) |
| 6 | Capture ICMP | 🟠 Module 2 | 4 echo request/reply pairs, generated manually via `ping` | [Exhibit 6](#ex6) |

---

## 🔵 Module 1 — Lab Topology

Exhibit 1. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-lab-topology-diagram.PNG"><img src="screenshots/ss-01-lab-topology-diagram.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Planned lab topology</b>
<br><sub>Three VMs, each with NAT + Host-only adapters</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠 Module 2 — Protocol Capture: Normal vs Suspicious

Exhibits 2 to 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-arp-capture-evidence.PNG"><img src="screenshots/ss-02-arp-capture-evidence.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — ARP</b>
<br><sub>Router resolves a known IP to a MAC address</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-dns-capture-evidence.PNG"><img src="screenshots/ss-03-dns-capture-evidence.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — DNS</b>
<br><sub>Standard query resolved via CNAME to an IP</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-http-capture-evidence.PNG"><img src="screenshots/ss-04-http-capture-evidence.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — HTTP</b>
<br><sub>Plain-text GET fetching a Certificate Revocation List</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-https-tls-capture-evidence.PNG"><img src="screenshots/ss-05-https-tls-capture-evidence.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — HTTPS/TLS</b>
<br><sub>TLSv1.2 Application Data, normal encrypted browsing</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/ss-06-icmp-capture-evidence.PNG"><img src="screenshots/ss-06-icmp-capture-evidence.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — ICMP</b>
<br><sub>4 echo request/reply pairs, generated manually</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| ARP normal resolution captured | Wireshark live capture | Module 2 | ✅ Confirmed |
| DNS normal resolution captured | Wireshark live capture | Module 2 | ✅ Confirmed |
| HTTP plaintext traffic captured | Wireshark live capture | Module 2 | ✅ Confirmed |
| HTTPS/TLS encrypted traffic captured | Wireshark live capture | Module 2 | ✅ Confirmed |
| ICMP traffic captured | `ping -c 4 8.8.8.8` + Wireshark | Module 2 | ✅ Confirmed (required manual generation) |
| A real attack/suspicious packet | — | — | ❌ Not present — suspicious patterns documented conceptually only |

> [!NOTE]
> The "suspicious traffic" side of each protocol reflects known attack patterns, not a captured attack — no real malicious traffic was present on this network. This is stated directly rather than implied.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🦈 **[Wireshark](https://www.wireshark.org)** · 🧭 **[OSI Model](https://en.wikipedia.org/wiki/OSI_model)** · 🧭 **[Troubleshooting Pipeline](README.md#troubleshooting-pipeline)**

</div>
