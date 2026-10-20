<a id="top"></a>
<div align="center">

# 🛡️ Project 19 — Index
### SIEM Dashboard & Visualizations on Azure
**Project 19 of 20 — Blue Team Defense Projects**

![Azure](https://img.shields.io/badge/Azure_VM-Ubuntu_24.04-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Windows](https://img.shields.io/badge/Windows_10_Pro-Endpoint-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh-4.14.9-3AAFDA?style=for-the-badge)
![MITRE](https://img.shields.io/badge/MITRE-T1110_Brute_Force-B03A2E?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots |
|:---:|:---:|
| **4** | **22** |

</div>

<p align="center">🧩 <b>Lab:</b> Azure Ubuntu VM · Wazuh 4.14.9 SIEM · Windows 10 Pro agent · 11 simulated failed-login alerts for one source IP</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Check the Azure VM | 🔵 Module 1 | `lab-server` Running, Ubuntu 24.04, 4 GiB RAM | [Exhibit 1](#ex1) |
| 2 | Set the inbound firewall rules | 🔵 Module 1 | SSH and HTTPS limited to one IP, agent ports 1514-1515 open | [Exhibit 2](#ex2) |
| 3 | Connect over SSH | 🔵 Module 1 | Placeholder key path failed, real key file worked | [Exhibit 3](#ex3) |
| 4 | Add swap space | 🔵 Module 1 | 4.0Gi swap active | [Exhibit 4](#ex4) |
| 5 | Installer blocked by port 443 | 🟠 Module 2 | `nginx` found on 443, stopped and disabled | [Exhibit 5](#ex5) |
| 6 | Dashboard install fails | 🟠 Module 2 | `No space left on device` in the installer log | [Exhibit 6](#ex6) |
| 7 | Resize the OS disk | 🟠 Module 2 | 30 GiB to 64 GiB (P6) | [Exhibit 7](#ex7) |
| 8 | Remove the broken package | 🟠 Module 2 | `dpkg --purge --force-all` completed | [Exhibit 8](#ex8) |
| 9 | Install completes | 🟠 Module 2 | `Installation finished` (credentials redacted) | [Exhibit 9](#ex9) |
| 10 | Open agent ports in UFW | 🟠 Module 2 | 1514/tcp and 1515/tcp allowed | [Exhibit 10](#ex10) |
| 11 | Reach the dashboard login | 🟠 Module 2 | Login page served over HTTPS | [Exhibit 11](#ex11) |
| 12 | Log in to an empty dashboard | 🟠 Module 2 | "No agents registered" before enrollment | [Exhibit 12](#ex12) |
| 13 | Install the Windows agent | 🟢 Module 3 | MSI installed, `WazuhSvc` started | [Exhibit 13](#ex13) |
| 14 | Confirm the agent is active | 🟢 Module 3 | `malaika-laptop`, v4.14.9, active | [Exhibit 14](#ex14) |
| 15 | Simulate failed logins | 🟢 Module 3 | Repeated SSH attempts as `fakeuser` | [Exhibit 15](#ex15) |
| 16 | Read the alert on the server | 🟢 Module 3 | Rule 5710, level 5, MITRE Credential Access | [Exhibit 16](#ex16) |
| 17 | Find the alerts in Discover | 🟣 Module 4 | `data.srcip` query, 11 hits | [Exhibit 17](#ex17) |
| 18 | Check the index in Dev Tools | 🟣 Module 4 | 770 documents, 5 `fakeuser` hits | [Exhibit 18](#ex18) |
| 19 | Build the pie chart | 🟣 Module 4 | Terms on `data.srcip`, Count, size 5 | [Exhibit 19](#ex19) |
| 20 | Save the dashboard | 🟣 Module 4 | Failed Login Monitoring saved | [Exhibit 20](#ex20) |
| 21 | Review the final firewall | 🟣 Module 4 | 22 and 443 from one IP, HTTP rule removed | [Exhibit 21](#ex21) |
| 22 | Stop the VM | 🟣 Module 4 | Stopped (deallocated) to save credits | [Exhibit 22](#ex22) |

---

## 🔵 Module 1 — Azure VM and Network Setup

Exhibits 1 to 4.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-azure-vm-overview.PNG"><img src="screenshots/ss-01-azure-vm-overview.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Azure VM overview</b>
<br><sub>Running, Ubuntu 24.04, B2ls v2, 4 GiB RAM</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-nsg-inbound-rules.PNG"><img src="screenshots/ss-02-nsg-inbound-rules.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — NSG inbound rules</b>
<br><sub>SSH and HTTPS restricted, agent ports open</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-ssh-connected.PNG"><img src="screenshots/ss-03-ssh-connected.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — SSH connected</b>
<br><sub>Login with the downloaded <code>.pem</code> key</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-swap-enabled.PNG"><img src="screenshots/ss-04-swap-enabled.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Swap enabled</b>
<br><sub><code>free -h</code> shows 4.0Gi swap</sub>
</td>
</tr>
</table>

---

## 🟠 Module 2 — Wazuh Installation and Recovery

Exhibits 5 to 12.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-install-blocked-port-443-nginx.PNG"><img src="screenshots/ss-05-install-blocked-port-443-nginx.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Port 443 in use</b>
<br><sub>Installer error and <code>nginx</code> listening</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/ss-06-install-failed-no-space-left.PNG"><img src="screenshots/ss-06-install-failed-no-space-left.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Disk full</b>
<br><sub><code>No space left on device</code></sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/ss-07-os-disk-resized-64gib.PNG"><img src="screenshots/ss-07-os-disk-resized-64gib.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — OS disk resized</b>
<br><sub>64 GiB, performance tier P6</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/ss-08-broken-package-purge.PNG"><img src="screenshots/ss-08-broken-package-purge.PNG" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Broken package purge</b>
<br><sub><code>dpkg --purge --force-all wazuh-manager</code></sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex9"></a>
<a href="screenshots/ss-09-wazuh-install-finished.PNG"><img src="screenshots/ss-09-wazuh-install-finished.PNG" width="380" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — Install finished</b>
<br><sub><code>Installation finished</code> (credentials redacted)</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex10"></a>
<a href="screenshots/ss-10-ufw-agent-ports.PNG"><img src="screenshots/ss-10-ufw-agent-ports.PNG" width="380" alt="Exhibit 10"></a>
<br><b>Exhibit 10 — UFW agent ports</b>
<br><sub>1514 and 1515 allowed, IPv4 and IPv6</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex11"></a>
<a href="screenshots/ss-11-wazuh-login-page.PNG"><img src="screenshots/ss-11-wazuh-login-page.PNG" width="380" alt="Exhibit 11"></a>
<br><b>Exhibit 11 — Dashboard login page</b>
<br><sub>Served over HTTPS from the Azure VM</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex12"></a>
<a href="screenshots/ss-12-dashboard-no-agents.PNG"><img src="screenshots/ss-12-dashboard-no-agents.PNG" width="380" alt="Exhibit 12"></a>
<br><b>Exhibit 12 — Dashboard before the agent</b>
<br><sub>"No agents registered" on the overview</sub>
</td>
</tr>
</table>

---

## 🟢 Module 3 — Endpoint Agent and Alert Generation

Exhibits 13 to 16.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex13"></a>
<a href="screenshots/ss-13-agent-install-powershell.PNG"><img src="screenshots/ss-13-agent-install-powershell.PNG" width="380" alt="Exhibit 13"></a>
<br><b>Exhibit 13 — Agent install on Windows</b>
<br><sub>MSI installed, service started successfully</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex14"></a>
<a href="screenshots/ss-14-endpoint-agent-active.PNG"><img src="screenshots/ss-14-endpoint-agent-active.PNG" width="380" alt="Exhibit 14"></a>
<br><b>Exhibit 14 — Agent active</b>
<br><sub><code>001 malaika-laptop</code>, v4.14.9, active</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex15"></a>
<a href="screenshots/ss-15-simulated-failed-ssh.PNG"><img src="screenshots/ss-15-simulated-failed-ssh.PNG" width="380" alt="Exhibit 15"></a>
<br><b>Exhibit 15 — Simulated failed logins</b>
<br><sub><code>ssh fakeuser@&lt;VM-Public-IP&gt;</code>, publickey denied</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex16"></a>
<a href="screenshots/ss-16-rule-5710-alert-run-command.PNG"><img src="screenshots/ss-16-rule-5710-alert-run-command.PNG" width="380" alt="Exhibit 16"></a>
<br><b>Exhibit 16 — Rule 5710 alert</b>
<br><sub>Non-existent user, level 5, via Azure Run Command</sub>
</td>
</tr>
</table>

---

## 🟣 Module 4 — Visualization and Dashboard

Exhibits 17 to 22.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex17"></a>
<a href="screenshots/ss-17-discover-srcip-hits.PNG"><img src="screenshots/ss-17-discover-srcip-hits.PNG" width="380" alt="Exhibit 17"></a>
<br><b>Exhibit 17 — Alerts in Discover</b>
<br><sub><code>data.srcip</code> query: 11 hits, last 90 days</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex18"></a>
<a href="screenshots/ss-18-devtools-index-check.PNG"><img src="screenshots/ss-18-devtools-index-check.PNG" width="380" alt="Exhibit 18"></a>
<br><b>Exhibit 18 — Dev Tools index check</b>
<br><sub>770 documents, 5 <code>fakeuser</code> hits</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex19"></a>
<a href="screenshots/ss-19-top-attacker-ips-visualization.PNG"><img src="screenshots/ss-19-top-attacker-ips-visualization.PNG" width="380" alt="Exhibit 19"></a>
<br><b>Exhibit 19 — Top Attacker IPs chart</b>
<br><sub>Terms aggregation on <code>data.srcip</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex20"></a>
<a href="screenshots/ss-20-failed-login-monitoring-dashboard.PNG"><img src="screenshots/ss-20-failed-login-monitoring-dashboard.PNG" width="380" alt="Exhibit 20"></a>
<br><b>Exhibit 20 — Saved dashboard</b>
<br><sub><code>Failed Login Monitoring</code></sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex21"></a>
<a href="screenshots/ss-21-nsg-restricted-final.PNG"><img src="screenshots/ss-21-nsg-restricted-final.PNG" width="380" alt="Exhibit 21"></a>
<br><b>Exhibit 21 — Final firewall rules</b>
<br><sub>22 and 443 from one IP, HTTP rule removed</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex22"></a>
<a href="screenshots/ss-22-vm-deallocated.PNG"><img src="screenshots/ss-22-vm-deallocated.PNG" width="380" alt="Exhibit 22"></a>
<br><b>Exhibit 22 — VM stopped</b>
<br><sub>Stopped (deallocated)</sub>
</td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Azure VM reachable with limited ports | NSG rules, SSH login | Module 1 | ✅ Confirmed |
| Wazuh stack installed | Installer log, dashboard login page | Module 2 | ✅ Confirmed |
| Agent registered and active | Endpoints page | Module 3 | ✅ Confirmed |
| Failed logins detected | Rule 5710 in the alert log, `data.srcip` query | Module 3 | ✅ 11 hits (simulated) |
| Alerts indexed | Dev Tools index count | Module 4 | ✅ 770 documents |
| Visualization saved to a dashboard | Visualize, Dashboards | Module 4 | ✅ Confirmed |
| Real attacker IPs observed | Not part of this lab | Module 4 | ➖ Not shown |
| Export or automation pipeline | Not part of this lab | Module 4 | ➖ Not attempted |

> [!NOTE]
> The simulated attack came from my own laptop against my own VM, so the chart has one slice (my own public IP). Rule 5710 alerts were raised on the VM's own SSH log, not from the Windows agent. Passwords visible in the original captures are blacked out in Exhibit 9. Dashboard times are UTC+5; server logs are UTC.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh](https://wazuh.com)** · ☁️ **[Microsoft Azure](https://azure.microsoft.com)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)**

</div>
