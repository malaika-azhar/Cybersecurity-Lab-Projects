<a id="top"></a>
<div align="center">

# 🔍 Project 03 — Index
### Automated Port & Service Scanner
**Project 03 of 10 — Foundational Projects**

![Python](https://img.shields.io/badge/Python_3.14-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-D9782D?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🐛 Errors Fixed | 🎯 Final Result |
|:---:|:---:|:---:|:---:|
| **7** | **6** | **3** | **Clean scan** |

</div>

<p align="center">🧩 <b>Lab:</b> Python + <code>python-nmap</code> wrapping Nmap · target <code>127.0.0.1</code></p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Install Python & python-nmap | 🔵 Module 1 | Python + library installed | [Exhibit 1](#ex1) |
| 2 | Write scanner.py | 🔵 Module 2 | Initial script saved | [Exhibit 2](#ex2) |
| 3 | Diagnose hidden file extension | 🔴 Module 3 | Found `scanner.py.txt`, renamed | [Exhibit 3](#ex3) |
| 4 | Install Nmap & refresh PATH | 🔴 Module 4 | Fixed install + stale CMD session | 📝 No screenshot |
| 5 | Diagnose invalid scan flag | 🔴 Module 5 | XML parse error traced to `-xyz` | [Exhibit 5](#ex5) |
| 6 | Configure the scan call | 🟠 Module 6 | `-sV -Pn --unprivileged` applied | — |
| 7 | Verify clean scan | 🟢 Module 7 | Host up, no errors | [Exhibit 7](#ex7) |

---

## 🔵 Module 1–2 — Setup

Exhibits 1 to 2.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/1_Python_Installation.PNG"><img src="screenshots/1_Python_Installation.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Python installed</b>
<br><sub>Python + <code>python-nmap</code> installed successfully</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/2_Scanner_Code.PNG"><img src="screenshots/2_Scanner_Code.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — scanner.py written</b>
<br><sub>Initial script version in Notepad</sub>
</td>
</tr>
</table>

---

## 🔴 Module 3 — Hidden Extension Error

Exhibits 3 (and its fix, same file group).

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/3_Extension_Error_Check.PNG"><img src="screenshots/3_Extension_Error_Check.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Hidden extension found</b>
<br><sub><code>dir</code> reveals <code>scanner.py.txt</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a href="screenshots/4_File_Renamed_Fix.PNG"><img src="screenshots/4_File_Renamed_Fix.PNG" width="380" alt="Exhibit 3 fix"></a>
<br><b>Exhibit 3 (fix) — Renamed</b>
<br><sub><code>ren scanner.py.txt scanner.py</code></sub>
</td>
</tr>
</table>

---

## 🔴 Module 4–5 — Install & Flag Errors

Exhibit 5 (Module 4 has no screenshot — documented from memory).

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/5_Nmap_Path_Error.PNG"><img src="screenshots/5_Nmap_Path_Error.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Invalid flag error</b>
<br><sub><code>xml.etree.ElementTree.ParseError</code> from <code>-xyz</code></sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 6–7 — Fix & Verify

Exhibit 7.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/6_Final_Scan_Success.PNG"><img src="screenshots/6_Final_Scan_Success.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Clean scan</b>
<br><sub>Host up, no errors, service-version detection enabled</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Real filename confirmed | `dir` | Module 3 | ✅ Confirmed |
| Nmap install + fresh CMD session | Reinstall, new terminal | Module 4 | ✅ Confirmed (no screenshot) |
| Invalid flag traced | XML parse error | Module 5 | ✅ Confirmed |
| Corrected scan flags | `-sV -Pn --unprivileged` | Module 6 | ✅ Confirmed |
| Clean scan on localhost | `python scanner.py` | Module 7 | ✅ Confirmed |

> [!NOTE]
> No screenshot exists for the Nmap-not-installed error (Module 4) — it occurred during an earlier run and was resolved before the lab was redone. Documented from memory, not hidden.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🔍 **[Nmap Documentation](https://nmap.org/book/man.html)** · 🐍 **[python-nmap on PyPI](https://pypi.org/project/python-nmap/)**

</div>
