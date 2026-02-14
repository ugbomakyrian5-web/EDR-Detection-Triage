# 🛡 EDR Lab Project: Detection Triage & Threat Investigation

![SOC Badge](https://img.shields.io/badge/SOC-Analysis-blue?style=for-the-badge) 
![EDR Badge](https://img.shields.io/badge/EDR-Lab-green?style=for-the-badge)
![Status Badge](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 📑 Table of Contents
- [Overview](#📑-overview)  
- [Key Investigations](#🔎-key-investigations)  
  - [DESKTOP-HR01 🟥 Malicious Payload Download](#desktop-hr01-🟥-malicious-payload-download)  
  - [WIN-ENG-LAPTOP03 🟧 Suspicious Execution & Exfiltration](#win-eng-laptop03-🟧-suspicious-execution--exfiltration)  
  - [DESKTOP-DEV01 🟩 Benign / False Positive](#desktop-dev01-🟩-benign--false-positive)  
- [Final Verdict Summary](#🚨-final-verdict-summary)  
- [Evidence](#📸-evidence)  
- [MITRE ATT&CK Mapping](#🧠-mitre-attck-mapping-interactive)  
- [Key Takeaways](#📌-key-takeaways)  

---

## 📑 Overview
This lab demonstrates **EDR-based endpoint detection triage**, focusing on:  

- ⚡ Threat identification and process lineage  
- 🔍 Absolute path analysis of suspicious binaries  
- 🌐 Validation using internal and external threat intelligence  
- 📝 Structured SOC documentation  

> **Scope:** Analysis only; containment/remediation excluded.

---

## 🔎 Key Investigations

<details>
<summary>DESKTOP-HR01 🟥 Malicious Payload Download</summary>

- **🛠 Tool:** CMD.exe → CURL.exe  
- **📂 File:** install.exe  
- **📁 Absolute Path:** `C:\Users\Public\install.exe`  
- **⚠️ Indicators:** Command-line payload retrieval, writable directory, generic filename  
- **✅ Verdict:** High-confidence malicious download  

</details>

<details>
<summary>WIN-ENG-LAPTOP03 🟧 Suspicious Execution & Exfiltration</summary>

- **🛠 Tool:** syncsvc.exe (masquerading as a sync service)  
- **📁 Path:** `C:\Users\haris.khan\AppData\Local\Temp\syncsvc.exe`  
- **🌐 Exfiltration URL:** https://files-wetransfer.com/upload/session/ab12cd34ef56/dump_2025.dmp  
- **⚠️ Indicators:** Execution from Temp, memory dump exposure, web-based exfiltration  
- **✅ Verdict:** Medium-high confidence; probable data exfiltration  

</details>

<details>
<summary>DESKTOP-DEV01 🟩 Benign / False Positive</summary>

- **🛠 Tool:** UpdateAgent.exe (internal IT utility)  
- **⚠️ Indicators:** Verified via threat intelligence; no anomalous behavior  
- **✅ Verdict:** Benign / False Positive  

</details>

---

### 🚨 Final Verdict Summary
| Host | Verdict | Status |
|------|---------|--------|
| DESKTOP-HR01 | Malicious Payload Download | 🟥 High Risk |
| WIN-ENG-LAPTOP03 | Suspicious Execution & Exfiltration | 🟧 Medium Risk |
| DESKTOP-DEV01 | Benign / False Positive | 🟩 Low Risk |

---

## 📸 Evidence

### EDR Process Tree
<img src="https://i.imgur.com/FOWfpyi.png" alt="EDR Process Tree" width="800px">

### Exfiltration Attempt
<img src="https://i.imgur.com/25gfkrX.png" alt="Exfiltration Attempt" width="800px">

### Suspicious File Activity
<img src="https://i.imgur.com/lHFQAh9.png" alt="Suspicious File Activity" width="800px">

### Additional Artifact
<img src="https://i.imgur.com/p3ApPTZ.png" alt="Additional Artifact" width="800px">

---

<details>
<summary>🧠 MITRE ATT&CK Mapping (Interactive)</summary>

| Tactic | Technique | ID | Notes |
|--------|-----------|----|-------|
| 🖥 Execution | Command and Scripting Interpreter | T1059 | CMD.exe → CURL.exe download activity |
| 🌐 Command & Control | Ingress Tool Transfer | T1105 | Payload retrieved from external server |
| 📤 Exfiltration | Exfiltration Over Web Service | T1567 | Memory dump uploaded via web service |
| 🕵️‍♂️ Defense Evasion | Masquerading | T1036 | syncsvc.exe mimics legitimate service |

> 💡 **Tip:** Each colored icon represents a MITRE tactic category:  
> - 🖥 Execution  
> - 🌐 Command & Control  
> - 📤 Exfiltration  
> - 🕵️‍♂️ Defense Evasion

</details>

---

<details>
<summary>📌 Key Takeaways</summary>

- 🛡 Legitimate tools (e.g., CURL) can be weaponized for malware staging  
- ⚡ Execution from writable directories is a strong compromise indicator  
- 🌐 Web-based file transfers are common exfiltration vectors  
- 🧠 Threat intelligence validation reduces false positives  

</details>


</details>
