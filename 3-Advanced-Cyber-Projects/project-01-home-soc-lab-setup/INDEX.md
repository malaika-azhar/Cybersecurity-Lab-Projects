<a id="top"></a>
<div align="center">

# 🛡️ Project 01 — Index
### Home SOC Lab Setup
**Project 01 of 18 — Blue Team Internship Portfolio**

![VMware](https://img.shields.io/badge/VMware_Workstation-607078?style=for-the-badge&logo=vmware&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu_Server_22.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh_Cloud_4.14.5-3AAFDA?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots |
|:---:|:---:|
| **2** | **9** |

</div>

<p align="center">🧩 <b>Lab:</b> 1 Ubuntu Server VM · Wazuh Cloud SIEM · VMware Workstation</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Create the VM and allocate hardware | 🔵 Module 1 | Ubuntu Server 22.04.5, 2048 MB RAM, 2 CPU cores | [Exhibit 1](#ex1) |
| 2 | Profile configuration | 🔵 Module 1 | Guest profile set during VM creation | [Exhibit 2](#ex2) |
| 3 | Network configuration during install | 🔵 Module 1 | NAT + Host-only adapters configured | [Exhibit 3](#ex3) |
| 4 | IP address confirmation | 🔵 Module 1 | Both interfaces up (`192.168.48.x` / `192.168.92.x`) | [Exhibit 4](#ex4) |
| 5 | Connectivity test | 🔵 Module 1 | `ping 8.8.8.8` — 0% packet loss | [Exhibit 5](#ex5) |
| 6 | Take rollback snapshot | 🔵 Module 1 | `Ubuntu-Working-Day2` saved | [Exhibit 6](#ex6) |
| 7 | Local Wazuh install pre-flight check | 🟠 Module 2 | 2GB VM flagged below recommended minimum | [Exhibit 7](#ex7) |
| 8 | Bypass attempt with `-i` flag | 🟠 Module 2 | Installer re-run; Indexer stage still risky | [Exhibit 8](#ex8) |
| 9 | Pivot to Wazuh Cloud and log in | 🟠 Module 2 | Cloud dashboard live, no agents yet | [Exhibit 9](#ex9) |

---

## 🔵 Module 1 — VM Lab Setup

Exhibits 1 to 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-vm-creation-hardware-config.PNG"><img src="screenshots/ss-01-vm-creation-hardware-config.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — VM creation</b>
<br><sub>Ubuntu Server 22.04.5, 2048 MB RAM, 2 CPU cores</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-profile-configuration.PNG"><img src="screenshots/ss-02-profile-configuration.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Profile configuration</b>
<br><sub>Guest profile set during VM creation</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-network-config-during-install.PNG"><img src="screenshots/ss-03-network-config-during-install.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Network during install</b>
<br><sub>NAT + Host-only adapters configured</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-ip-address-confirmation.PNG"><img src="screenshots/ss-04-ip-address-confirmation.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — IP confirmation</b>
<br><sub><code>ip a</code> shows both interfaces up with addresses</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-connectivity-test-ping.PNG"><img src="screenshots/ss-05-connectivity-test-ping.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Connectivity test</b>
<br><sub><code>ping -c 4 8.8.8.8</code> — 0% packet loss</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/ss-06-snapshot-ubuntu-working-day2.PNG"><img src="screenshots/ss-06-snapshot-ubuntu-working-day2.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Rollback snapshot</b>
<br><sub><code>Ubuntu-Working-Day2</code> taken before Wazuh</sub>
</td>
</tr>
</table>

---

## 🟠 Module 2 — Wazuh Manager Setup

Exhibits 7 to 9.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/ss-07-wazuh-preflight-check-fail.PNG"><img src="screenshots/ss-07-wazuh-preflight-check-fail.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Pre-flight check fails</b>
<br><sub>Installer flags the 2GB VM as below minimum</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/ss-08-wazuh-install-i-flag-bypass.PNG"><img src="screenshots/ss-08-wazuh-install-i-flag-bypass.PNG" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — <code>-i</code> flag bypass</b>
<br><sub>Installer re-run to skip the pre-flight check</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex9"></a>
<a href="screenshots/ss-09-wazuh-cloud-dashboard-login.PNG"><img src="screenshots/ss-09-wazuh-cloud-dashboard-login.PNG" width="380" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — Wazuh Cloud live</b>
<br><sub>Admin login; no agents registered yet</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Dual-adapter networking | `ip a` | Module 1 | ✅ Confirmed |
| Internet via NAT | `ping -c 4 8.8.8.8` | Module 1 | ✅ Confirmed |
| Local install blocked by RAM | Installer pre-flight check | Module 2 | ✅ Confirmed (documented) |
| Cloud SIEM live | Wazuh Cloud dashboard login | Module 2 | ✅ Confirmed |

> [!NOTE]
> Every substitution (one VM, Wazuh Cloud, VMware) follows the plan approved by program support. Kali Linux VM is deferred until a RAM upgrade.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh](https://wazuh.com)** · 🖥️ **[VMware Workstation](https://www.vmware.com/products/workstation-pro.html)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)**

</div>
