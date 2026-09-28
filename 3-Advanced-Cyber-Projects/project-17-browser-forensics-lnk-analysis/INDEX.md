<a id="top"></a>
<div align="center">

# 🌐 Project 26 — Index
### Browser Forensics & LNK Analysis
**Project 26 of 29 — Advanced Cyber Projects**

![Chrome](https://img.shields.io/badge/Browser-Chrome-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)
![LECmd](https://img.shields.io/badge/Tool-LECmd-1E8449?style=for-the-badge)
![BrowsingHistoryView](https://img.shields.io/badge/Tool-BrowsingHistoryView-F39C12?style=for-the-badge)
![LNK Files](https://img.shields.io/badge/Analyzed-75%2F75_LNK_Files-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🔗 LNK Files Parsed | ❌ Parse Errors |
|:---:|:---:|:---:|:---:|
| **2** | **10** | **75 / 75** | **0** |

</div>

<p align="center">🧩 <b>Lab:</b> Chrome full artifact set ➜ BrowsingHistoryView export ➜ 75 LNK files ➜ LECmd ➜ Chronological Timeline</p>

---

## 📑 Step Index

All 10 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Locate and copy the Chrome profile | 🔵 Module 1 | Full artifact set identified before analysis | [Exhibit 1](#ex1) |
| 2 | Export and review browsing history | 🔵 Module 1 | Multi-profile history captured | [Exhibit 2](#ex2) |
| 3 | Review download history | 🔵 Module 1 | Task briefs, reports, archive tool identified | [Exhibit 3](#ex3) |
| 4 | Review cookies and site data | 🔵 Module 1 | Storage concentrated on a few frequent domains | [Exhibit 4](#ex4) |
| 5 | Review autofill and stored credentials | 🔵 Module 1 | 6 passwords, 1 address stored | [Exhibit 5](#ex5) |
| 6 | Review installed extensions | 🔵 Module 1 | Google Docs Offline installed and active | [Exhibit 6](#ex6) |
| 7 | Parse all LNK files with LECmd | 🟢 Module 2 | 75/75 processed, zero errors | [Exhibit 7](#ex7) |
| 8 | Review the full parsed output | 🟢 Module 2 | Complete metadata for every shortcut | [Exhibit 8](#ex8) |
| 9 | Confirm no external device via volume serial | 🟢 Module 2 | Single serial across all 75 entries | [Exhibit 9](#ex9) |
| 10 | Build the chronological access timeline | 🟢 Module 2 | Minute-by-minute sorted sequence | [Exhibit 10](#ex10) |

---

## 🔵 Module 1 — Chrome Artifact Review

Exhibits 1 to 6. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex1"></a>
<a href="screenshots/Exhibit01_chrome_userdata_folder.png"><img src="screenshots/Exhibit01_chrome_userdata_folder.png" width="280" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — User Data folder</b>
<br><sub>Full artifact set before any file is queried</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex2"></a>
<a href="screenshots/Exhibit02_browsing_history_export.png"><img src="screenshots/Exhibit02_browsing_history_export.png" width="280" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — History export</b>
<br><sub>Visit time, count, type, and source file</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex3"></a>
<a href="screenshots/Exhibit03_download_history.png"><img src="screenshots/Exhibit03_download_history.png" width="280" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Download history</b>
<br><sub>Documents, archives, and PDFs</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex4"></a>
<a href="screenshots/Exhibit04_cookies_site_data.png"><img src="screenshots/Exhibit04_cookies_site_data.png" width="280" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Cookies & site data</b>
<br><sub>Storage and cookie count per domain</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex5"></a>
<a href="screenshots/Exhibit05_autofill_passwords.png"><img src="screenshots/Exhibit05_autofill_passwords.png" width="280" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Autofill & passwords</b>
<br><sub>Stored credentials and payment data</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex6"></a>
<a href="screenshots/Exhibit06_extensions_listing.png"><img src="screenshots/Exhibit06_extensions_listing.png" width="280" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Extensions</b>
<br><sub>Version, size, ID, and permissions</sub>
</td>
</tr>
</table>

---

## 🟢 Module 2 — LNK Parsing & Timeline Correlation

Exhibits 7 to 10.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/Exhibit07_lecmd_processing_confirmation.png"><img src="screenshots/Exhibit07_lecmd_processing_confirmation.png" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — LECmd processing</b>
<br><sub>75/75 files in 32.13 seconds, zero errors</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/Exhibit08_lecmd_csv_output.png"><img src="screenshots/Exhibit08_lecmd_csv_output.png" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Full CSV output</b>
<br><sub>Timestamps, target paths, machine/MAC IDs</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex9"></a>
<a href="screenshots/Exhibit09_volume_serial_number.png"><img src="screenshots/Exhibit09_volume_serial_number.png" width="380" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — Volume serial check</b>
<br><sub>Single serial across all entries — no USB</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex10"></a>
<a href="screenshots/Exhibit10_chronological_timeline.png"><img src="screenshots/Exhibit10_chronological_timeline.png" width="380" alt="Exhibit 10"></a>
<br><b>Exhibit 10 — Chronological timeline</b>
<br><sub>Sorted by TargetAccessed, minute by minute</sub>
</td>
</tr>
</table>

---

## 🎯 Key Findings Summary

| Finding | Evidence | Status |
|---|---|:---:|
| Edge / Firefox presence | Host check prior to analysis | ❌ Confirmed absent |
| LNK parse success rate | LECmd batch run | ✅ 75 / 75, 0 errors |
| External storage device used | Volume Serial Number comparison | ❌ None found |
| Chronological timeline | `TargetAccessed` sort | ✅ Built, complete |

> [!NOTE]
> A negative finding — no external device ever referenced — is exactly as reportable as a positive one. It directly answers a real investigative question rather than leaving it open.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🌐 **[Chrome](https://www.google.com/chrome/)** · 🔗 **[LECmd](https://ericzimmerman.github.io/#!index.md)** · 🕘 **[BrowsingHistoryView](https://www.nirsoft.net/utils/browsing_history_view.html)** · 🧭 **[Correlation Pipeline](README.md#correlation-pipeline)**

</div>
