<a id="top"></a>
<div align="center">

# 🕵️ Project 18 — Index
### Mantooth Investigation — Autopsy Triage & Windows Artefact Analysis
**Project 18 of 18 — Advanced Cyber Projects**

![Autopsy](https://img.shields.io/badge/Autopsy_4.23.1-2E4053?style=for-the-badge)
![E01](https://img.shields.io/badge/EWF%2FE01_Image-8E44AD?style=for-the-badge)
![NTFS](https://img.shields.io/badge/NTFS_Analysis-217346?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete_(Lab_1_Scope)-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🗂️ Deleted Files Found | 🎯 Questions Covered |
|:---:|:---:|:---:|:---:|
| **3** | **17** | **276** | **9 (Q1–Q7, Q10, Q11)** |

</div>

<p align="center">🧩 <b>Case:</b> Mantooth.E01 ➜ Autopsy ingest ➜ Triage (encryption, deleted files, EXIF, web, email) ➜ Windows artefacts (Recycle Bin, Prefetch, USB)</p>

---

## 📑 Step Index

All 12 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Create the case and configure ingest | 🔵 Module 1 | Mantooth.E01 added, ingest modules selected | [Exhibit 1](#ex1), [2](#ex2) |
| 2 | Verify the image MD5 hash | 🔵 Module 1 | MD5 `31217210a1a69f272079a3bde3d9d8fc` confirmed | [Exhibit 3](#ex3) |
| 3 | Document the partition layout | 🔵 Module 1 | Four volumes; vol2 holds the Windows installation | [Exhibit 4](#ex4) |
| 4 | Find encrypted files | 🟠 Module 2 | 2 password-protected files flagged Notable | [Exhibit 5](#ex5) |
| 5 | Review deleted files | 🟠 Module 2 | 261 file-system / 276 total deleted files | [Exhibit 6](#ex6), [7](#ex7) |
| 6 | Read photo EXIF metadata | 🟠 Module 2 | 8 photographs, Sony / Kodak / Olympus models seen | [Exhibit 8](#ex8) |
| 7 | Review web search history | 🟠 Module 2 | "check washing", "making meth", "atm card stealing" | [Exhibit 9](#ex9) |
| 8 | Recover email addresses | 🟠 Module 2 | 61 entries from Outlook.pst and .eml files | [Exhibit 10](#ex10) |
| 9 | Identify the operating system | 🟢 Module 3 | WESMANTOOTH-PC, Windows Vista Ultimate (x86) | [Exhibit 11](#ex11) |
| 10 | Recover the Recycle Bin cleanup | 🟢 Module 3 | CameraShy.exe deleted 2007-07-14 22:55:57 | [Exhibit 12](#ex12) |
| 11 | Check Xcopy in Prefetch | 🟢 Module 3 | Run count 15, last run 2007-08-24 17:47:33 | [Exhibit 13](#ex13), [14](#ex14), [15](#ex15) |
| 12 | Review USB device history | 🟢 Module 3 | Canon IXUS 700 and two flash drives identified | [Exhibit 16](#ex16), [17](#ex17) |

---

## 🔵 Module 1 — Case Setup & Image Verification

Exhibits 1 to 4. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-add-data-source-wizard.PNG"><img src="screenshots/ss-01-add-data-source-wizard.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Add Data Source wizard</b>
<br><sub>Select Data Source step, before browsing to Mantooth.E01</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-configure-ingest-modules.PNG"><img src="screenshots/ss-02-configure-ingest-modules.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Ingest modules</b>
<br><sub>Modules selected for the run (Keyword Search deselected)</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-md5-hash-container-tab.PNG"><img src="screenshots/ss-03-md5-hash-container-tab.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — MD5 hash</b>
<br><sub>Container tab with MD5 and acquisition metadata from the E01 header</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-partition-layout-4volumes.PNG"><img src="screenshots/ss-04-partition-layout-4volumes.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Partition layout</b>
<br><sub>Four volumes; vol2 (NTFS/exFAT) is the Windows installation</sub>
</td>
</tr>
</table>

---

## 🟠 Module 2 — Targeted Triage Findings

Exhibits 5 to 10.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex5"></a>
<a href="screenshots/ss-05-encryption-detected-2files.PNG"><img src="screenshots/ss-05-encryption-detected-2files.PNG" width="280" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Encrypted files</b>
<br><sub>Two password-protected documents flagged Notable</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex6"></a>
<a href="screenshots/ss-06-deleted-files-overview.PNG"><img src="screenshots/ss-06-deleted-files-overview.PNG" width="280" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Deleted files overview</b>
<br><sub>File System (261) and All (276)</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex7"></a>
<a href="screenshots/ss-07-deleted-files-full-listing.PNG"><img src="screenshots/ss-07-deleted-files-full-listing.PNG" width="280" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Deleted files listing</b>
<br><sub>Full 276-entry listing, sorted by name</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex8"></a>
<a href="screenshots/ss-08-exif-metadata-8photos.PNG"><img src="screenshots/ss-08-exif-metadata-8photos.PNG" width="280" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — EXIF metadata</b>
<br><sub>8 photographs with Date Created and Device Model</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex9"></a>
<a href="screenshots/ss-09-web-search-results.PNG"><img src="screenshots/ss-09-web-search-results.PNG" width="280" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — Web search history</b>
<br><sub>Repeated fraud-related searches via google.com</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex10"></a>
<a href="screenshots/ss-10-email-addresses-recovered.PNG"><img src="screenshots/ss-10-email-addresses-recovered.PNG" width="280" alt="Exhibit 10"></a>
<br><b>Exhibit 10 — Email addresses</b>
<br><sub>61 entries from Outlook.pst and .eml files</sub>
</td>
</tr>
</table>

---

## 🟢 Module 3 — Windows Artefact Hunting

Exhibits 11 to 17.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex11"></a>
<a href="screenshots/ss-11-os-information-wesmantoothpc.PNG"><img src="screenshots/ss-11-os-information-wesmantoothpc.PNG" width="280" alt="Exhibit 11"></a>
<br><b>Exhibit 11 — OS information</b>
<br><sub>WESMANTOOTH-PC, Windows Vista Ultimate, x86</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex12"></a>
<a href="screenshots/ss-12-recyclebin-camerashy-exe.PNG"><img src="screenshots/ss-12-recyclebin-camerashy-exe.PNG" width="280" alt="Exhibit 12"></a>
<br><b>Exhibit 12 — Recycle Bin</b>
<br><sub>CameraShy.exe deletion record with the Hacker Stuff DLL and ValidateCreditCa zip</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex13"></a>
<a href="screenshots/ss-13-prefetch-runprograms-listing.PNG"><img src="screenshots/ss-13-prefetch-runprograms-listing.PNG" width="280" alt="Exhibit 13"></a>
<br><b>Exhibit 13 — Prefetch listing</b>
<br><sub>Run Programs, 18 entries including XCOPY.EXE</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex14"></a>
<a href="screenshots/ss-14-xcopy-selected-in-list.PNG"><img src="screenshots/ss-14-xcopy-selected-in-list.PNG" width="280" alt="Exhibit 14"></a>
<br><b>Exhibit 14 — Xcopy selected</b>
<br><sub>XCOPY.EXE-8E0707F2.pf among system prefetch entries</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex15"></a>
<a href="screenshots/ss-15-xcopy-prefetch-detail.PNG"><img src="screenshots/ss-15-xcopy-prefetch-detail.PNG" width="280" alt="Exhibit 15"></a>
<br><b>Exhibit 15 — Xcopy detail</b>
<br><sub>Run count 15, last run 2007-08-24 17:47:33</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex16"></a>
<a href="screenshots/ss-16-usb-device-attached-listing.PNG"><img src="screenshots/ss-16-usb-device-attached-listing.PNG" width="280" alt="Exhibit 16"></a>
<br><b>Exhibit 16 — USB devices</b>
<br><sub>30 entries: flash drives, mice, Canon camera</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex17"></a>
<a href="screenshots/ss-17-usb-device-id-column.PNG"><img src="screenshots/ss-17-usb-device-id-column.PNG" width="280" alt="Exhibit 17"></a>
<br><b>Exhibit 17 — USB Device IDs</b>
<br><sub>Distinct IDs for the Canon camera and both flash drives</sub>
</td>
<td></td>
<td></td>
</tr>
</table>

---

## 🎯 Key Findings

| Artefact | Finding | Exhibit |
|---|---|---|
| Encryption Detection | `How To Steal Credit Numbers.doc` and `Those who owes.xls` password-protected | [5](#ex5) |
| Web Search | "check washing", "making meth", "atm card stealing" searched repeatedly on 2007-07-12 | [9](#ex9) |
| Recycle Bin | CameraShy.exe, a "Hacker Stuff" DLL and `ValidateCreditCa....zip` deleted within ~70 seconds | [12](#ex12) |
| Prefetch | XCOPY.EXE run 15 times, last on 2007-08-24 | [15](#ex15) |
| USB Device Attached | Canon Digital IXUS 700 and two Silicon Integrated Systems flash drives | [16](#ex16), [17](#ex17) |

> [!NOTE]
> All timestamps are shown as recorded in Autopsy with the case time zone Asia/Karachi (GMT+5:00); apply −12 hours for Mountain Time. The 30 USB entries share one timestamp, which most likely reflects a single driver-database enumeration, not 30 connections. Items without a screenshot are listed under Scope & Limitations in the README.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🔍 **[Autopsy](https://www.autopsy.com)** · 🧭 **[README Troubleshooting Pipeline](README.md#troubleshooting-pipeline)**

</div>
