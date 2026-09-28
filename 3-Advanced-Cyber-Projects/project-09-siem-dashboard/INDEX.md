<a id="top"></a>
<div align="center">

# 📊 Project 12 — Index
### Custom SOC Dashboard Design
**Project 12 of 29 — Advanced Cyber Projects**

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005EB8?style=for-the-badge&logo=wazuh&logoColor=white)
![OpenSearch](https://img.shields.io/badge/Dashboards-OpenSearch-005EB8?style=for-the-badge&logo=opensearch&logoColor=white)
![Design Principle](https://img.shields.io/badge/Principle-One_Panel_One_Question-6f42c1?style=for-the-badge)
![Panels](https://img.shields.io/badge/Panels-5-F39C12?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every panel and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 📋 Panels | ❓ Questions Answered |
|:---:|:---:|:---:|:---:|
| **2** | **2** | **5** | **5** |

</div>

<p align="center">🧩 <b>Lab:</b> 5 pre-written questions ➜ 5 mapped panels ➜ <code>SOC-Week4-Dashboard</code> assembled in Wazuh / OpenSearch Dashboards</p>

---

## 📑 Step Index

Both steps of the project, with the screenshot that proves each one.

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Write 5 questions, map each to one panel | 🔵 Module 1 | Panel-per-question design table (see README) | Table (see README) |
| 2 | Assemble and capture the final dashboard | 🟢 Module 2 | 5 panels live, 1 finding flagged for follow-up | [Exhibit 1](#ex1) · [Exhibit 2](#ex2) |

---

## 🔵 Module 1 — Panel-to-Question Map

<div align="center">
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

## 🟢 Module 2 — Assembled Dashboard

Exhibits 1 to 2. Click a screenshot to open it full size.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/Exhibit1_dashboard_agent_status_timeline.png"><img src="screenshots/Exhibit1_dashboard_agent_status_timeline.png" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Agent status & timeline</b>
<br><sub>67 disconnected / 61 active, plus alert volume over time with two clear spikes</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/Exhibit2_dashboard_severity_sourceips_toprules.png"><img src="screenshots/Exhibit2_dashboard_severity_sourceips_toprules.png" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Severity, source IPs, top rules</b>
<br><sub>Led by Integrity checksum changed (9,207) and Suricata NULL scan (5,348)</sub>
</td>
</tr>
</table>

---

## 🎯 Key Findings Summary

| Panel | Key Reading | Status |
|---|---|:---:|
| Agent Status | 61 active / **67 disconnected** | 🚩 Flagged for follow-up |
| Alert Timeline | Two clear volume spikes | ✅ Matches testing windows |
| Severity (7-day) | Majority at Level 7 | ✅ As expected |
| Top Source IPs | Concentrated on 2 internal IPs | ✅ Documented |
| Top 10 Rules | FIM checksum changes lead | ✅ Documented |

> [!NOTE]
> The disconnected-agent count is surfaced here deliberately, not filtered out — a dashboard that only shows good news isn't a monitoring tool.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

📊 **[Wazuh](https://wazuh.com)** · 🔍 **[OpenSearch Dashboards](https://opensearch.org/docs/latest/dashboards/)** · 🧭 **[Dashboard Pipeline](README.md#dashboard-pipeline)**

</div>
