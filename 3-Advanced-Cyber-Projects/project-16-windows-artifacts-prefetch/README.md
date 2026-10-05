<div align="center">

# 🗂️ Windows Artifacts — Prefetch & Thumbcache

**Project 16 of 18 — Blue Team Internship Portfolio**

PECmd Execution Profiling · Context-Based Suspicion Review · Locked-File Recovery

![Windows](https://img.shields.io/badge/Windows_Prefetch-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![EZTools](https://img.shields.io/badge/PECmd-EZ_Tools-2E4053?style=for-the-badge)
![Robocopy](https://img.shields.io/badge/Robocopy_%2FB-8E44AD?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

363 Prefetch files parsed to profile every program that ran on a live machine — including one Temp-path execution that looked suspicious by the textbook rule, until context (a confirmed legitimate install) closed it correctly instead of flagging it. A locked thumbcache database recovered with a backup-mode copy rounds out the artefact set.

### [📑 Open the visual index](INDEX.md)

</div>

---

## 📑 Table of Contents

1. [At a Glance](#at-a-glance)
2. [Project Background](#project-background)
3. [Environment](#environment)
4. [Project Flow](#project-flow)
5. [Module 1 — Prefetch Extraction & Parsing](#module-1)
6. [Module 2 — Execution Profiling](#module-2)
7. [Module 3 — Contextual Investigation: the Temp-Path Installer](#module-3)
8. [Module 4 — Thumbcache Recovery](#module-4)
9. [Coverage Snapshot](#coverage-snapshot)
10. [Troubleshooting Pipeline](#troubleshooting-pipeline)
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

| 🧩 .pf Files Parsed | 🖼️ Screenshots | 💰 Cost |
|:---:|:---:|:---:|
| **362 / 363** | **7** | **$0** |

---

<a id="project-background"></a>
## 📖 Project Background

All artefacts here were extracted live from my own personal Windows machine, continuing directly from the event-log baseline in [Project 14](../project-14-windows-event-log-analysis). This project covers program-execution history (Prefetch) and the thumbnail cache — two artefact categories that each persist independently of the files or sessions that generated them.

| Task Block | Status | Note |
|---|:---:|---|
| Prefetch Analysis (Days 56–57) | ✅ Complete | 363 files copied, 362 parsed, top-20 profiled, one Temp-path execution investigated and explained |
| Thumbcache (Day 58) | ✅ Complete | `thumbcache_1280.db` recovered with `robocopy /B` |

---

<a id="environment"></a>
## 🖧 Environment

| Item | Value |
|---|---|
| **Prefetch Source** | `C:\Windows\Prefetch` → copied to `C:\Forensics\Prefetch` |
| **Parsing Tool** | PECmd (Eric Zimmerman's EZ Tools) |
| **Files Copied** | 363 `.pf` files |
| **Files Parsed** | 362 of 363 (1 corrupted — `SYNTPHELPER.EXE`, invalid signature) |
| **Parse Time** | 87.26 seconds |
| **Thumbcache DB Recovered** | `thumbcache_1280.db` (2,097,152 bytes) via `robocopy /B` |

---

<a id="project-flow"></a>
## ⏱️ Project Flow

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': {
  'doneTaskBkgColor':'#117864', 'doneTaskBorderColor':'#083D33',
  'sectionBkgColor':'#D6DBDF', 'altSectionBkgColor':'#EAECEE',
  'taskTextColor':'#FFFFFF', 'taskTextOutsideColor':'#1B2631',
  'taskTextLightColor':'#FFFFFF',
  'titleColor':'#1B2A4A', 'fontSize':'18px'
}}}%%
gantt
    title Project Flow — Four Modules
    dateFormat YYYY-MM-DD
    axisFormat %b %d
    section Prefetch
    Module 1 - Prefetch extraction and parsing        :done, 2026-01-01, 1d
    Module 2 - Execution profiling, Top 20 and paths   :done, 2026-01-01, 1d
    Module 3 - Contextual investigation, Temp installer :done, 2026-01-02, 1d
    section Thumbcache
    Module 4 - Thumbcache recovery                     :done, 2026-01-02, 1d
```

---

<a id="module-1"></a>
## 🔵 Module 1 — Prefetch Extraction & Parsing

**Objective:** Copy the live Prefetch directory to a working folder before any parsing, per the task brief's warning against working directly from the live directory, then parse it into a structured CSV.

### Step 1 — Copy the Prefetch directory ✅

```
mkdir C:\Forensics\Prefetch
xcopy C:\Windows\Prefetch C:\Forensics\Prefetch /E /H /C /I
(dir C:\Forensics\Prefetch\*.pf).Count
```

<p align="center">
  <img src="screenshots/ss-01-prefetch-copy-confirmation-363files.PNG" alt="Exhibit 1 - Prefetch copy confirmation" width="850"><br>
  <em>Exhibit 1 (Figure 56.1) — Confirmed count of 363 <code>.pf</code> files successfully copied to the working directory</em>
</p>

### Step 2 — Parse with PECmd ✅

```
.\PECmd.exe -d C:\Forensics\Prefetch --csv C:\Forensics\Prefetch\ --csvf prefetch_output.csv
```

<p align="center">
  <img src="screenshots/ss-02-pecmd-parsing-completion.PNG" alt="Exhibit 2 - PECmd parsing completion" width="850"><br>
  <em>Exhibit 2 (Figure 56.2) — PECmd completion output: 362 of 363 files processed successfully in 87.26 seconds; <code>SYNTPHELPER.EXE</code> failed with an invalid-signature error, consistent with a corrupted or non-standard prefetch entry rather than a parsing fault</em>
</p>

---

<a id="module-2"></a>
## 🟠 Module 2 — Execution Profiling

**Objective:** Sort by run count to identify the most-executed programs, then check every top entry's execution path for anything outside a standard location.

### Step 3 — Build the Top 20 Most-Executed Programs table ✅

The seven most-executed entries of the sorted table:

| Executable | Run Count | Last Run | Analyst Note |
|---|:---:|---|---|
| CHROME.EXE | 1,225 | 9/12/2026 7:50 | Expected — primary browser |
| CHROME.EXE | 1,121 | 9/12/2026 7:56 | Expected — secondary Chrome process path |
| CHROME.EXE | 703 | 9/12/2026 7:57 | Expected — browser helper/renderer path |
| SEARCHFILTERHOST.EXE | 557 | 9/12/2026 6:49 | Expected — Windows Search indexing |
| SVCHOST.EXE | 448 | 9/12/2026 7:55 | Expected — Windows service host |
| SVCHOST.EXE | 425 | 9/12/2026 1:05 | Expected — Windows service host |
| CONHOST.EXE | 338 | 9/12/2026 7:58 | Expected — console host |

<p align="center">
  <img src="screenshots/ss-03-top20-runcount-table.PNG" alt="Exhibit 3 - Top 20 RunCount table" width="850"><br>
  <em>Exhibit 3 (Figure 56.3) — RunCount-sorted table of the most-executed programs</em>
</p>

### Step 4 — Check execution paths for suspicious locations ✅

Among the top 20 highest-run-count entries, all execution paths resolved to standard, expected locations: `WINDOWS\SYSTEM32`, `PROGRAM FILES\GOOGLE`, `PROGRAMDATA\MICROSOFT`, and `PROGRAM FILES (X86)\IOBIT` (a legitimately installed third-party utility). No Temp or Downloads execution was found among the highest-frequency entries.

<p align="center">
  <img src="screenshots/ss-04-directories-column-reference.PNG" alt="Exhibit 4 - Directories column reference" width="850"><br>
  <em>Exhibit 4 (Figure 56.4) — Full Directories column extracted for the top-run entries, used as the working reference for the standard-path check</em>
</p>

<p align="center">
  <img src="screenshots/ss-05-directories-widened-temp-check.PNG" alt="Exhibit 5 - Widened directories, TEMP check" width="850"><br>
  <em>Exhibit 5 (Figure 56.5) — Widened Directories column for the top-run-count entries, all showing standard locations</em>
</p>

---

<a id="module-3"></a>
## 🟢 Module 3 — Contextual Investigation: the Temp-Path Installer

**Objective:** When a genuine Temp-path execution does appear — just not in the top 20 — investigate it in context rather than either ignoring it or flagging it automatically.

### Step 5 — Review the full execution timeline for Temp-path activity ✅

A separate review of the PECmd-generated timeline (`prefetch_output_Timeline.csv`, distinct from the top-20 table) identified two entries executing from `\USERS\<USER>\APPDATA\LOCAL\TEMP\IS-TJ7CF.TMP\` and `\IS-0278P.TMP\`, both tied to `ADVANCED-SYSTEMCARE-SETUP.TMP`.

<p align="center">
  <img src="screenshots/ss-06-installer-temppath-timeline.PNG" alt="Exhibit 6 - Installer Temp-path timeline" width="850"><br>
  <em>Exhibit 6 (Figure 56.6) — Timeline rows showing <code>ADVANCED-SYSTEMCARE-SETUP.TMP</code> executing from two AppData\Local\Temp installer extraction subfolders</em>
</p>

🎯 **Finding — investigated, not flagged:** The filename and path pattern (an InstallShield-style `.TMP` extraction folder) are consistent with expected installer self-extraction behavior, and this conclusion is corroborated by the same software (IObit Advanced SystemCare) already installed under `C:\Program Files (x86)\IOBIT\` — confirmed directly in Module 2's standard-path check. This is a worked example of correctly assessing execution-path suspicion in context, rather than flagging every Temp-path hit uniformly.

---

<a id="module-4"></a>
## 🟣 Module 4 — Thumbcache Recovery

**Objective:** Recover the thumbnail cache database from a live system, where Explorer holds the file open.

### Step 6 — Bypass the Explorer lock on the thumbcache database ✅

Thumbcache database files are held open by a live-running Windows Explorer, preventing a normal file copy. A `robocopy` operation using backup mode (`/B`) was used to bypass the lock.

```
mkdir C:\Forensics\Thumbcache
robocopy "C:\Users\<user>\AppData\Local\Microsoft\Windows\Explorer" C:\Forensics\Thumbcache thumbcache_*.db /B
```

<p align="center">
  <img src="screenshots/ss-07-thumbcache-robocopy-confirmation.PNG" alt="Exhibit 7 - Thumbcache robocopy confirmation" width="850"><br>
  <em>Exhibit 7 (Figure 58.1) — Directory listing confirming <code>thumbcache_1280.db</code> (2,097,152 bytes) is in the working directory after <code>robocopy /B</code></em>
</p>

`thumbcache_1280.db` was copied to the working directory; a second database (`thumbcache_16.db`) remained locked and was not copied.

---

<a id="coverage-snapshot"></a>
## 🌟 Coverage Snapshot

| 🛡️ Artefact | ✅ Status | 📌 Detail |
|---|---|---|
| Prefetch Copy & Parse | Complete | 363 copied, 362 parsed (1 corrupted, explained) |
| Execution Profiling | Complete | Top 20 all resolve to standard paths |
| Temp-Path Investigation | Complete | Investigated and correctly closed as expected installer behavior |
| Thumbcache | Complete | `thumbcache_1280.db` recovered despite the Explorer lock |

### 🧾 What the Evidence Proves

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}, 'flowchart': {'nodeSpacing': 24, 'rankSpacing': 34, 'padding': 8}}}%%
flowchart LR
    M1["🔵 Module 1<br/>Extraction"]:::m1 --> P1["✅ Proven<br/>362/363 files parsed cleanly"]:::ok
    M2["🟠 Module 2<br/>Profiling"]:::m2 --> P2["✅ Proven<br/>top-20 all standard paths"]:::ok
    M3["🟢 Module 3<br/>Context Check"]:::m3 --> P3["✅ Proven<br/>Temp hit correctly explained"]:::ok
    M4["🟣 Module 4<br/>Thumbcache"]:::m4 --> P4["✅ Proven<br/>thumbcache_1280.db recovered"]:::ok
    classDef m1 fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    classDef m2 fill:#B9770E,stroke:#6E4409,stroke-width:2px,color:#FFFFFF
    classDef m3 fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    classDef m4 fill:#76448A,stroke:#432752,stroke-width:2px,color:#FFFFFF
    classDef ok fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    linkStyle default stroke:#2C3E50,stroke-width:2px
```

---

<a id="troubleshooting-pipeline"></a>
## 🧭 Troubleshooting Pipeline

How a textbook "suspicious path" gets correctly closed instead of falsely flagged

```mermaid
flowchart TB
    Find["🔎 FIND AN EXECUTION FROM TEMP/DOWNLOADS"]:::findClass
    Rule["📖 MATCHES THE TEXTBOOK 'SUSPICIOUS PATH' RULE"]:::ruleClass
    Context["🧩 CHECK FOR CORROBORATING CONTEXT"]:::contextClass
    Installed["❓ IS THE SAME SOFTWARE CONFIRMED INSTALLED ELSEWHERE?"]:::qClass
    Close["✅ CLOSE AS EXPECTED BEHAVIOR"]:::closeClass
    Flag["🚨 ESCALATE AS GENUINE CONCERN"]:::flagClass

    Find --> Rule --> Context --> Installed
    Installed -->|YES, standard path| Close
    Installed -->|NO corroboration| Flag

    classDef findClass fill:#2C3E70,stroke:#131B3A,stroke-width:4px,color:#FFFFFF,font-weight:bold
    classDef ruleClass fill:#B7950B,stroke:#6B5807,stroke-width:4px,color:#FFFFFF,font-weight:bold
    classDef contextClass fill:#1A5276,stroke:#0B2E43,stroke-width:4px,color:#FFFFFF,font-weight:bold
    classDef qClass fill:#76448A,stroke:#432752,stroke-width:4px,color:#FFFFFF,font-weight:bold
    classDef closeClass fill:#1E8449,stroke:#0E4A28,stroke-width:4px,color:#FFFFFF,font-weight:bold
    classDef flagClass fill:#943126,stroke:#571C16,stroke-width:4px,color:#FFFFFF,font-weight:bold

    linkStyle default stroke:#2C3E50,stroke-width:3px
```

---

<a id="command-reference"></a>
## 🧰 Command Reference

| # | Command | Used In | Purpose |
|:---:|---|---|---|
| 1 | `xcopy C:\Windows\Prefetch ... /E /H /C /I` | Module 1 | Copy the live Prefetch directory before parsing |
| 2 | `.\PECmd.exe -d ... --csv ...` | Module 1 | Parse `.pf` files into a structured CSV |
| 3 | `robocopy ... thumbcache_*.db /B` | Module 4 | Bypass Explorer's file lock on the thumbcache database using backup mode |

---

<a id="project-summary"></a>
## 📝 Project Summary

| Module | Tooling | Key Outcome |
|---|---|---|
| Module 1 — Prefetch Extraction | `xcopy`, PECmd | 362 of 363 `.pf` files parsed cleanly; 1 corrupted file explained |
| Module 2 — Execution Profiling | RunCount sort, Directories column | Top 20 programs all confirmed executing from standard paths |
| Module 3 — Contextual Investigation | Timeline export cross-reference | Temp-path installer execution investigated and correctly closed, not flagged |
| Module 4 — Thumbcache Recovery | Robocopy `/B` | `thumbcache_1280.db` recovered from under an Explorer lock |

---

<a id="challenges-fixes"></a>
## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| One `.pf` file (`SYNTPHELPER.EXE`) failed to parse with an invalid-signature error | Documented as a corrupted/non-standard prefetch entry rather than a parsing failure, and excluded from the 362-file analysis set |
| A Temp-path installer execution matched the textbook "suspicious location" pattern | Cross-referenced against the same software's confirmed legitimate install path before closing it as expected behavior |
| Thumbcache database files locked by a live Explorer process | Used `robocopy /B` (backup mode) to bypass the lock rather than skipping the artefact |
| A second thumbcache file (`thumbcache_16.db`) remained locked | Not copied; the first database was already recovered |

---

<a id="scope-limitations"></a>
## 🚧 Scope & Limitations

- **Own personal machine, non-incident baseline:** No confirmed compromise indicator exists in this dataset.
- **Personal content withheld:** The Windows username and the drive serial number are redacted where legible, per the privacy handling standard set in the task brief.
- **One corrupted prefetch file:** `SYNTPHELPER.EXE` could not be parsed (1 of 363) and is excluded from the execution-profile analysis.
- **Second thumbcache database not recovered:** `thumbcache_16.db` remained locked and was not copied.

---

<a id="what-i-learned"></a>
## 🧠 What I Learned

- **A suspicious-path rule is a starting point, not a verdict.** The Advanced SystemCare Temp execution matched the textbook definition of suspicious, but corroborating it against the same software's confirmed install path turned a potential false positive into a correctly closed finding.
- **A locked file needs a documented workaround, not a skipped step.** `robocopy /B` bypassing Explorer's lock is only useful if the method itself is recorded — so another analyst could replicate it exactly.

---

<a id="skills-demonstrated"></a>
## 🛠️ Skills Demonstrated

- Parsing Windows Prefetch (`.pf`) files with PECmd (EZ Tools) to build an execution profile
- Distinguishing standard execution paths from genuinely suspicious ones using corroborating context
- Bypassing a locked live file (thumbcache database) with a documented, replicable workaround
- Applying a privacy-redaction standard to usernames and drive identifiers in screenshots

---

<a id="screenshot-index"></a>
## 🖼️ Screenshot Index

| # | File | Shows |
|:---:|---|---|
| 1 | `ss-01-prefetch-copy-confirmation-363files.PNG` | 363 `.pf` files copied to the working directory |
| 2 | `ss-02-pecmd-parsing-completion.PNG` | PECmd: 362/363 parsed successfully, 87.26 seconds |
| 3 | `ss-03-top20-runcount-table.PNG` | Top 20 RunCount-sorted programs table |
| 4 | `ss-04-directories-column-reference.PNG` | Full Directories column for top-run entries |
| 5 | `ss-05-directories-widened-temp-check.PNG` | Widened Directories column for the top-run entries |
| 6 | `ss-06-installer-temppath-timeline.PNG` | Advanced SystemCare Temp-path installer timeline rows |
| 7 | `ss-07-thumbcache-robocopy-confirmation.PNG` | Directory listing of `thumbcache_1280.db` (2,097,152 bytes) after `robocopy /B` |

---

<a id="repo-structure"></a>
## 📁 Repo Structure

```text
project-16-windows-artifacts-prefetch/
|-- README.md
|-- INDEX.md
`-- screenshots/
    |-- ss-01-prefetch-copy-confirmation-363files.PNG
    |-- ss-02-pecmd-parsing-completion.PNG
    |-- ss-03-top20-runcount-table.PNG
    |-- ss-04-directories-column-reference.PNG
    |-- ss-05-directories-widened-temp-check.PNG
    |-- ss-06-installer-temppath-timeline.PNG
    `-- ss-07-thumbcache-robocopy-confirmation.PNG
```

<div align="center">

🧰 **[EZ Tools — PECmd](https://ericzimmerman.github.io/)** · 🪟 **[Windows Prefetch](https://learn.microsoft.com/en-us/windows/win32/w8cookbook/-order-prelaunch-optimization)** · 🧭 **[Troubleshooting Pipeline](#troubleshooting-pipeline)**

</div>
