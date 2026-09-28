<a id="top"></a>
<div align="center">

# 🕵️ Project 05 — Index
### Network Forensics — FTP Brute Force & Malware Upload
**Project 05 of 10 — Foundational Projects**

![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![TryHackMe](https://img.shields.io/badge/TryHackMe-212C42?style=for-the-badge&logo=tryhackme&logoColor=white)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🔑 Credentials | 🚩 Malicious File |
|:---:|:---:|:---:|:---:|
| **7** | **6** | **password123** | **shell.php** |

</div>

<p align="center">🧩 <b>Lab:</b> TryHackMe "h4cked" · Wireshark · <code>capture.pcapng</code></p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Find a usable lab file | 🔵 Module 1 | Free "h4cked" room selected | — |
| 2 | Load the capture in Wireshark | 🔵 Module 2 | `capture.pcapng` opened | [Exhibit 1](#ex1) |
| 3 | Isolate the attacker's traffic | 🟠 Module 3 | `ftp` filter → attacker IP found | [Exhibit 2](#ex2) |
| 4 | Capture the brute-force attempt | 🟠 Module 4 | Plaintext failed logins read | [Exhibit 3](#ex3) |
| 5 | Confirm the breach | 🟢 Module 5 | `230 Login successful` | [Exhibit 4](#ex4) |
| 6 | Diagnose the missing payload | 🔴 Module 6 | `STOR shell.php` isolated | [Exhibit 5](#ex5) |
| 7 | Confirm upload & escalation | 🟢 Module 7 | Transfer complete + `CHMOD 777` | [Exhibit 6](#ex6) |

---

## 🔵 Module 2 — Load the Capture

Exhibit 1.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/1_Wireshark_File_Open_Success.PNG"><img src="screenshots/1_Wireshark_File_Open_Success.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Capture loaded</b>
<br><sub>Raw packets visible after opening the file</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠 Module 3–4 — Isolate & Capture

Exhibits 2 to 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/2_FTP_Traffic_Filtered.PNG"><img src="screenshots/2_FTP_Traffic_Filtered.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — FTP filtered</b>
<br><sub>Attacker IP 192.168.0.147 identified</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/3_Hacker_Credentials_Found.PNG"><img src="screenshots/3_Hacker_Credentials_Found.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Brute force captured</b>
<br><sub>Failed plaintext login attempts</sub>
</td>
</tr>
</table>

---

## 🟢 Module 5 — Breach Confirmed

Exhibit 4.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/4_Hacker_Login_Success_and_Directory.PNG"><img src="screenshots/4_Hacker_Login_Success_and_Directory.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Login success</b>
<br><sub><code>230 Login successful</code>, dir <code>/var/www/html</code></sub>
</td>
<td></td>
</tr>
</table>

---

## 🔴 Module 6 — Missing Payload Diagnosed

Exhibit 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/5_Malware_File_Upload_Detected.PNG"><img src="screenshots/5_Malware_File_Upload_Detected.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Upload isolated</b>
<br><sub><code>STOR shell.php</code> found via command filter</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 7 — Upload & Escalation Confirmed

Exhibit 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/6_Malware_Transfer_Complete_and_Permissions.PNG"><img src="screenshots/6_Malware_Transfer_Complete_and_Permissions.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Escalation confirmed</b>
<br><sub>Transfer complete + <code>CHMOD 777</code></sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Attacker IP identified | `ftp` filter | Module 3 | ✅ Confirmed |
| Brute-force attempts read | Plaintext packet inspection | Module 4 | ✅ Confirmed |
| Breach confirmed | `230 Login successful` | Module 5 | ✅ Confirmed |
| Payload found after manual scroll failed | `ftp.request.command == "STOR"` | Module 6 | ✅ Confirmed |
| Escalation confirmed | `226 Transfer complete`, `CHMOD 777` | Module 7 | ✅ Confirmed |

> [!NOTE]
> Manual scrolling failed to locate the malware upload (Module 6) — switching to a command-specific filter is what actually surfaced it. Documented as the real investigative path, not skipped.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🕵️ **[TryHackMe — h4cked Room](https://tryhackme.com/room/hacked)** · 🦈 **[Wireshark Docs](https://www.wireshark.org/docs/)**

</div>
