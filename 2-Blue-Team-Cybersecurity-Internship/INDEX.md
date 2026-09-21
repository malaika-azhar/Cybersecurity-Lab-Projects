<a id="top"></a>
<div align="center">

# 📇 Index — Blue Team Internship Reports
### Weeks 1–12 · SOC Operations to Digital Forensics
**2 Phases · 12 Weekly Deliverable Reports**

![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-005EB8?style=for-the-badge&logo=wazuh&logoColor=white)
![Suricata](https://img.shields.io/badge/NIDS-Suricata-EF3B2D?style=for-the-badge)
![pfSense](https://img.shields.io/badge/Firewall-pfSense-212121?style=for-the-badge&logo=pfsense&logoColor=white)
![Autopsy](https://img.shields.io/badge/Forensics-Autopsy-6f42c1?style=for-the-badge)
![Kali](https://img.shields.io/badge/Lab-Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Reports-12_of_12-brightgreen?style=for-the-badge)

**Quick guide to every weekly report in this folder.**

### [📖 Open the full README](README.md)

</div>

---

<div align="center">

| 📄 Reports | 📚 Total Pages | 🗓️ Weeks | 🧭 Phases |
|:---:|:---:|:---:|:---:|
| **12** | **298** | **12** | **2** |

</div>

<p align="center">🧩 <b>Lab:</b> VirtualBox lab (Kali, Ubuntu, Windows, pfSense, Wazuh) ➜ detection and network defense · Forensic images and artefacts ➜ investigation</p>

---

## 📑 Week Index

All 12 weeks at a glance, with the report for each.

| # | Focus | Phase | Key Tools | Report |
|:---:|---|:---:|---|:---:|
| 1 | SOC foundations and lab setup | 🔵 One | Wazuh | [Week 01](REPORTS/Week01_Report.pdf) |
| 2 | FIM, custom rules, log analysis, active response | 🔵 One | Wazuh | [Week 02](REPORTS/Week02_Report.pdf) |
| 3 | Suricata IDS and Wazuh integration | 🔵 One | Suricata, ipset, iptables | [Week 03](REPORTS/Week03_Report.pdf) |
| 4 | pfSense, threat intel, vulnerability assessment | 🔵 One | pfSense, VirusTotal, URLhaus | [Week 04](REPORTS/Week04_Report.pdf) |
| 5 | Malware analysis and detection engineering | 🔵 One | ANY.RUN, binwalk, Suricata | [Week 05](REPORTS/Week05_Report.pdf) |
| 6 | Phase One capstone | 🔵 One | Full lab | [Week 06](REPORTS/Week06_Report.pdf) |
| 7 | Disk imaging and file system analysis | 🟣 Two | Sleuth Kit, analyzeMFT | [Week 07](REPORTS/Week07_Report.pdf) |
| 8 | Windows artefact analysis | 🟣 Two | PECmd, event logs | [Week 08](REPORTS/Week08_Report.pdf) |
| 9 | Browser forensics and LNK analysis | 🟣 Two | BrowsingHistoryView, LECmd | [Week 09](REPORTS/Week09_Report.pdf) |
| 10 | Autopsy triage and registry analysis | 🟣 Two | Autopsy | [Week 10](REPORTS/Week10_Report.pdf) |
| 11 | Email forensics and super timeline | 🟣 Two | Autopsy, timeline tools | [Week 11](REPORTS/Week11_Report.pdf) |
| 12 | Final case: M57.biz capstone | 🟣 Two | Autopsy | [Week 12](REPORTS/Week12_Report.pdf) |

---

## 🔵 Phase One — SOC Operations

Weeks 1 to 6. Each card links to the full PDF.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="wk1"></a>
<img src="https://img.shields.io/badge/Week-01-1A5276?style=for-the-badge" alt="Week 1"><br>
<b>SOC Foundations & Lab Setup</b>
<br><sub>Wazuh Manager deployment and agent onboarding. A hardware-limited install moved to a hosted trial</sub>
<br><a href="REPORTS/Week01_Report.pdf">📄 Open PDF</a> · 27 pages
</td>
<td align="center" valign="top" width="50%">
<a id="wk2"></a>
<img src="https://img.shields.io/badge/Week-02-1A5276?style=for-the-badge" alt="Week 2"><br>
<b>FIM, Custom Rules & Active Response</b>
<br><sub>File integrity monitoring, custom Wazuh rules, Windows security events and correlated activity</sub>
<br><a href="REPORTS/Week02_Report.pdf">📄 Open PDF</a> · 37 pages
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="wk3"></a>
<img src="https://img.shields.io/badge/Week-03-1A5276?style=for-the-badge" alt="Week 3"><br>
<b>Suricata IDS & Wazuh Integration</b>
<br><sub>3 custom Suricata rules, <code>eve.json</code> ingestion, GeoIP blocking with ipset and iptables</sub>
<br><a href="REPORTS/Week03_Report.pdf">📄 Open PDF</a> · 30 pages
</td>
<td align="center" valign="top" width="50%">
<a id="wk4"></a>
<img src="https://img.shields.io/badge/Week-04-1A5276?style=for-the-badge" alt="Week 4"><br>
<b>pfSense, Threat Intel & Vulnerabilities</b>
<br><sub>Managed perimeter, live URLhaus feed (20,826 indicators), OpenSSH findings 30 to 6 after patching</sub>
<br><a href="REPORTS/Week04_Report.pdf">📄 Open PDF</a> · 27 pages
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="wk5"></a>
<img src="https://img.shields.io/badge/Week-05-1A5276?style=for-the-badge" alt="Week 5"><br>
<b>Malware Analysis & Detection Engineering</b>
<br><sub>2 samples analysed, 12 IOC/IOA entries, custom Suricata rule matched 8 of 8 in isolated replay</sub>
<br><a href="REPORTS/Week05_Report.pdf">📄 Open PDF</a> · 31 pages
</td>
<td align="center" valign="top" width="50%">
<a id="wk6"></a>
<img src="https://img.shields.io/badge/Week-06-1A5276?style=for-the-badge" alt="Week 6"><br>
<b>Phase One Capstone</b>
<br><sub>Insider-threat simulation and incident response, bringing the first six weeks together</sub>
<br><a href="REPORTS/Week06_Report.pdf">📄 Open PDF</a> · 14 pages
</td>
</tr>
</table>

---

## 🟣 Phase Two — Digital Forensics & Incident Response

Weeks 7 to 12. Each card links to the full PDF.

<table>
<tr>
<td align="center" valign="top" width="50%">
<a id="wk7"></a>
<img src="https://img.shields.io/badge/Week-07-6f42c1?style=for-the-badge" alt="Week 7"><br>
<b>Disk Imaging & File System Analysis</b>
<br><sub>E01 imaging with hash verification, NTFS alternate data streams, Sleuth Kit triage and deleted-file recovery</sub>
<br><a href="REPORTS/Week07_Report.pdf">📄 Open PDF</a> · 25 pages
</td>
<td align="center" valign="top" width="50%">
<a id="wk8"></a>
<img src="https://img.shields.io/badge/Week-08-6f42c1?style=for-the-badge" alt="Week 8"><br>
<b>Windows Artefact Analysis</b>
<br><sub>Event logs, Prefetch execution records, thumbcache and Recycle Bin on a live endpoint</sub>
<br><a href="REPORTS/Week08_Report.pdf">📄 Open PDF</a> · 23 pages
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="wk9"></a>
<img src="https://img.shields.io/badge/Week-09-6f42c1?style=for-the-badge" alt="Week 9"><br>
<b>Browser Forensics & LNK Analysis</b>
<br><sub>Chrome profile forensics and 75 of 75 LNK files parsed with zero errors</sub>
<br><a href="REPORTS/Week09_Report.pdf">📄 Open PDF</a> · 23 pages
</td>
<td align="center" valign="top" width="50%">
<a id="wk10"></a>
<img src="https://img.shields.io/badge/Week-10-6f42c1?style=for-the-badge" alt="Week 10"><br>
<b>Autopsy Triage & Registry Analysis</b>
<br><sub>Triage, artefact hunting and registry analysis on a forensic image</sub>
<br><a href="REPORTS/Week10_Report.pdf">📄 Open PDF</a> · 26 pages
</td>
</tr>
<tr>
<td align="center" valign="top" width="50%">
<a id="wk11"></a>
<img src="https://img.shields.io/badge/Week-11-6f42c1?style=for-the-badge" alt="Week 11"><br>
<b>Email Forensics & Super Timeline</b>
<br><sub>Email extraction, artefact corroboration and the start-big, filter-down timeline method</sub>
<br><a href="REPORTS/Week11_Report.pdf">📄 Open PDF</a> · 12 pages
</td>
<td align="center" valign="top" width="50%">
<a id="wk12"></a>
<img src="https://img.shields.io/badge/Week-12-6f42c1?style=for-the-badge" alt="Week 12"><br>
<b>Final Case — M57.biz Capstone</b>
<br><sub>Disk, memory and USB exfiltration analysis of a data-leak case</sub>
<br><a href="REPORTS/Week12_Report.pdf">📄 Open PDF</a> · 23 pages
</td>
</tr>
</table>

---

### 📈 Numbers at a Glance

Taken directly from the reports.

| Week | Measure | Result |
|:---:|---|:---:|
| 3 | Custom Suricata rules validated | **3** |
| 3 | Suricata alerts confirmed in the Wazuh dashboard | **2,737** |
| 4 | Threat-feed indicators loaded into a CDB list | **20,826** |
| 4 | OpenSSH findings after a verified patch | **30 → 6** |
| 5 | Malware samples analysed | **2** |
| 5 | Consolidated IOC / IOA entries | **12** |
| 5 | Custom rule matches in isolated replay | **8 / 8** |
| 9 | LNK files parsed with zero errors | **75 / 75** |

---

## 🎯 Verification Checklist

| Check | Method | Layer | Status |
|:---:|---|---|:---:|
| Log pipeline delivers | `ss` showing an active listener on UDP 514 | Network | ✅ Confirmed (Week 4) |
| Patch closed the gap | Re-scan filtered to patched packages | Host | ✅ Confirmed (Week 4) |
| Custom rule works alone | Isolated replay with only that rule loaded | Network | ✅ Confirmed (Week 5) |
| Lab isolation | Failed ping after disabling the adapter at the hypervisor | Lab | ✅ Confirmed (Week 5) |
| Sample integrity | Hashes compared with published values | Lab | ✅ Confirmed (Week 5) |
| Host-side correlation | File-integrity alert to pair with the network alert | Host | ❌ Not captured (Week 3) |
| Second Suricata rule live test | Replay against the second sample | Network | ❌ Not covered (Week 5) |
| Wazuh custom rules, incident-response plan | Not started | Host | ❌ Not covered (Week 5) |
| Case findings from the evidence image | Image could not be accessed | Forensics | ❌ Methodology only (Week 11) |
| Disk and memory analysis | Marked as pending | Forensics | ❌ Pending (Week 12) |

> [!NOTE]
> Gaps are listed here rather than hidden. Each one is explained in the report for that week. Screenshots live inside the PDFs, and sensitive identifiers such as API keys and internal file names are redacted.

---

<div align="center">

[⬆️ Back to top](#top) &nbsp;·&nbsp; [📖 Full README](README.md)

🛡️ **[Wazuh](https://wazuh.com)** · 🔎 **[Suricata](https://suricata.io)** · 🌐 **[pfSense](https://www.pfsense.org)** · 🧬 **[Autopsy](https://www.autopsy.com)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)** · 📈 **[Detection-to-Response Pipeline](README.md#pipeline)**

</div>
