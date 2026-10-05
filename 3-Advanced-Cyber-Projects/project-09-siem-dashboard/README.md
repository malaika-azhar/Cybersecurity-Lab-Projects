<div align="center">

# 📊 Custom SOC Dashboard Design

**Project 09 of 18 — Advanced Cyber Projects**

Panel-per-Question Dashboard Engineering (Wazuh)

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005EB8?style=for-the-badge&logo=wazuh&logoColor=white)
![OpenSearch](https://img.shields.io/badge/Dashboards-OpenSearch-005EB8?style=for-the-badge&logo=opensearch&logoColor=white)
![Design Principle](https://img.shields.io/badge/Principle-One_Panel_One_Question-6f42c1?style=for-the-badge)
![Panels](https://img.shields.io/badge/Panels-5-F39C12?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A five-panel SOC dashboard built against five pre-written questions rather than assembled from whatever data happened to be available.

### [📑 Open the visual index](INDEX.md)

</div>

---

## 📑 Table of Contents

1. [At a Glance](#at-a-glance)
2. [Project Background](#project-background)
3. [Environment](#environment)
4. [Project Flow](#project-flow)
5. [Module 1 — Panel Design Against Pre-Written Questions](#module-1)
6. [Coverage Snapshot](#coverage-snapshot)
7. [Dashboard Design Pipeline](#dashboard-pipeline)
8. [Module 2 — Assembled Dashboard](#module-2)
9. [Project Summary](#project-summary)
10. [Challenges & Fixes](#challenges-fixes)
11. [Scope & Limitations](#scope-limitations)
12. [What I Learned](#what-i-learned)
13. [Skills Demonstrated](#skills-demonstrated)
14. [Screenshot Index](#screenshot-index)
15. [Repo Structure](#repo-structure)

---

<a id="at-a-glance"></a>
## 📊 At a Glance

| 🧩 Modules | 🖼️ Screenshots | 📋 Panels | ❓ Questions Answered |
|:---:|:---:|:---:|:---:|
| **2** | **2** | **5** | **5** |

---

<a id="project-background"></a>
## 📖 Project Background

A dashboard assembled by adding every chart that happens to be available produces a wall of color with no clear purpose — a panel with no statable question communicates nothing to whoever reads it later. This project inverts that order: five specific, statable questions were written first, and each panel was built only to answer one of them.

- **Module 1 — Panel Design Against Pre-Written Questions:** Decide what needs to be known before building anything, then map each question to exactly one panel.
- **Module 2 — Assembled Dashboard:** Assemble the final dashboard and record what each panel shows.

> [!NOTE]
> Agent status and rule-firing counts are live, constantly shifting figures. The final assembled dashboard screenshot — captured last — is treated as the single source of truth for every number cited here, not the individual panels built earlier during construction.

<div align="center">

### 🧩 Panel-to-Question Map

<table>
<tr>
<td align="center" valign="top" width="20%">

**❓ How bad<br>was this period?**<br>
<sub><code>panel-severity-7day</code></sub>

</td>
<td align="center" valign="top" width="20%">

**❓ Are all machines<br>reporting?**<br>
<sub><code>panel-agent-status</code></sub>

</td>
<td align="center" valign="top" width="20%">

**❓ What is firing<br>the most?**<br>
<sub><code>panel-top10-rules</code></sub>

</td>
<td align="center" valign="top" width="20%">

**❓ Where is traffic<br>coming from?**<br>
<sub><code>panel-top-source-ips</code></sub>

</td>
<td align="center" valign="top" width="20%">

**❓ What happened<br>over time?**<br>
<sub><code>panel-alert-timeline</code></sub>

</td>
</tr>
</table>

</div>

---

<a id="environment"></a>
## 🖧 Environment

| Item | Value |
|---|---|
| **Dashboard Platform** | Wazuh Dashboard (OpenSearch Dashboards) |
| **Dashboard Name** | `SOC-Week4-Dashboard` |
| **Panel Count** | 5 |
| **Data Sources** | FIM, PAM/sudo audit, Suricata alerts, package manager events |
| **Design Principle** | One panel = one pre-written, statable question |

---

<a id="project-flow"></a>
## ⏱️ Project Flow

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': {
  'activeTaskBkgColor':'#1A5276', 'activeTaskBorderColor':'#0B2E43',
  'doneTaskBkgColor':'#117864', 'doneTaskBorderColor':'#083D33',
  'critBkgColor':'#943126', 'critBorderColor':'#571C16',
  'sectionBkgColor':'#D6DBDF', 'altSectionBkgColor':'#EAECEE',
  'taskTextColor':'#FFFFFF', 'taskTextOutsideColor':'#1B2631',
  'taskTextLightColor':'#FFFFFF',
  'titleColor':'#1B2A4A', 'fontSize':'16px'
}}}%%
gantt
    title Project Flow — Questions to Assembled Dashboard
    dateFormat YYYY-MM-DD
    axisFormat %b %d
    section Panel Design
    Write 5 Questions & Map to 5 Panels     :active, 2026-07-19, 1d
    section Assembly
    Build & Save SOC-Week4-Dashboard        :done, 2026-07-19, 1d
```
<p align="center"><em>Colors distinguish each project stage — all stages complete.</em></p>

---

<a id="module-1"></a>
## 🔵 Module 1 — Panel Design Against Pre-Written Questions

**Objective:** Decide what a SOC analyst or engineer actually needs to know before building a single panel, then map each question to exactly one panel — rather than building panels first and justifying them afterward.

### Step 1 — Write the five questions first ✅

| Question | Panel | What It Shows |
|---|---|---|
| How bad was this period? | `panel-severity-7day` | Alert count by `rule.level`, last 7 days |
| Are all machines reporting? | `panel-agent-status` | Agent health: Active vs. Disconnected |
| What is firing the most? | `panel-top10-rules` | Top rules by alert count |
| Where is traffic coming from? | `panel-top-source-ips` | Top source IP addresses |
| What happened over time? | `panel-alert-timeline` | Alert volume timeline, 3-hour buckets |

### 🔍 Analyst Note — Why the Question Comes Before the Panel

```mermaid
flowchart TD
    A["❓ Write a specific,<br/>statable question"] --> B{"Can it be answered<br/>in one sentence?"}
    B -->|No| C["🚫 Question too vague —<br/>refine before building"]
    B -->|Yes| D["📊 Build exactly one panel<br/>to answer it"]
    D --> E["✅ Panel earns its place<br/>on the dashboard"]
    C -.-> A

    classDef question fill:#e8f1fb,stroke:#005EB8,stroke-width:2px,color:#000
    classDef check fill:#f1ecfb,stroke:#6f42c1,stroke-width:2px,color:#000
    classDef bad fill:#fdeaea,stroke:#C8102E,stroke-width:2px,color:#000
    classDef good fill:#eef7ee,stroke:#2ea44f,stroke-width:2px,color:#000
    class A question
    class B check
    class C bad
    class D,E good
```

A colourful chart with no clear label and no stated time range communicates nothing to whoever reads it later. Every panel in this dashboard was built against a question that could be stated in a single sentence before construction began — not added because the data happened to be available.

---

<a id="coverage-snapshot"></a>
## 🌟 Coverage Snapshot

| 🛡️ Layer | ✅ Status | 📌 Detail |
|---|---|---|
| Panel Design | Question-First | All 5 panels map to a pre-written, statable question |
| Dashboard Assembly | Saved | `SOC-Week4-Dashboard`, all panels live |
| Agent Status Panel | Captured | Panel shows 67 disconnected / 61 active |
| Source of Truth | Assembled Screenshot | Final dashboard capture used over earlier per-panel builds |

---

<a id="dashboard-pipeline"></a>
## 🧭 Dashboard Design Pipeline

From a raw question to a trustworthy, cited number

```mermaid
flowchart TB
    Question["❓ QUESTION WRITTEN FIRST"]:::questionClass
    Map["🗺️ MAPPED TO ONE PANEL"]:::mapClass
    Build["🔨 PANEL BUILT"]:::buildClass
    Assemble["🧩 ASSEMBLED INTO DASHBOARD"]:::assembleClass
    Snapshot["📸 FINAL SCREENSHOT CAPTURED"]:::snapshotClass
    Cite["📝 CITED AS SOURCE OF TRUTH"]:::citeClass

    Question --> Map --> Build --> Assemble --> Snapshot --> Cite

    classDef questionClass fill:#2C3E70,stroke:#131B3A,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef mapClass fill:#1A5276,stroke:#0B2E43,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef buildClass fill:#B9770E,stroke:#6E4409,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef assembleClass fill:#76448A,stroke:#432752,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef snapshotClass fill:#B7950B,stroke:#6B5807,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef citeClass fill:#1E8449,stroke:#0E4A28,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px

    linkStyle default stroke:#2C3E50,stroke-width:4px
```

---

<a id="module-2"></a>
## 🟢 Module 2 — Assembled Dashboard

**Objective:** Assemble all five panels into a single saved dashboard and record what each panel shows.

### Step 2 — Assemble and capture the dashboard ✅

<p align="center">
  <img src="screenshots/Exhibit1_dashboard_agent_status_timeline.png" alt="Exhibit 1 - Dashboard panels 1 of 2" width="850"><br>
  <em>Exhibit 1 — Assembled <code>SOC-Week4-Dashboard</code>, panels 1 of 2: agent status (67 disconnected / 61 active) and alert volume timeline (3-hour buckets) with a burst of high-volume buckets peaking at about 6,500 alerts</em>
</p>

<p align="center">
  <img src="screenshots/Exhibit2_dashboard_severity_sourceips_toprules.png" alt="Exhibit 2 - Dashboard panels 2 of 2" width="850"><br>
  <em>Exhibit 2 — Assembled dashboard, panels 2 of 2: severity-by-level bar chart, top source IPs, and top 10 firing rules (Integrity checksum changed: 9,207; Suricata CUSTOM Nmap NULL Scan Detected: 5,348)</em>
</p>

### Step 3 — Record what each panel shows ✅

The readings below are taken from the two assembled-dashboard screenshots above.

🎯 **Result:** Five panels built, each answering one pre-written question, and saved in one dashboard.

| Panel | Key Reading |
|---|---|
| `panel-agent-status` | 61 active / **67 disconnected** |
| `panel-alert-timeline` | Volume peaks at about 6,500 alerts per 3-hour bucket |
| `panel-severity-7day` | Level 7 has the most alerts, followed by Level 3 |
| `panel-top-source-ips` | Only 6 events carry a source IP: 4 from `192.168.56.1` (the pfSense LAN gateway, per the Week 4 report), 2 from `192.168.56.99` |
| `panel-top10-rules` | Led by Integrity checksum changed (9,207), then Suricata NULL scan (5,348) |

---

<a id="project-summary"></a>
## 📝 Project Summary

| Module | Tooling | Key Result |
|---|---|---|
| Panel Design Against Pre-Written Questions | Wazuh Dashboard, OpenSearch visualizations | 5 questions, each mapped to exactly one panel before building began |
| Assembled Dashboard | `SOC-Week4-Dashboard` | Five panels saved in one dashboard; readings captured in two screenshots |

---

<a id="challenges-fixes"></a>
## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| Agent status and rule-firing counts shifted between when individual panels were first built and when the full dashboard was assembled | Standardised on the final assembled screenshot as the single source of truth for every number cited, rather than an earlier, already-stale per-panel capture |

---

<a id="scope-limitations"></a>
## 🚧 Scope & Limitations

- **Snapshot in time:** All figures reflect the state at the moment the dashboard was assembled and captured — agent counts and rule totals are live and will have moved on since.
- **What the agent counts measure was not checked:** The agent status panel is quoted as displayed (67 disconnected, 61 active). Whether it counts distinct agents or status records was not verified.
- **Five panels only:** This dashboard answers five specific questions; it is not a general-purpose, exhaustive SOC view.

---

<a id="what-i-learned"></a>
## 🧠 What I Learned

- **A panel with no statable question doesn't belong on the dashboard.** Writing the question before building anything kept every panel purposeful rather than decorative.
- **Dashboard numbers are a snapshot, not a constant.** Citing the earliest per-panel screenshot instead of the final assembled view risks reporting a number that was already stale by the time it's written down.

---

<a id="skills-demonstrated"></a>
## 🛠️ Skills Demonstrated

- Designing dashboard panels against explicit, pre-written questions rather than available data
- Building and saving a multi-panel SOC dashboard in OpenSearch Dashboards
- Treating live, shifting figures correctly by citing a single authoritative snapshot

---

<a id="screenshot-index"></a>
## 🖼️ Screenshot Index

| # | File | Shows |
|:---:|---|---|
| 1 | `Exhibit1_dashboard_agent_status_timeline.png` | Agent status panel and alert volume timeline |
| 2 | `Exhibit2_dashboard_severity_sourceips_toprules.png` | Severity bar chart, top source IPs, top 10 firing rules |

---

<a id="repo-structure"></a>
## 📁 Repo Structure

```text
project-09-siem-dashboard/
|-- README.md
|-- INDEX.md
`-- screenshots/
    |-- Exhibit1_dashboard_agent_status_timeline.png
    `-- Exhibit2_dashboard_severity_sourceips_toprules.png
```

<div align="center">

📊 **[Wazuh](https://wazuh.com)** · 🔍 **[OpenSearch Dashboards](https://opensearch.org/docs/latest/dashboards/)** · 🧭 **[Dashboard Pipeline](#dashboard-pipeline)**

</div>
