<a id="top"></a>
<div align="center">

# 🚨 Project 06 — Index
### SIEM Alert Triage — SOC Simulator
**Project 06 of 10 — Foundational Projects**

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![TryHackMe](https://img.shields.io/badge/TryHackMe-212C42?style=for-the-badge&logo=tryhackme&logoColor=white)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🎫 Alerts Triaged | ⚖️ Verdicts |
|:---:|:---:|:---:|:---:|
| **9** | **12** | **2** | **1 FP · 1 TP** |

</div>

<p align="center">🧩 <b>Lab:</b> TryHackMe SOC Simulator · Splunk · Scenario 1 (Phishing)</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Open the simulator | 🔵 Module 1 | Scenario 1 loaded | [Exhibit 1](#ex1) |
| 2 | Review the alert queue | 🔵 Module 2 | Alert 8818 picked up | [Exhibit 2](#ex2) |
| 3 | Assign the alert | 🟠 Module 3 | Assigned to self | [Exhibit 3](#ex3) |
| 4 | Review alert details | 🟠 Module 4 | Raw email data read | [Exhibit 4](#ex4) |
| 5 | Investigate domain history | 🟢 Module 5 | Internal ticket found | [Exhibit 5](#ex5) |
| 6 | File case report — Alert 1 | 🟢 Module 6 | False Positive submitted | [Exhibit 6](#ex6) |
| 7 | Open the second alert | 🟣 Module 7 | Typosquat domain identified | [Exhibit 7](#ex7) |
| 8 | Confirm the click | 🔴 Module 8 | Firewall log shows `allowed` | [Exhibit 8](#ex8) |
| 9 | File case report — Alert 2 | 🟢 Module 9 | True Positive + escalation | [Exhibit 9](#ex9) |

---

## 🔵 Module 1–2 — Intake

Exhibits 1 to 2.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/SS1_Introduction_to_Phishing_Dashboard.PNG"><img src="screenshots/SS1_Introduction_to_Phishing_Dashboard.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Simulator loaded</b>
<br><sub>Scenario 1 ready</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/SS2_Introduction_to_Phishing_Alert_Queue.PNG"><img src="screenshots/SS2_Introduction_to_Phishing_Alert_Queue.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Alert queue</b>
<br><sub>5 pending alerts</sub>
</td>
</tr>
</table>

---

## 🟠 Module 3–4 — Assign & Review

Exhibits 3 to 4.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/SS3_Assigned_Alert.PNG"><img src="screenshots/SS3_Assigned_Alert.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Alert 8818 assigned</b>
<br><sub>Investigation begins</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/SS4_Alert_Details.PNG"><img src="screenshots/SS4_Alert_Details.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Raw email data</b>
<br><sub>hrconnex.thm onboarding email</sub>
</td>
</tr>
</table>

---

## 🟢 Module 5–6 — Alert 1 Investigation

Exhibits 5 to 6.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/SS5_SIEM_Search.PNG"><img src="screenshots/SS5_SIEM_Search.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Splunk search</b>
<br><sub>Internal ticket confirms legitimacy</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/SS8_Case_Report_Submitted.PNG"><img src="screenshots/SS8_Case_Report_Submitted.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Verdict filed</b>
<br><sub>False Positive submitted</sub>
</td>
</tr>
</table>

---

## 🟣🔴 Module 7–8 — Alert 2 Investigation

Exhibits 7 to 8.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/SS9_Second_Alert_Details.PNG"><img src="screenshots/SS9_Second_Alert_Details.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Typosquat domain</b>
<br><sub><code>m1crosoftsupport.co</code></sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/SS11_SIEM_Phishing_Proof.PNG"><img src="screenshots/SS11_SIEM_Phishing_Proof.PNG" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Click confirmed</b>
<br><sub>Firewall log: action <code>allowed</code></sub>
</td>
</tr>
</table>

---

## 🟢 Module 9 — Verdict Filed

Exhibit 9.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex9"></a>
<a href="screenshots/SS12_True_Positive_Submitted.PNG"><img src="screenshots/SS12_True_Positive_Submitted.PNG" width="380" alt="Exhibit 9"></a>
<br><b>Exhibit 9 — True Positive</b>
<br><sub>Escalated; isolation + password reset</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Alert 1 evidence found | Splunk domain search | Module 5 | ✅ Confirmed |
| Alert 1 verdict filed | Case report | Module 6 | ✅ Confirmed (FP) |
| Alert 2 typosquat identified | Domain string review | Module 7 | ✅ Confirmed |
| Alert 2 click confirmed | Firewall log | Module 8 | ✅ Confirmed |
| Alert 2 escalated with remediation | Case report | Module 9 | ✅ Confirmed (TP) |

> [!NOTE]
> Both alerts shared the identical surface pattern ("external link email") — only SIEM/firewall evidence separated the False Positive from the True Positive.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🚨 **[TryHackMe SOC Simulator](https://tryhackme.com/module/soc-simulator)**

</div>
