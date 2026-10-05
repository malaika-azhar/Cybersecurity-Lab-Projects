<a id="top"></a>
<div align="center">

# 🗂️ Project 16 — Index
### Windows Artifacts — Prefetch & Thumbcache
**Project 16 of 18 — Blue Team Internship Portfolio**

![Windows](https://img.shields.io/badge/Windows_Prefetch-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![EZTools](https://img.shields.io/badge/PECmd-EZ_Tools-2E4053?style=for-the-badge)
![Robocopy](https://img.shields.io/badge/Robocopy_%2FB-8E44AD?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 .pf Files | 🖼️ Screenshots |
|:---:|:---:|
| **362 / 363** | **7** |

</div>

<p align="center">🧩 <b>Scope:</b> Prefetch execution profile ➜ context-checked Temp-path finding ➜ thumbcache recovery</p>

---

## 📑 Step Index

All 6 steps of the project, with the screenshot that shows each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Copy the Prefetch directory | 🔵 Module 1 | 363 `.pf` files copied | [Exhibit 1](#ex1) |
| 2 | Parse with PECmd | 🔵 Module 1 | 362/363 parsed, 1 corrupted | [Exhibit 2](#ex2) |
| 3 | Build the Top 20 RunCount table | 🟠 Module 2 | Chrome + core Windows processes dominate | [Exhibit 3](#ex3) |
| 4 | Check execution paths for suspicion | 🟠 Module 2 | All top-20 paths standard, no Temp/Downloads hits | Exhibits [4](#ex4), [5](#ex5) |
| 5 | Review the full timeline for Temp-path activity | 🟢 Module 3 | Advanced SystemCare installer found in Temp | [Exhibit 6](#ex6) |
| 6 | Bypass the Explorer lock on thumbcache | 🟣 Module 4 | `thumbcache_1280.db` copied via `robocopy /B` | [Exhibit 7](#ex7) |

---

## 🔵 Module 1 — Prefetch Extraction & Parsing

Exhibits 1 to 2. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-prefetch-copy-confirmation-363files.PNG"><img src="screenshots/ss-01-prefetch-copy-confirmation-363files.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Prefetch copy confirmation</b>
<br><sub>363 .pf files copied to the working directory</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-pecmd-parsing-completion.PNG"><img src="screenshots/ss-02-pecmd-parsing-completion.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — PECmd completion</b>
<br><sub>362/363 processed, 1 corrupted (SYNTPHELPER.EXE)</sub>
</td>
</tr>
</table>

---

## 🟠 Module 2 — Execution Profiling

Exhibits 3 to 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-top20-runcount-table.PNG"><img src="screenshots/ss-03-top20-runcount-table.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Top 20 RunCount table</b>
<br><sub>Chrome + core Windows processes dominate</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-directories-column-reference.PNG"><img src="screenshots/ss-04-directories-column-reference.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Directories column</b>
<br><sub>Working reference for the standard-path check</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-directories-widened-temp-check.PNG"><img src="screenshots/ss-05-directories-widened-temp-check.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — TEMP search check</b>
<br><sub>Standard paths among top-run entries</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 3 — Contextual Investigation: the Temp-Path Installer

Exhibit 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/ss-06-installer-temppath-timeline.PNG"><img src="screenshots/ss-06-installer-temppath-timeline.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Installer Temp-path timeline</b>
<br><sub>Advanced SystemCare Setup, correctly closed as expected</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟣 Module 4 — Thumbcache Recovery

Exhibit 7.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/ss-07-thumbcache-robocopy-confirmation.PNG"><img src="screenshots/ss-07-thumbcache-robocopy-confirmation.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Thumbcache robocopy</b>
<br><sub>Directory listing of <code>thumbcache_1280.db</code> after backup-mode robocopy</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Prefetch directory copied before parsing | `xcopy` | Module 1 | ✅ Confirmed |
| 362/363 files parsed successfully | PECmd | Module 1 | ✅ Confirmed |
| Top 20 programs profiled | RunCount sort | Module 2 | ✅ Confirmed |
| All top-20 paths standard | Directories column check | Module 2 | ✅ Confirmed |
| Temp-path installer investigated in context | Timeline cross-reference | Module 3 | ✅ Confirmed — correctly closed |
| Thumbcache recovered despite Explorer lock | `robocopy /B` | Module 4 | ✅ Confirmed |

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🧰 **[EZ Tools — PECmd](https://ericzimmerman.github.io/)** · 🧭 **[Troubleshooting Pipeline](README.md#troubleshooting-pipeline)**

</div>
