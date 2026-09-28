<a id="top"></a>
<div align="center">

# 🐧 Project 07 — Index
### Linux Log Analysis & Forensics — SOC Investigation
**Project 07 of 10 — Foundational Projects**

![Linux](https://img.shields.io/badge/Linux_CLI-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![auditd](https://img.shields.io/badge/auditd-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 📜 Log Sources | 🎯 Attack Stages |
|:---:|:---:|:---:|:---:|
| **7** | **7** | **4** | **4** |

</div>

<p align="center">🧩 <b>Lab:</b> Compromised Linux host · <code>syslog</code> / <code>auth.log</code> / <code>dpkg.log</code> / <code>auditd</code></p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Connect & escalate to root | 🔵 Module 1 | SSH + `sudo su` | [Exhibit 1](#ex1) |
| 2 | Analyze syslog | 🔵 Module 2 | Baseline health checked | [Exhibit 2](#ex2) |
| 3 | Check NTP time sync | 🔵 Module 3 | `ntp.ubuntu.com` confirmed | [Exhibit 3](#ex3) |
| 4 | Investigate auth log for brute force | 🔴 Module 4 | `10.14.94.82` identified | [Exhibit 4](#ex4) |
| 5 | Find the backdoor user | 🔴 Module 5 | `xerxes` added to sudo | [Exhibit 5](#ex5) |
| 6 | Check package manager logs | 🟠 Module 6 | `unzip` installed | [Exhibit 6](#ex6) |
| 7 | Analyze auditd records | 🟣 Module 7 | `naabu` download + network scan | [Exhibit 7](#ex7) |

---

## 🔵 Module 1–3 — Baseline

Exhibits 1 to 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/SS1_Linux_Logs_Connection.PNG"><img src="screenshots/SS1_Linux_Logs_Connection.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Root access</b>
<br><sub>SSH connection + <code>sudo su</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/SS2_Syslog_Analysis.PNG"><img src="screenshots/SS2_Syslog_Analysis.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Syslog reviewed</b>
<br><sub>System health baseline</sub>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/SS3_Syslog_Timesync.PNG"><img src="screenshots/SS3_Syslog_Timesync.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — NTP sync confirmed</b>
<br><sub>Timestamp trust established</sub>
</td>
<td></td>
</tr>
</table>

---

## 🔴 Module 4–5 — Breach Evidence

Exhibits 4 to 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/SS4_Auth_Failed_Logins.PNG"><img src="screenshots/SS4_Auth_Failed_Logins.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Brute force found</b>
<br><sub><code>10.14.94.82</code> in auth.log</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/SS5_Auth_Sudo_User.PNG"><img src="screenshots/SS5_Auth_Sudo_User.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Backdoor found</b>
<br><sub><code>xerxes</code> added to sudo</sub>
</td>
</tr>
</table>

---

## 🟠🟣 Module 6–7 — Tooling Evidence

Exhibits 6 to 7.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/SS6_Package_Manager_Logs.PNG"><img src="screenshots/SS6_Package_Manager_Logs.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Tool installed</b>
<br><sub><code>unzip</code> in dpkg.log</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/SS7_Auditd_Analysis.PNG"><img src="screenshots/SS7_Auditd_Analysis.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Scan confirmed</b>
<br><sub><code>naabu</code> download + 192.168.50.0/24 scan</sub>
</td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Timestamps trustworthy | NTP sync source confirmed | Module 3 | ✅ Confirmed |
| Brute-force entry point found | `auth.log` | Module 4 | ✅ Confirmed |
| Backdoor account found | `useradd`/`usermod` filter | Module 5 | ✅ Confirmed |
| Tool installation found | `dpkg.log` | Module 6 | ✅ Confirmed |
| Network scan confirmed | `ausearch` | Module 7 | ✅ Confirmed |

> [!NOTE]
> No single log told the full story — the timeline only became clear by correlating `auth.log`, `dpkg.log`, `syslog`, and `auditd` together.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🐧 **[TryHackMe — Linux Logging for SOC](https://tryhackme.com/room/linuxloggingforsoc)**

</div>
