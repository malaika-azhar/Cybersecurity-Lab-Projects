<div align="center">

# 🔐 Project 14 — Windows Event Log Analysis

**Project 14 of 18 — Blue Team Internship Portfolio**

EvtxECmd Parsing · Logon Type Baseline · Failed Logon & Service-Account Noise

![Windows](https://img.shields.io/badge/Windows_Security.evtx-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![EZTools](https://img.shields.io/badge/EvtxECmd-EZ_Tools-2E4053?style=for-the-badge)
![SHA256](https://img.shields.io/badge/SHA256_Verified-217346?style=for-the-badge)
![MITRE](https://img.shields.io/badge/Auth_Baseline-C6501F?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A live Security.evtx log, hashed before parsing and parsed into a structured CSV with EvtxECmd. Ends with a clean human-vs-background-noise authentication baseline.

### [📑 Open the visual index](INDEX.md)

</div>

---

## 📑 Table of Contents

1. [At a Glance](#at-a-glance)
2. [Project Background](#project-background)
3. [Environment](#environment)
4. [Logon Type Reference](#logon-type-reference)
5. [Project Flow](#project-flow)
6. [Module 1 — Evidence Integrity & Parsing](#module-1)
7. [Module 2 — Human Baseline (Logon Type 2)](#module-2)
8. [Module 3 — Failed Logon Tracking](#module-3)
9. [Module 4 — Background Noise (Logon Type 5)](#module-4)
10. [Coverage Snapshot](#coverage-snapshot)
11. [Command Reference](#command-reference)
12. [Project Summary](#project-summary)
13. [Challenges & Fixes](#challenges-fixes)
14. [Scope & Limitations](#scope-limitations)
15. [What I Learned](#what-i-learned)
16. [Skills Demonstrated](#skills-demonstrated)
17. [Screenshot Index](#screenshot-index)
18. [Repo Structure](#repo-structure)

---

<a id="at-a-glance"></a>
## 📊 At a Glance

| 🧩 Parsing Passes | 🖼️ Screenshots | 🎯 Event IDs Analyzed | 📋 Records Parsed | 💰 Cost |
|:---:|:---:|:---:|:---:|:---:|
| **1** | **7** | **2** | **32,738** | **$0** |

---

<a id="project-background"></a>
## 📖 Project Background

All work in this project was performed against my own live, personal Windows machine — not a pre-built evidence file. The goal: extract and analyze the Security.evtx log to build an authentication baseline covering physical logon activity, failed logons, and background service-account noise, using Eric Zimmerman's `EvtxECmd` to parse the raw log into a structured, filterable CSV.

| Task Block | Status | Note |
|---|:---:|---|
| Event Log Analysis (Days 53–55) | ✅ Complete | Human baseline, failed logon, and service-account noise all documented |

---

<a id="environment"></a>
## 🖧 Environment

| Item | Value |
|---|---|
| **Source Log** | `C:\Windows\System32\winevt\Logs\Security.evtx` (live, own machine) |
| **Working Copy** | `C:\Forensics\EventLogs\Security.evtx` |
| **Integrity Hash** | SHA256 `b84b2dc4…36b9463` |
| **Parsing Tool** | EvtxECmd (Eric Zimmerman's EZ Tools) |
| **Output** | `output.csv` — 32,738 records, 0 errors, 0 dropped |
| **Event IDs in Scope** | 4624 (logon), 4625 (failed logon) |

---

<a id="logon-type-reference"></a>
## 🔑 Logon Type Reference

| Type | Meaning | Human Present? |
|:---:|---|:---:|
| **2** | Interactive logon at the physical console (including cold boot) | ✅ Yes |
| **5** | Service logon — background Windows services authenticating for system tasks | ❌ No |
| **7** | Unlock of a previously locked session | ✅ Yes |
| **10** | RemoteInteractive (RDP) logon | ✅ Yes |

Distinguishing these is the foundation of every authentication investigation: Types 2, 7, and 10 represent points where a human was actually present at or connecting to the machine, while Type 5 is background noise that recurs constantly and independently of any user action.

---

<a id="project-flow"></a>
## ⏱️ Project Flow

```mermaid
flowchart LR
    M1["🔵 Module 1<br/>Evidence integrity<br/>and parsing"]:::m1 --> M2["🟠 Module 2<br/>Human baseline<br/>Logon Type 2"]:::m2
    M2 --> M3["🟢 Module 3<br/>Failed logon<br/>Event 4625"]:::m3
    M3 --> M4["🟣 Module 4<br/>Background noise<br/>Logon Type 5"]:::m4
    classDef m1 fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    classDef m2 fill:#B9770E,stroke:#6E4409,stroke-width:2px,color:#FFFFFF
    classDef m3 fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    classDef m4 fill:#76448A,stroke:#432752,stroke-width:2px,color:#FFFFFF
    linkStyle default stroke:#2C3E50,stroke-width:2px
```

---

<a id="module-1"></a>
## 🔵 Module 1 — Evidence Integrity & Parsing

**Objective:** Copy the live Security log under an elevated terminal, hash it immediately for integrity, then parse it into a structured, filterable CSV.

### Step 1 — Copy the log and generate an integrity hash ✅

```
mkdir C:\Forensics\EventLogs
copy C:\Windows\System32\winevt\Logs\Security.evtx C:\Forensics\EventLogs\Security.evtx
certutil -hashfile C:\Forensics\EventLogs\Security.evtx SHA256
```

<p align="center">
  <img src="screenshots/ss-01-certutil-sha256-hash.PNG" alt="Exhibit 1 - SHA256 hash" width="850"><br>
  <em>Exhibit 1 (Figure 53.1) — <code>certutil</code> SHA256 output confirming the integrity hash of the copied Security.evtx file: <code>b84b2dc4…36b9463</code></em>
</p>

### Step 2 — Parse with EvtxECmd ✅

```
.\EvtxECmd.exe -f C:\Forensics\EventLogs\Security.evtx --csv C:\Forensics\EventLogs\ --csvf output.csv
```

<p align="center">
  <img src="screenshots/ss-02-evtxecmd-csv-output-confirm.PNG" alt="Exhibit 2 - EvtxECmd CSV output confirmation" width="850"><br>
  <em>Exhibit 2 (Figure 53.2) — EvtxECmd confirming CSV output will be saved to <code>C:\Forensics\EventLogs\output.csv</code></em>
</p>

<p align="center">
  <img src="screenshots/ss-03-evtxecmd-pass1-completion.PNG" alt="Exhibit 3 - EvtxECmd completion" width="850"><br>
  <em>Exhibit 3 (Figure 53.2b) — EvtxECmd completion log: 32,738 records included, 0 errors, 0 dropped events</em>
</p>

---

<a id="module-2"></a>
## 🟠 Module 2 — Human Baseline (Logon Type 2)

**Objective:** Establish the physical working-hours pattern via Logon Type 2.

### Step 3 — Filter for Logon Type 2 (physical console logon) ✅

<p align="center">
  <img src="screenshots/ss-04-output-csv-filtered-logontype.PNG" alt="Exhibit 4 - Filtered output.csv" width="850"><br>
  <em>Exhibit 4 (Figure 53.3) — Parsed <code>output.csv</code> opened in a spreadsheet, filtered on MapDescription and Logon Type columns ahead of the search</em>
</p>

<p align="center">
  <img src="screenshots/ss-05-logontype2-event-4624.PNG" alt="Exhibit 5 - Logon Type 2 event" width="850"><br>
  <em>Exhibit 5 (Figure 53.4) — First identified Logon Type 2 event: EventId 4624, TimeCreated 7/24/2026 23:27</em>
</p>

---

<a id="module-3"></a>
## 🟢 Module 3 — Failed Logon Tracking

**Objective:** Locate the most recent failed logon.

### Step 4 — Locate Event ID 4625 (failed logon) ✅

<p align="center">
  <img src="screenshots/ss-06-event-4625-failed-logon.PNG" alt="Exhibit 6 - Event 4625 failed logon" width="850"><br>
  <em>Exhibit 6 (Figure 53.5) — Row containing EventId 4625 ("Failed logon"), TimeCreated 9/11/2026 23:23, with the FailureReason2 field referencing the account involved</em>
</p>

---

<a id="module-4"></a>
## 🟣 Module 4 — Background Noise (Logon Type 5)

**Objective:** Identify background service accounts to separate expected Windows noise from genuine human activity.

### Step 5 — Filter Event ID 4624 for Logon Type 5 (service logon) ✅

<p align="center">
  <img src="screenshots/ss-07-logontype5-background-accounts.PNG" alt="Exhibit 7 - Logon Type 5 background accounts" width="850"><br>
  <em>Exhibit 7 (Figure 55.1) — Filtered Logon Type 5 entries showing UserName values including <code>DESKTOP-0O3U1SH$</code> and the local user account, tied to Event ID 5379 (Credential Manager) and related service-context events</em>
</p>

🎯 **Why these shouldn't be flagged as suspicious:** `DESKTOP-0O3U1SH$` is the machine's own computer account, used by Windows itself (Group Policy, domain/workgroup communication) rather than a human user — its recurring Logon Type 5 activity is expected on every Windows machine. The intern's own account appearing in a Type 5 context reflects Credential Manager and related background services operating on behalf of the logged-in session, not a second human logon. An analyst reviewing a compromised server should expect exactly this pattern and focus investigative attention on Logon Types 2, 3, and 10 instead.

---

<a id="coverage-snapshot"></a>
## 🌟 Coverage Snapshot

| 🛡️ Area | ✅ Status | 📌 Detail |
|---|---|---|
| Evidence Integrity | Complete | SHA256 hash generated immediately after copy |
| Human Baseline (Type 2) | Complete | First interactive logon identified with timestamp |
| Failed Logon (4625) | Complete | Most recent instance located with timestamp and failure reason |
| Background Noise (Type 5) | Complete | Multiple service accounts identified and explained |

### 🧾 What the Evidence Proves

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}, 'flowchart': {'nodeSpacing': 24, 'rankSpacing': 34, 'padding': 8}}}%%
flowchart LR
    M1["🔵 Module 1<br/>Integrity"]:::m1 --> P1["✅ Proven<br/>hash + clean parse"]:::ok
    M2["🟠 Module 2<br/>Baseline"]:::m2 --> P2["✅ Proven<br/>Type 2 logon identified"]:::ok
    M3["🟢 Module 3<br/>Failed Logon"]:::m3 --> P3["✅ Proven<br/>4625 located"]:::ok
    M4["🟣 Module 4<br/>Noise"]:::m4 --> P4["✅ Proven<br/>Type 5 accounts explained"]:::ok
    classDef m1 fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    classDef m2 fill:#B9770E,stroke:#6E4409,stroke-width:2px,color:#FFFFFF
    classDef m3 fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    classDef m4 fill:#76448A,stroke:#432752,stroke-width:2px,color:#FFFFFF
    classDef ok fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    linkStyle default stroke:#2C3E50,stroke-width:2px
```

---

<a id="command-reference"></a>
## 🧰 Command Reference

| # | Command | Used In | Purpose |
|:---:|---|---|---|
| 1 | `mkdir C:\Forensics\EventLogs` | Module 1 | Create a dedicated working folder, separate from the live log location |
| 2 | `copy Security.evtx C:\Forensics\EventLogs\` | Module 1 | Copy the live log under an elevated terminal before any parsing |
| 3 | `certutil -hashfile ... SHA256` | Module 1 | Generate an integrity hash immediately after copying |
| 4 | `.\EvtxECmd.exe -f ... --csv ... --csvf output.csv` | Module 1 | Parse the EVTX log into a structured, filterable CSV |

---

<a id="project-summary"></a>
## 📝 Project Summary

| Module | Tooling | Key Outcome |
|---|---|---|
| Module 1 — Evidence Integrity & Parsing | `certutil`, EvtxECmd | 32,738-record CSV produced with a verified SHA256 source hash |
| Module 2 — Human Baseline | Spreadsheet filtering | Logon Type 2 baseline confirmed with timestamp |
| Module 3 — Failed Logon | Spreadsheet filtering, Event ID 4625 | Most recent failed logon located with timestamp |
| Module 4 — Background Noise | Event ID 4624, Logon Type 5 | Multiple service accounts identified and explained as non-suspicious |

---

<a id="challenges-fixes"></a>
## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| Service accounts (Logon Type 5) could be mistaken for suspicious activity | Explained each account's actual role (machine account, Credential Manager) rather than flagging by pattern alone |

---

<a id="scope-limitations"></a>
## 🚧 Scope & Limitations

- **Own personal machine, not a compromised endpoint:** All findings reflect this machine's normal activity — there is no confirmed malicious event in this dataset.
- **Scope:** This project covers Event IDs 4624 and 4625 only.

---

<a id="what-i-learned"></a>
## 🧠 What I Learned

- **Hash first, analyze second.** Hashing the copied log immediately keeps the evidence verifiable for everything that follows.
- **Background noise has to be actively identified, not just ignored.** Explaining what `DESKTOP-0O3U1SH$` and Logon Type 5 actually represent is what lets a real anomaly stand out later.

---

<a id="skills-demonstrated"></a>
## 🛠️ Skills Demonstrated

- Maintaining evidence integrity via SHA256 hashing before any analysis
- Parsing Windows EVTX logs into structured CSV with EvtxECmd (EZ Tools)
- Distinguishing Logon Types 2, 5, 7, and 10 and their investigative significance
- Interpreting Event IDs 4624 and 4625 in context, not just by ID number
- Separating background service-account noise from genuine human activity

---

<a id="screenshot-index"></a>
## 🖼️ Screenshot Index

| # | File | Shows |
|:---:|---|---|
| 1 | `ss-01-certutil-sha256-hash.PNG` | SHA256 integrity hash of the copied Security.evtx |
| 2 | `ss-02-evtxecmd-csv-output-confirm.PNG` | EvtxECmd confirming CSV output path |
| 3 | `ss-03-evtxecmd-pass1-completion.PNG` | Completion: 32,738 records, 0 errors |
| 4 | `ss-04-output-csv-filtered-logontype.PNG` | output.csv filtered on Logon Type columns |
| 5 | `ss-05-logontype2-event-4624.PNG` | First Logon Type 2 event, EventId 4624 |
| 6 | `ss-06-event-4625-failed-logon.PNG` | Event 4625 failed logon row |
| 7 | `ss-07-logontype5-background-accounts.PNG` | Filtered Logon Type 5 background service accounts |

---

<a id="repo-structure"></a>
## 📁 Repo Structure

```text
project-14-windows-event-log-analysis/
|-- README.md
|-- INDEX.md
`-- screenshots/
    |-- ss-01-certutil-sha256-hash.PNG
    |-- ss-02-evtxecmd-csv-output-confirm.PNG
    |-- ss-03-evtxecmd-pass1-completion.PNG
    |-- ss-04-output-csv-filtered-logontype.PNG
    |-- ss-05-logontype2-event-4624.PNG
    |-- ss-06-event-4625-failed-logon.PNG
    `-- ss-07-logontype5-background-accounts.PNG
```

<div align="center">

🪟 **[Windows Security Event IDs](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/basic-audit-logon-events)** · 🧰 **[EZ Tools — EvtxECmd](https://ericzimmerman.github.io/)**

</div>
