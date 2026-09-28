<a id="top"></a>
<div align="center">

# 🦠 Project 04 — Index
### Threat Framework Mapping — WannaCry Case Study
**Project 04 of 10 — Foundational Projects**

![ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-C8102E?style=for-the-badge)
![D3FEND](https://img.shields.io/badge/MITRE_D3FEND-148F77?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🗺️ Frameworks | 🎯 Malware |
|:---:|:---:|:---:|:---:|
| **5** | **5** | **3** | **WannaCry (S0366)** |

</div>

<p align="center">🧩 <b>Frameworks:</b> MITRE ATT&CK · Pyramid of Pain · MITRE D3FEND</p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Establish the ATT&CK baseline | 🔵 Module 1 | Matrix opened as reference point | [Exhibit 1](#ex1) |
| 2 | Extract WannaCry's technical profile | 🟠 Module 2 | Located via Software DB (S0366) | [Exhibit 2](#ex2) |
| 3 | Map indicators to the Pyramid of Pain | 🟣 Module 3 | Hashes low, TTPs high | [Exhibit 3](#ex3) |
| 4 | Drill into detection strategy | 🟢 Module 4 | T1543 monitoring guidance pulled | [Exhibit 4](#ex4) |
| 5 | Map defensive countermeasures | 🔴 Module 5 | D3FEND controls mapped to T1543 | [Exhibit 5](#ex5) |

---

## 🔵 Module 1 — Baseline

Exhibit 1.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/SS-1_Mitre_Attack_Framework_Home.PNG"><img src="screenshots/SS-1_Mitre_Attack_Framework_Home.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — ATT&CK Matrix</b>
<br><sub>Homepage / baseline reference opened</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠 Module 2 — Attacker View

Exhibit 2.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/SS-2_WannaCry_Technique_Mapping.PNG"><img src="screenshots/SS-2_WannaCry_Technique_Mapping.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — WannaCry TTPs</b>
<br><sub>Profile S0366 located after name search failed</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟣 Module 3 — Indicator Triage

Exhibit 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/SS-3_Pyramid_of_Pain_Notes.PNG"><img src="screenshots/SS-3_Pyramid_of_Pain_Notes.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Indicators ranked</b>
<br><sub>File hashes vs. TTPs on the Pyramid of Pain</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟢 Module 4 — Detection Drill

Exhibit 4.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/SS-4_WannaCry_Detection_Controls.PNG"><img src="screenshots/SS-4_WannaCry_Detection_Controls.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — T1543 guidance</b>
<br><sub><code>sc.exe</code> / <code>powershell.exe</code> monitoring</sub>
</td>
<td></td>
</tr>
</table>

---

## 🔴 Module 5 — Defender View

Exhibit 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/SS-5_Mitre_D3fend_Defensive_Matrix.PNG"><img src="screenshots/SS-5_Mitre_D3fend_Defensive_Matrix.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Countermeasures mapped</b>
<br><sub>D3FEND controls tied back to T1543</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| WannaCry located by ID after name search failed | Software DB, S0366 | Module 2 | ✅ Confirmed |
| Indicators explicitly ranked | Pyramid of Pain | Module 3 | ✅ Confirmed |
| Detection guidance pulled for T1543 | ATT&CK technique page | Module 4 | ✅ Confirmed |
| Countermeasures mapped back to T1543 | D3FEND matrix | Module 5 | ✅ Confirmed |

> [!NOTE]
> ATT&CK's search bar returned "No Results" for "WannaCry" — the entry was found by navigating directly to the Software database by ID (S0366) instead.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🎯 **[MITRE ATT&CK](https://attack.mitre.org/)** · 🛡️ **[MITRE D3FEND](https://d3fend.mitre.org/)** · 🔺 **[Pyramid of Pain](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)**

</div>
