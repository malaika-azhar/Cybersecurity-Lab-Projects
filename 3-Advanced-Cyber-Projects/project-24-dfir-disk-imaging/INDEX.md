<a id="top"></a>
<div align="center">

# 🕵️ Project 24 — Index
### DFIR Foundations — Disk Imaging & File Systems
**Project 24 of 29 — Advanced Cyber Projects**

![Kali](https://img.shields.io/badge/Host-Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![EnCase](https://img.shields.io/badge/Image_Format-EnCase_E01-6C3483?style=for-the-badge)
![NTFS](https://img.shields.io/badge/Filesystem-NTFS-1E8449?style=for-the-badge)
![Sleuth Kit](https://img.shields.io/badge/Toolkit-The_Sleuth_Kit-CA6F1E?style=for-the-badge)
![Chain of Custody](https://img.shields.io/badge/Focus-Chain_of_Custody-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🛠️ Tool Substitutions | 💰 Cost |
|:---:|:---:|:---:|:---:|
| **2** | **11** | **5, all disclosed** | **$0** |

</div>

<p align="center">🧩 <b>Lab:</b> 500 MB controlled NTFS evidence source ➜ E01 image ➜ ADS + MACB analysis ➜ Sleuth Kit CLI triage</p>

---

## 📑 Step Index

All 9 steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Hash the source before acquisition | 🔵 Module 1 | Baseline MD5/SHA256 established | [Exhibit 1](#ex1) |
| 2 | Acquire the E01 image | 🔵 Module 1 | Full chain-of-custody metadata embedded | [Exhibit 2](#ex2) |
| 3 | Independently re-verify the hash | 🔵 Module 1 | `ewfverify` — SUCCESS, hash matches | [Exhibit 3](#ex3) |
| 4 | Mount read-only and confirm integrity | 🔵 Module 1 | Both original files present, unmodified | [Exhibit 4](#ex4) |
| 5 | Mount with stream support, create hidden stream | 🟢 Module 2 | Default stream unchanged at 14 bytes | [Exhibit 5](#ex5) |
| 6 | Recover the hidden stream by name | 🟢 Module 2 | 27-byte hidden payload fully recovered | [Exhibit 6](#ex6) · [Exhibit 7](#ex7) |
| 7 | Extract MACB timestamps | 🟢 Module 2 | Birth time confirmed via `stat` | [Exhibit 8](#ex8) |
| 8 | Verify file system structure | 🟢 Module 2 | NTFS structure confirmed via `fsstat` | [Exhibit 9](#ex9) |
| 9 | Enumerate and recover deleted files | 🟢 Module 2 | Exact content recovered from orphaned MFT record | [Exhibit 10](#ex10) · [Exhibit 11](#ex11) |

---

## 🔵 Module 1 — Acquisition & Hash Verification

Exhibits 1 to 4. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="25%">
<a id="ex1"></a>
<a href="screenshots/Exhibit01_source_hash.png"><img src="screenshots/Exhibit01_source_hash.png" width="220" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Source hash</b>
<br><sub>Baseline MD5/SHA256 before acquisition</sub>
</td>
<td align="center" valign="top" width="25%">
<a id="ex2"></a>
<a href="screenshots/Exhibit02_e01_acquisition.png"><img src="screenshots/Exhibit02_e01_acquisition.png" width="220" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — E01 acquired</b>
<br><sub><code>ewfacquire</code> success, hash matches source</sub>
</td>
<td align="center" valign="top" width="25%">
<a id="ex3"></a>
<a href="screenshots/Exhibit03_ewfverify.png"><img src="screenshots/Exhibit03_ewfverify.png" width="220" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Re-verified</b>
<br><sub><code>ewfverify</code> independent hash confirmation</sub>
</td>
<td align="center" valign="top" width="25%">
<a id="ex4"></a>
<a href="screenshots/Exhibit04_readonly_mount.png"><img src="screenshots/Exhibit04_readonly_mount.png" width="220" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Read-only mount</b>
<br><sub>Both files present, unmodified</sub>
</td>
</tr>
</table>

---

## 🟢 Module 2 — NTFS Internals & Sleuth Kit Triage

Exhibits 5 to 11.

<table>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex5"></a>
<a href="screenshots/Exhibit05_ads_mount_streams.png"><img src="screenshots/Exhibit05_ads_mount_streams.png" width="280" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Stream-aware mount</b>
<br><sub>Hidden stream visible to <code>getfattr</code></sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex6"></a>
<a href="screenshots/Exhibit06_ads_hidden_content.png"><img src="screenshots/Exhibit06_ads_hidden_content.png" width="280" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Hidden content recovered</b>
<br><sub>27-byte stream read back by name</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex7"></a>
<a href="screenshots/Exhibit07_ads_verification.png"><img src="screenshots/Exhibit07_ads_verification.png" width="280" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Full ADS sequence</b>
<br><sub>Default vs. hidden stream side by side</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex8"></a>
<a href="screenshots/Exhibit08_macb_timestamps.png"><img src="screenshots/Exhibit08_macb_timestamps.png" width="280" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — MACB timestamps</b>
<br><sub>Birth time as the most reliable indicator</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex9"></a>
<a href="screenshots/Exhibit09_fsstat_filesystem_info.png"><img src="screenshots/Exhibit09_fsstat_filesystem_info.png" width="280" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — fsstat output</b>
<br><sub>NTFS structure confirmed, clean acquisition</sub>
</td>
<td align="center" valign="top" width="33%">
<a id="ex10"></a>
<a href="screenshots/Exhibit10_fls_deleted_files.png"><img src="screenshots/Exhibit10_fls_deleted_files.png" width="280" alt="Exhibit 10"></a>
<br><b>Exhibit 10 — Orphaned MFT records</b>
<br><sub><code>fls -rd</code> enumeration</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="33%">
<a id="ex11"></a>
<a href="screenshots/Exhibit11_icat_recovered_content.png"><img src="screenshots/Exhibit11_icat_recovered_content.png" width="280" alt="Exhibit 11"></a>
<br><b>Exhibit 11 — Deleted content recovered</b>
<br><sub><code>icat</code> recovers exact original text</sub>
</td>
<td></td>
<td></td>
</tr>
</table>

---

## 🎯 Tool Substitution Summary

| Windows Tool (Brief) | Linux Substitute Used | Status |
|---|---|:---:|
| FTK Imager | `ewfacquire` / `ewfverify` | ✅ Disclosed |
| Arsenal Image Mounter | Read-only loop mount | ✅ Disclosed |
| MFT Explorer | `stat` against the mounted file | ✅ Disclosed |
| Autopsy GUI | The Sleuth Kit CLI (`fsstat`, `fls`, `icat`) | ✅ Disclosed |

> [!NOTE]
> Both `fsstat` and `fls` segfaulted on exit — but only after printing complete, valid output. The data produced is not discarded by the crash; this is documented in the full README.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🕵️ **[The Sleuth Kit](https://www.sleuthkit.org)** · 💾 **[libewf](https://github.com/libyal/libewf)** · 🐧 **[ntfs-3g](https://github.com/tuxera/ntfs-3g)** · 🔍 **[Forensic Pipeline](README.md#forensic-pipeline)**

</div>
