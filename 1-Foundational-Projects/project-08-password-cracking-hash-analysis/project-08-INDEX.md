<a id="top"></a>
<div align="center">

# 🔓 Project 08 — Index
### Password Cracking & Hash Analysis
**Project 08 of 10 — Foundational Projects**

![John](https://img.shields.io/badge/John_the_Ripper-DA3B3B?style=for-the-badge)
![TryHackMe](https://img.shields.io/badge/TryHackMe-212C42?style=for-the-badge&logo=tryhackme&logoColor=white)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**Quick guide to every step and screenshot in this project.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 🧩 Modules | 🖼️ Screenshots | 🔑 Hashes Cracked | ⏱️ Time Each |
|:---:|:---:|:---:|:---:|
| **8** | **8** | **3 / 3** | **< 1 sec** |

</div>

<p align="center">🧩 <b>Lab:</b> TryHackMe "Crack the Hash" · John the Ripper · <code>rockyou.txt</code></p>

---

## 📑 Step Index

| # | Step | Module | Result | Evidence |
|:---:|---|:---:|---|:---:|
| 1 | Start the room | 🔵 Module 1 | AttackBox launched | [Exhibit 1](#ex1) |
| 2 | Identify Hash 1 | 🟠 Module 2 | MD5 confirmed | [Exhibit 2](#ex2) |
| 3 | Crack Hash 1 | 🟢 Module 3 | `easy` | [Exhibit 3](#ex3) |
| 4 | Identify Hash 2 | 🟠 Module 4 | MD5 confirmed | [Exhibit 4](#ex4) |
| 5 | Crack Hash 2 | 🟢 Module 5 | `123` | [Exhibit 5](#ex5) |
| 6 | Identify Hash 3 | 🟠 Module 6 | SHA-1 confirmed | [Exhibit 6](#ex6) |
| 7 | Run crack command for Hash 3 | 🟢 Module 7 | John the Ripper run | [Exhibit 7](#ex7) |
| 8 | Confirm Hash 3 cracked | 🟢 Module 8 | `password`, 0 left | [Exhibit 8](#ex8) |

---

## 🔵 Module 1 — Setup

Exhibit 1.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex1"></a>
<a href="screenshots/SS1_Room_Started.PNG"><img src="screenshots/SS1_Room_Started.PNG" width="380" alt="Exhibit 1"></a>
<br><b>Exhibit 1 — Room started</b>
<br><sub>AttackBox launched</sub>
</td>
<td></td>
</tr>
</table>

---

## 🟠🟢 Module 2–3 — Hash 1

Exhibits 2 to 3.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex2"></a>
<a href="screenshots/SS2_Hash1_Identify.PNG"><img src="screenshots/SS2_Hash1_Identify.PNG" width="380" alt="Exhibit 2"></a>
<br><b>Exhibit 2 — Hash 1 identified</b>
<br><sub>MD5</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex3"></a>
<a href="screenshots/SS3_Hash1_Cracked.PNG"><img src="screenshots/SS3_Hash1_Cracked.PNG" width="380" alt="Exhibit 3"></a>
<br><b>Exhibit 3 — Hash 1 cracked</b>
<br><sub>Password: <code>easy</code></sub>
</td>
</tr>
</table>

---

## 🟠🟢 Module 4–5 — Hash 2

Exhibits 4 to 5.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex4"></a>
<a href="screenshots/SS4_Hash2_Identify.PNG"><img src="screenshots/SS4_Hash2_Identify.PNG" width="380" alt="Exhibit 4"></a>
<br><b>Exhibit 4 — Hash 2 identified</b>
<br><sub>MD5</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex5"></a>
<a href="screenshots/SS5_Hash2_Cracked.PNG"><img src="screenshots/SS5_Hash2_Cracked.PNG" width="380" alt="Exhibit 5"></a>
<br><b>Exhibit 5 — Hash 2 cracked</b>
<br><sub>Password: <code>123</code></sub>
</td>
</tr>
</table>

---

## 🟠🟢 Module 6–8 — Hash 3

Exhibits 6 to 8.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex6"></a>
<a href="screenshots/SS6_Hash3_Identify.PNG"><img src="screenshots/SS6_Hash3_Identify.PNG" width="380" alt="Exhibit 6"></a>
<br><b>Exhibit 6 — Hash 3 identified</b>
<br><sub>SHA-1</sub>
</td>
<td align="center" valign="top" width="50%">
<a id="ex7"></a>
<a href="screenshots/SS7_Hash3_Crack_Command.PNG"><img src="screenshots/SS7_Hash3_Crack_Command.PNG" width="380" alt="Exhibit 7"></a>
<br><b>Exhibit 7 — Crack command run</b>
<br><sub>John the Ripper against Hash 3</sub>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="ex8"></a>
<a href="screenshots/SS8_Hash3_Cracked.PNG"><img src="screenshots/SS8_Hash3_Cracked.PNG" width="380" alt="Exhibit 8"></a>
<br><b>Exhibit 8 — Hash 3 cracked</b>
<br><sub>Password: <code>password</code>, 0 left</sub>
</td>
<td></td>
</tr>
</table>

---

## 🎯 Verification Checklist

| Check | Method | Module | Status |
|:---:|---|---|:---:|
| Hash 1 identified & cracked | `hashid`, John the Ripper | Modules 2–3 | ✅ Confirmed (MD5 → `easy`) |
| Hash 2 identified & cracked | `hashid`, John the Ripper | Modules 4–5 | ✅ Confirmed (MD5 → `123`) |
| Hash 3 identified & cracked | `hashid`, John the Ripper | Modules 6–8 | ✅ Confirmed (SHA-1 → `password`) |

> [!NOTE]
> Hash 3 (SHA-1, a stronger algorithm) cracked just as fast as the two MD5 hashes — proving crack speed depends on password predictability, not algorithm strength.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🔓 **[TryHackMe — Crack the Hash](https://tryhackme.com/room/crackthehash)** · 🛠️ **[John the Ripper](https://www.openwall.com/john/)**

</div>
