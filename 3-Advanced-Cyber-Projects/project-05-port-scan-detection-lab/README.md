<div align="center">

# 🔍 Port Scan Detection Lab

**Project 07 of 29 — Advanced Cyber Projects**

Network IDS Rule Engineering (Suricata)

![Suricata](https://img.shields.io/badge/IDS-Suricata-CC0000?style=for-the-badge&logo=suricata&logoColor=white)
![Kali](https://img.shields.io/badge/Attacker-Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-T1046-C8102E?style=for-the-badge)
![Detection Engineering](https://img.shields.io/badge/Focus-Signature_Iteration-6f42c1?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free_%26_Open--Source-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A custom Suricata signature written to detect a stealth Nmap NULL scan — tested against real scan traffic, corrected after its first form under-performed, and pushed live into a running sensor without a service restart.

### [📑 Open the visual index](INDEX.md)

</div>

---

## 📑 Table of Contents

1. [At a Glance](#at-a-glance)
2. [Project Background](#project-background)
3. [Environment](#environment)
4. [Project Flow](#project-flow)
5. [Module 1 — Signature Authoring & Iteration](#module-1)
6. [Coverage Snapshot](#coverage-snapshot)
7. [Detection Pipeline](#detection-pipeline)
8. [Module 2 — Live Verification & Reload](#module-2)
9. [MITRE ATT&CK Mapping](#mitre-mapping)
10. [Project Summary](#project-summary)
11. [Challenges & Fixes](#challenges-fixes)
12. [Scope & Limitations](#scope-limitations)
13. [What I Learned](#what-i-learned)
14. [Skills Demonstrated](#skills-demonstrated)
15. [Screenshot Index](#screenshot-index)
16. [Repo Structure](#repo-structure)

---

<a id="at-a-glance"></a>
## 📊 At a Glance

| 🧩 Modules | 🖼️ Screenshots | 📜 Signature Revisions | 🎯 MITRE Techniques |
|:---:|:---:|:---:|:---:|
| **2** | **4** | **2 (iterated live)** | **1** |

---

<a id="project-background"></a>
## 📖 Project Background

A NULL scan sends TCP packets with every control flag cleared — real TCP communication always sets at least one flag, so a completely flagless packet is not something a legitimate client ever produces. It is a fingerprint of a stealth scanning tool deliberately probing port state without completing a handshake. This project writes a signature to catch exactly that pattern, then proves the signature works against real generated traffic rather than trusting it on the strength of its syntax alone.

- **Module 1 — Signature Authoring & Iteration:** Update the ruleset, author the detection logic, and correct it after the first form failed to reliably fire.
- **Module 2 — Live Verification & Reload:** Trigger a real scan, confirm the alert in the sensor's own log, and push the corrected rule into a running sensor without any capture downtime.

> [!NOTE]
> The first version of this signature looked more precise on paper than the version that actually worked. Both are documented here, because understanding *why* the more deliberate-looking syntax under-performed is itself part of the detection-engineering skill.

<div align="center">

### 🧩 Detection Setup at a Glance

<table>
<tr>
<td align="center" valign="top" width="30%">

![Kali](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)

**Scanning Source**<br>
<sub><code>nmap -sN</code><br>Stealth NULL scan</sub>

</td>
<td align="center" valign="middle" width="10%">

**➜**

</td>
<td align="center" valign="top" width="30%">

![Suricata](https://img.shields.io/badge/Suricata-CC0000?style=for-the-badge&logo=suricata&logoColor=white)

**Detection Engine**<br>
<sub>Custom rule in<br><code>local.rules</code></sub>

</td>
<td align="center" valign="middle" width="10%">

**➜**

</td>
<td align="center" valign="top" width="20%">

**📄 fast.log**<br>
<sub>Alert confirmed<br>with SID and revision</sub>

</td>
</tr>
</table>

</div>

---

<a id="environment"></a>
## 🖧 Environment

| Item | Value |
|---|---|
| **IDS Platform** | Suricata 8.0.6 RELEASE |
| **Capture Interface** | `eth0` (af-packet) |
| **Rule File** | `/etc/suricata/rules/local.rules` |
| **Alert Log** | `/var/log/suricata/fast.log` |
| **Reload Method** | `suricatasc -c reload-rules` (live, no restart) |
| **Scan Tool** | Nmap — `nmap -sN` (TCP NULL scan) |

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
    title Project Flow — Signature Draft to Live-Verified Rule
    dateFormat YYYY-MM-DD
    axisFormat %b %d
    section Signature Authoring
    Update Ruleset & Author Detection Logic   :active, 2026-07-18, 1d
    section Iteration
    Diagnose Non-Firing Revision & Correct    :done, 2026-07-18, 1d
    section Verification
    Trigger Real Scan & Reload Live           :crit, 2026-07-18, 1d
```
<p align="center"><em>Colors distinguish each project stage — all stages complete.</em></p>

---

<a id="module-1"></a>
## 🔵 Module 1 — Signature Authoring & Iteration

**Objective:** Update Suricata's ruleset against the latest Emerging Threats Open feed, then author a signature that matches the specific packet-level fingerprint of a stealth NULL scan.

### Step 1 — Update the ruleset ✅

```bash
sudo suricata-update
```

<p align="center">
  <img src="screenshots/Exhibit1_suricata_update_clean_run.png" alt="Exhibit 1 - suricata-update clean run" width="850"><br>
  <em>Exhibit 1 — Clean <code>suricata-update</code> run confirming the remote checksum was successfully verified against the Emerging Threats Open ruleset</em>
</p>

### Step 2 — Author the detection logic ✅

```text
alert tcp any any -> any any (msg:"CUSTOM Nmap NULL Scan Detected"; flags:0; sid:9000001; rev:3;)
```

The `flags:0` bitmask matches a TCP packet where every control flag byte evaluates to a clean zero — the exact fingerprint of a NULL scan probe, since a legitimate handshake always sets at least one flag.

### 🔍 Iteration Note — Why the More Deliberate Syntax Under-performed

```mermaid
flowchart TD
    A["✍️ Rev 1/2 — Negated flag list<br/>flags:!FSRPAU"] --> B{"Fires reliably against<br/>real NULL scan traffic?"}
    B -->|No| C["🔎 Diagnose: raw engine parsing<br/>favors the plain bitmask form"]
    C --> D["✍️ Rev 3 — Bitmask form<br/>flags:0"]
    D --> E{"Fires reliably?"}
    E -->|Yes| F["✅ Documented as the<br/>working, final signature"]

    classDef draft fill:#fff4e5,stroke:#e08a00,stroke-width:2px,color:#000
    classDef decision fill:#f1ecfb,stroke:#6f42c1,stroke-width:2px,color:#000
    classDef bad fill:#fdeaea,stroke:#C8102E,stroke-width:2px,color:#000
    classDef good fill:#eef7ee,stroke:#2ea44f,stroke-width:2px,color:#000
    class A draft
    class B,E decision
    class C bad
    class D draft
    class F good
```

The first instinct was that explicitly excluding every named flag (`flags:!FSRPAU`) would be a more precise match than the bare zero-value shorthand. In practice, the plain bitmask form (`flags:0`) is what the engine matched reliably. This is recorded rather than hidden, because a signature that *looks* more precise is not the same as a signature that *fires* correctly — the only way to know is to generate the real traffic and check the log.

---

<a id="coverage-snapshot"></a>
## 🌟 Coverage Snapshot

| 🛡️ Layer | ✅ Status | 📌 Detail |
|---|---|---|
| Ruleset Currency | Updated | Emerging Threats Open, checksum verified |
| Signature Authored | Complete | `sid:9000001` — NULL scan bitmask match |
| Live Traffic Test | Fired | Real `nmap -sN` scan against the monitored host |
| Live Reload | Confirmed | Pushed via `suricatasc`, zero capture downtime |

---

<a id="detection-pipeline"></a>
## 🧭 Detection Pipeline

How a scan packet becomes a verified, reloadable signature

```mermaid
flowchart TB
    Packet["📥 TCP PACKET, ALL FLAGS CLEARED"]:::packetClass
    Capture["🌐 CAPTURED ON ETH0 (AF-PACKET)"]:::captureClass
    Match["🎯 MATCHED AGAINST FLAGS:0"]:::matchClass
    Fire["🚨 SIGNATURE FIRES"]:::fireClass
    Log["📝 WRITTEN TO FAST.LOG"]:::logClass
    Verify["🧪 VERIFIED AGAINST REAL SCAN"]:::verifyClass
    Reload["🔄 PUSHED LIVE, NO RESTART"]:::reloadClass

    Packet --> Capture --> Match --> Fire --> Log --> Verify --> Reload

    classDef packetClass fill:#2C3E70,stroke:#131B3A,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef captureClass fill:#1A5276,stroke:#0B2E43,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef matchClass fill:#B9770E,stroke:#6E4409,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef fireClass fill:#1E8449,stroke:#0E4A28,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef logClass fill:#707B7C,stroke:#3B4142,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef verifyClass fill:#B7950B,stroke:#6B5807,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px
    classDef reloadClass fill:#76448A,stroke:#432752,stroke-width:5px,color:#FFFFFF,font-weight:bold,font-size:16px

    linkStyle default stroke:#2C3E50,stroke-width:4px
```

---

<a id="module-2"></a>
## 🟢 Module 2 — Live Verification & Reload

**Objective:** Trigger the signature with a real scan, confirm the exact alert in the sensor's own log, document the rationale behind the detection logic, and push the corrected rule into a running sensor without interrupting capture.

### Step 3 — Trigger a real NULL scan ✅

```bash
nmap -sN 192.168.56.107
```

### Step 4 — Confirm the signature fires in fast.log ✅

<p align="center">
  <img src="screenshots/Exhibit2_nmap_null_scan_alert_firing.png" alt="Exhibit 2 - NULL scan alert firing" width="850"><br>
  <em>Exhibit 2 — <code>fast.log</code> confirming <b>CUSTOM Nmap NULL Scan Detected</b> firing against the live scan, classified as an Attempted Information Leak</em>
</p>

### Step 5 — Document the detection rationale ✅

Each rule was documented with the threat scenario, the exact traffic characteristic matched, and any adjustment made after the first test — so the signature is self-explanatory to anyone reviewing it later.

<p align="center">
  <img src="screenshots/Exhibit3_rule_explanation_document.png" alt="Exhibit 3 - Rule explanation document" width="850"><br>
  <em>Exhibit 3 — Written rule-explanation report covering threat scenario, traffic characteristic matched, and technical adjustments applied during testing</em>
</p>

### Step 6 — Reload the corrected rule into a running sensor ✅

```bash
sudo nano /etc/suricata/rules/local.rules
sudo suricatasc -c reload-rules
```

<p align="center">
  <img src="screenshots/Exhibit4_live_rule_reload_confirmation.png" alt="Exhibit 4 - Live rule reload confirmation" width="850"><br>
  <em>Exhibit 4 — Live rule reload via the Suricata socket control interface, confirming <code>{"message":"done","return":"OK"}</code> with no reload errors</em>
</p>

🎯 **Result:** The signature was corrected and pushed into a live sensor without a single service restart — an operationally significant distinction, since restarting a network sensor even briefly creates a genuine blind window in a production SOC.

| Check | Method | Outcome |
|---|---|---|
| Signature fires on real traffic | `fast.log` after live scan | ✅ Confirmed |
| Reload applied without downtime | `suricatasc -c reload-rules` | ✅ Confirmed, no restart |
| Rationale documented | Written explanation report | ✅ Confirmed |

---

<a id="mitre-mapping"></a>
## 🎯 MITRE ATT&CK Mapping

| Signature | Detects | Technique | Tactic |
|:---:|---|---|---|
| `sid:9000001` | TCP NULL scan (all control flags cleared) | [T1046](https://attack.mitre.org/techniques/T1046/) — Network Service Discovery | Discovery |

A NULL scan is reconnaissance, not exploitation — the technique maps to the Discovery tactic because the attacker is enumerating live services and port state before deciding where to focus a follow-on attack.

---

<a id="project-summary"></a>
## 📝 Project Summary

| Module | Tooling | Key Finding |
|---|---|---|
| Signature Authoring & Iteration | `suricata-update`, `local.rules` | Bitmask form (`flags:0`) fired reliably where a negated flag list did not |
| Live Verification & Reload | `nmap -sN`, `fast.log`, `suricatasc` | Real scan confirmed detected; corrected rule pushed live with zero downtime |

---

<a id="challenges-fixes"></a>
## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| The negated flag list (`flags:!FSRPAU`) looked more precise but did not reliably fire against real scan traffic | Diagnosed against live traffic and corrected to the simpler bitmask form (`flags:0`) |
| A full sensor restart would create a capture blind window while testing corrections | Used the Suricata socket control interface (`suricatasc reload-rules`) to push changes into a running sensor |

---

<a id="scope-limitations"></a>
## 🚧 Scope & Limitations

- **Single scan type:** This signature targets the NULL scan flag pattern specifically. Other stealth scan types (FIN, Xmas) would need their own signatures with different flag matches.
- **IDS mode, not IPS:** The sensor observes and logs matching traffic; it does not block the scan itself.
- **Lab-generated traffic only:** Verification is against a controlled `nmap -sN` run in the lab, not production network noise.

---

<a id="what-i-learned"></a>
## 🧠 What I Learned

- **Syntax that looks more precise is not automatically more correct.** The negated flag list was a reasonable first instinct, but the plain bitmask form is what the engine actually matched reliably against real traffic.
- **A signature is only proven by generating the real attack it targets.** Reading the rule syntax back to confirm it "looks right" is not a substitute for triggering it.
- **Live reload is an operational skill, not just a convenience.** Pushing a correction into a running sensor without a restart avoids creating the exact blind window a network IDS exists to eliminate.

---

<a id="skills-demonstrated"></a>
## 🛠️ Skills Demonstrated

- Authoring Suricata detection signatures from a raw threat scenario
- Diagnosing a non-firing rule against real triggered traffic rather than assuming syntax correctness
- Using the Suricata socket control interface for live rule reloads
- Mapping a reconnaissance-stage detection to its correct MITRE ATT&CK tactic
- Documenting rule rationale for future review, not just the final working syntax

---

<a id="screenshot-index"></a>
## 🖼️ Screenshot Index

| # | File | Shows |
|:---:|---|---|
| 1 | `Exhibit1_suricata_update_clean_run.png` | Clean `suricata-update` run, checksum verified |
| 2 | `Exhibit2_nmap_null_scan_alert_firing.png` | `fast.log` confirming the signature firing on a real scan |
| 3 | `Exhibit3_rule_explanation_document.png` | Written rationale covering threat scenario and adjustments |
| 4 | `Exhibit4_live_rule_reload_confirmation.png` | Live rule reload via `suricatasc`, no restart required |

---

<a id="repo-structure"></a>
## 📁 Repo Structure

```text
project-07-port-scan-detection-lab/
|-- README.md
|-- INDEX.md
`-- screenshots/
    |-- Exhibit1_suricata_update_clean_run.png
    |-- Exhibit2_nmap_null_scan_alert_firing.png
    |-- Exhibit3_rule_explanation_document.png
    `-- Exhibit4_live_rule_reload_confirmation.png
```

<div align="center">

🔍 **[Suricata](https://suricata.io)** · 🐧 **[Nmap](https://nmap.org)** · 🎯 **[MITRE ATT&CK](https://attack.mitre.org)** · 🔄 **[Detection Pipeline](#detection-pipeline)**

</div>
