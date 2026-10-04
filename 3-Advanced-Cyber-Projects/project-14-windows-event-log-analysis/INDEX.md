<a id="top"></a>
<div align="center">

# 🔐 Project 14 — Index
### Windows Event Log Analysis
**Project 14 of 18 — Blue Team Internship Portfolio**

![Windows](https://img.shields.io/badge/Windows_Security.evtx-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![EZTools](https://img.shields.io/badge/EvtxECmd-EZ_Tools-2E4053?style=for-the-badge)
![SHA256](https://img.shields.io/badge/SHA256_Verified-217346?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Parsing Passes | 🖼️ Screenshots | 🎯 Event IDs | 📋 Records (Pass 2) |
|:---:|:---:|:---:|:---:|
| **2** | **8** | **3** | **33,127** |

</div>

<p align="center">🧩 <b>Source:</b> Live Security.evtx (own machine) ➜ EvtxECmd ➜ Logon Type baseline</p>

---

## 📑 Step Index

All 8 steps of the project, with the screenshot that shows each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Copy the log and hash it | 🔵 Module 1 | SHA256 `b84b2dc4…36b9463` | [Exhibit 1](#ex1) |
| 2 | Parse with EvtxECmd (Pass 1) | 🔵 Module 1 | CSV output path confirmed | [Exhibit 2](#ex2) |
| 3 | Confirm Pass 1 completion | 🔵 Module 1 | 32,738 records, 0 errors | [Exhibit 3](#ex3) |
| 4 | Filter for Logon Type 2 | 🟠 Module 2 | output.csv filtered on Logon Type | [Exhibit 4](#ex4) |
| 5 | Identify the Type 2 baseline event | 🟠 Module 2 | EventId 4624, 7/24/2026 23:27 | [Exhibit 5](#ex5) |
| 6 | Re-parse after lock/unlock test | 🟠 Module 2 | Pass 2: 33,127 records — still no Type 7 found | [Exhibit 6](#ex6) |
| 7 | Locate Event 4625 (failed logon) | 🟢 Module 3 | TimeCreated 9/11/2026 23:23 | [Exhibit 7](#ex7) |
| 8 | Filter for Logon Type 5 (service noise) | 🟣 Module 4 | `DESKTOP-0O3U1SH$` + local account identified | [Exhibit 8](#ex8) |

---

## 🔵 Module 1 — Evidence Integrity & Parsing

Exhibits 1 to 3. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/ss-01-certutil-sha256-hash.PNG"><img src="screenshots/ss-01-certutil-sha256-hash.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — SHA256 hash</b>
<br><sub>Integrity hash of the copied Security.evtx</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/ss-02-evtxecmd-csv-output-confirm.PNG"><img src="screenshots/ss-02-evtxecmd-csv-output-confirm.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — CSV output confirmed</b>
<br><sub>EvtxECmd output path confirmation</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/ss-03-evtxecmd-pass1-completion.PNG"><img src="screenshots/ss-03-evtxecmd-pass1-completion.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Pass 1 completion</b>
<br><sub>32,738 records, 0 errors, 0 dropped</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠 Module 2 — Human Baseline & the Logon Type 7 Finding

Exhibits 4 to 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/ss-04-output-csv-filtered-logontype.PNG"><img src="screenshots/ss-04-output-csv-filtered-logontype.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Filtered output.csv</b>
<br><sub>MapDescription and Logon Type columns</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/ss-05-logontype2-event-4624.PNG"><img src="screenshots/ss-05-logontype2-event-4624.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Logon Type 2 event</b>
<br><sub>EventId 4624, 7/24/2026 23:27</sub>
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/ss-06-evtxecmd-pass2-completion.PNG"><img src="screenshots/ss-06-evtxecmd-pass2-completion.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Pass 2 completion</b>
<br><sub>33,127 records, post lock/unlock test</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 3 — Failed Logon & Privilege Tracking

Exhibit 7.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/ss-07-event-4625-failed-logon.PNG"><img src="screenshots/ss-07-event-4625-failed-logon.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Event 4625</b>
<br><sub>Failed logon, TimeCreated 9/11/2026 23:23</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟣 Module 4 — Background Noise (Logon Type 5)

Exhibit 8.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/ss-08-logontype5-background-accounts.PNG"><img src="screenshots/ss-08-logontype5-background-accounts.PNG" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Logon Type 5 accounts</b>
<br><sub><code>DESKTOP-0O3U1SH$</code> and local account, service context</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Source log integrity hashed before analysis | `certutil` SHA256 | Module 1 | ✅ Confirmed |
| Log parsed cleanly | EvtxECmd, 0 errors | Module 1 | ✅ Confirmed |
| Logon Type 2 baseline identified | Spreadsheet filter | Module 2 | ✅ Confirmed |
| Logon Type 7 event found | Deliberate lock/unlock test, re-parse | Module 2 | ❌ Not found — documented as a finding |
| Event 4625 (failed logon) located | Spreadsheet filter | Module 3 | ✅ Confirmed |
| Event 4672 correctly attributed to SYSTEM startup | Timestamp clustering | Module 3 | ✅ Confirmed |
| Logon Type 5 background accounts explained | Spreadsheet filter | Module 4 | ✅ Confirmed |

> [!NOTE]
> The Logon Type 7 absence is reported exactly as observed, even after a deliberate test designed to produce one — this is treated as an open investigative item, not a resolved result.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🪟 **[Windows Security Event IDs](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/basic-audit-logon-events)** · 🧰 **[EZ Tools](https://ericzimmerman.github.io/)** · 🧭 **[Troubleshooting Pipeline](README.md#troubleshooting-pipeline)**

</div>
