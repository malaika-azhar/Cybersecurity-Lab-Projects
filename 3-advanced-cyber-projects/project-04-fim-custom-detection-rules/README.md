<div align="center">

# 🛡️ Project 4
### File Integrity Monitoring & Custom Detection Rule Engineering
**SIEM Detection Engineering (Wazuh)**

![Wazuh](https://img.shields.io/badge/Wazuh-1A73E8?style=for-the-badge&logo=wazuh&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu_Server-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![XML](https://img.shields.io/badge/Custom_Rules-XML-F39C12?style=for-the-badge)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-Mapped-8E44AD?style=for-the-badge)
![Detection Engineering](https://img.shields.io/badge/Detection_Engineering-B03A2E?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-%240-117864?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-21618C?style=for-the-badge)

**Real-time File Integrity Monitoring configured on a live Linux endpoint, validated end-to-end against actual create/modify/delete events, and extended with two custom Wazuh detection rules — local account creation and SSH brute-force — each engineered, tuned against real triggered traffic, and mapped to MITRE ATT&CK.**

</div>

<br>

<div align="center">

## 📊 At a Glance

| 🧩 Modules | 🖼️ Screenshots | 📜 Custom Rules Written | 🎯 MITRE Techniques Mapped |
|:---:|:---:|:---:|:---:|
| **2** | **8** | **2 tested + 1 drafted** | **2** |

</div>

<br>

## 🖧 Environment

| Item | Value |
|---|---|
| SIEM Platform | Wazuh Manager / Indexer / Dashboard |
| Monitored Endpoint | Ubuntu Server (Wazuh Agent) |
| Config File | `/var/ossec/etc/ossec.conf` |
| Custom Rules File | `/var/ossec/etc/rules/local_rules.xml` |
| Tuning Tool | `wazuh-logtest` |

<br>

---

<div align="center">

## 🧭 Detection Engineering Pipeline

*How a raw endpoint event becomes a tuned, MITRE-tagged alert*

</div>

```mermaid
flowchart TB
    Raw["📥 RAW ENDPOINT LOG"]:::rawClass
    Decode["⚙️ DECODER PARSES FIELDS"]:::decodeClass
    Parent["🔗 MATCHES PARENT RULE"]:::parentClass
    Custom["🧩 CUSTOM RULE CHAINED"]:::customClass
    Fire["🚨 CUSTOM RULE FIRES"]:::fireClass
    Silent["⬜ NO ALERT — LOGGED ONLY"]:::silentClass
    Test["🧪 VERIFIED AGAINST REAL TRAFFIC"]:::testClass
    Tune["🔧 TUNE THRESHOLDS & CONDITIONS"]:::tuneClass
    Flag["🚩 FLAGGED AS UNTESTED"]:::flagClass
    Mitre["🎯 MAPPED TO MITRE ATT&CK"]:::mitreClass

    Raw --> Decode --> Parent --> Custom
    Custom -->|YES| Fire
    Custom -->|NO| Silent
    Fire --> Test
    Test -->|YES| Tune
    Test -->|NO| Flag
    Tune --> Mitre
    Flag --> Mitre

    classDef rawClass fill:#2C3E70,stroke:#131B3A,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef decodeClass fill:#1A5276,stroke:#0B2E43,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef parentClass fill:#117864,stroke:#083D33,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef customClass fill:#B9770E,stroke:#6E4409,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef fireClass fill:#1E8449,stroke:#0E4A28,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef silentClass fill:#707B7C,stroke:#3B4142,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef testClass fill:#B7950B,stroke:#6B5807,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef tuneClass fill:#76448A,stroke:#432752,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef flagClass fill:#943126,stroke:#571C16,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef mitreClass fill:#148F77,stroke:#0B5142,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px

    linkStyle default stroke:#2C3E50,stroke-width:4px
```

<br>

<div align="center">

## ⏱️ Project Flow

</div>

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
    title Project Flow — FIM to Tuned Detection Rules
    dateFormat YYYY-MM-DD
    axisFormat %s
    section File Integrity Monitoring
    Syscheck Config & Live Validation      :active, 2026-01-01, 1d
    section Rule Engineering
    Author, Trigger & Tune Custom Rules    :done, 2026-01-02, 1d
    section Verification
    Confirm Alerts on Dashboard            :crit, 2026-01-03, 1d
```
<p align="center"><em>Colors distinguish each project stage — all stages complete.</em></p>

<br>

<p align="center"><img src="screenshots/03_fim_alerts_timeline.png" width="650"></p>

<br>

---

## 🔵 Module 1 — File Integrity Monitoring (FIM)

**Objective:** Configure Wazuh's `syscheck` module for real-time monitoring on a core system directory, generate live file-system events on the monitored endpoint, and validate that added/modified/deleted events are correctly captured, decoded, and surfaced on the dashboard.

**Step 1 — Enable real-time syscheck on the target directory** ✅
```xml
<syscheck>
  <disabled>no</disabled>
  <frequency>300</frequency>
  <scan_on_start>yes</scan_on_start>
  <directories realtime="yes" report_changes="yes">/etc</directories>
  <directories realtime="yes" report_changes="no">/var/log</directories>
</syscheck>
```
`report_changes="yes"` was enabled on the high-value config directory so content-level diffs are captured, while the high-volume, low-signal log directory was left as notification-only to avoid excessive diff storage.

<p align="center"><img src="screenshots/01_fim_syscheck_config.png" width="600"></p>

**Step 2 — Restart the agent and confirm it comes back Active** ✅
<p align="center"><img src="screenshots/02_agent_active_status.png" width="600"></p>

**Step 3 — Generate a full file lifecycle on the monitored path** ✅
```bash
touch /etc/test_file.txt      # create
echo "edit" >> /etc/test_file.txt   # modify
rm /etc/test_file.txt         # delete
```

**Step 4 — Confirm all three lifecycle events on the dashboard** ✅
<p align="center"><img src="screenshots/03_fim_alerts_timeline.png" width="600"></p>

🎯 **Result:** All three lifecycle events landed in the File Integrity Monitoring view with correct rule IDs and matching timestamps.

| Change | Rule ID | Rule Description |
|---|:---:|---|
| Added | `554` | File added to the system |
| Modified | `550` | Integrity checksum changed |
| Deleted | `553` | File deleted |

<br>

<div align="center">

### 🌟 Coverage Snapshot

| 🛡️ Layer | ✅ Status | 📌 Detail |
|:---:|:---:|:---|
| File Integrity Monitoring | Live | Real-time on `/etc`, notification-only on `/var/log` |
| Detection Rules | 2 Firing | New-user creation + SSH brute-force |
| MITRE Coverage | 2 Techniques | T1136.001 · T1110.001 |
| Untested Rule | 1 Drafted | External storage insertion — ready, no matching endpoint yet |

</div>

<br>

---



## 🟢 Module 2 — Custom Detection Rule Engineering

**Objective:** Move beyond default, generic SIEM rules and author detection logic tailored to specific threat scenarios, chaining onto parent rules rather than parsing raw logs from scratch, and validate each rule against real triggered traffic before trusting it.

```
[Raw Endpoint Log] → [Decoder Parses Fields] → [Parent Rule Matches] → [Custom Rule Chains & Fires]
```

**Step 5 — Author the custom rule set** ✅
```xml
<group name="syslog,sshd,windows,">

  <!-- Rule 1: Local user account creation -->
  <rule id="100001" level="10">
    <if_sid>5501</if_sid>
    <match>new user</match>
    <description>New local user account has been created on Linux system.</description>
    <mitre><id>T1136.001</id></mitre>
  </rule>

  <!-- Rule 2: SSH brute-force detection -->
  <rule id="100002" level="12" frequency="5" timeframe="120">
    <if_matched_sid>5710</if_matched_sid>
    <same_source_ip />
    <description>SSH Brute Force attack detected from source IP.</description>
    <mitre><id>T1110.001</id></mitre>
  </rule>

  <!-- Rule 3: External storage device insertion (drafted, pending a matching endpoint) -->
  <rule id="100003" level="7">
    <if_sid>60001</if_sid>
    <field name="win.system.eventID">^2003$|^1006$</field>
    <description>External storage device insertion detected on host.</description>
    <mitre><id>T1200</id></mitre>
  </rule>

</group>
```
<p align="center"><img src="screenshots/04_custom_rules_xml.png" width="600"></p>

**Step 6 — Trigger Rule 100001 with a real account-creation event** ✅
```bash
sudo adduser test_user
```
<p align="center"><img src="screenshots/05_adduser_trigger.png" width="600"></p>

**Step 7 — Confirm Rule 100001 fires on the dashboard** ✅
<p align="center"><img src="screenshots/07_rule100001_alert.png" width="600"></p>

**Step 8 — Trigger Rule 100002 with a real SSH brute-force burst** ✅
```bash
for i in {1..10}; do ssh -o ConnectTimeout=2 -o PubkeyAuthentication=no wronguser@localhost; done
```
<p align="center"><img src="screenshots/06_ssh_bruteforce_trigger.png" width="600"></p>

**Step 9 — Confirm Rule 100002 fires on the dashboard** ✅
<p align="center"><img src="screenshots/08_rule100002_alert.png" width="600"></p>

🎯 **Result:** Both rules fired correctly against real triggered traffic, each mapped to a MITRE ATT&CK technique.

| Rule ID | Description | MITRE Technique | Status |
|:---:|---|---|:---:|
| `100001` | Local user account creation | T1136.001 — Create Account: Local Account | ✅ Tested & Firing |
| `100002` | SSH brute-force detection | T1110.001 — Brute Force: Password Guessing | ✅ Tested & Firing |
| `100003` | External storage insertion | T1200 — Hardware Additions | ⏳ Drafted, pending endpoint |

**Tuning note:** `wazuh-logtest` showed the SSH auth-failure baseline actually matched parent rule `5710` (invalid user), not `5716` as first assumed — Rule 100002 was corrected accordingly. `<same_source_ip />` combined with `frequency="5"` and `timeframe="120"` restricts the match to a genuine burst from one source within a 2-minute window, separating automated brute force from ordinary mistyped passwords.

<br>

---

## 📝 Project Summary

| Module | Tooling | Key Finding |
|---|---|---|
| File Integrity Monitoring | `syscheck`, Wazuh Dashboard | Full add/modify/delete lifecycle captured with correct rule IDs |
| Custom Rule Engineering | `local_rules.xml`, `wazuh-logtest` | Two rules authored, tuned against real traffic, and MITRE-mapped |

## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| SSH brute-force rule assumed parent `5716` but never fired | Used `wazuh-logtest` to trace the real parent rule (`5710`) and corrected the chain |
| Loose brute-force matching risked false positives from simultaneous unrelated logins | Added `<same_source_ip />` alongside `frequency`/`timeframe` to isolate genuine bursts |
| USB-insertion rule had no matching endpoint to validate against | Rule left syntactically integrated and clearly marked as untested rather than falsely presented as verified |

## 🧠 What I Learned
Raw logs can't be evaluated directly — the decoder has to parse them into structured fields before any rule logic can run, and parent-rule chaining (`if_sid` / `if_matched_sid`) means new detection logic inherits already-parsed fields instead of being built from scratch. `frequency` alone, without a bounded `timeframe`, can fire on events that are days apart — the two have to work together to encode a genuine rate-based condition. And a rule that *looks* syntactically correct is not the same as a rule that fires correctly: the only way to know is to generate the real traffic and check the log every time.

## 📁 Repo Structure
```
project-04-fim-custom-detection-rules/
├── README.md
└── screenshots/
    ├── 01_fim_syscheck_config.png
    ├── 02_agent_active_status.png
    ├── 03_fim_alerts_timeline.png
    ├── 04_custom_rules_xml.png
    ├── 05_adduser_trigger.png
    ├── 06_ssh_bruteforce_trigger.png
    ├── 07_rule100001_alert.png
    └── 08_rule100002_alert.png
```
