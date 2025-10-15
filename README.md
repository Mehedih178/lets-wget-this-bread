# 🧠 Linux Auditd File Monitoring — "Let's wget This Bread"

> A forensic-style mini project that demonstrates how to track unauthorized file modifications in Linux using the `auditd` daemon.

---

## 📸 Project Overview

This project monitors a protected directory (`/protected_files`) using **Linux Auditd**, detects file changes made by custom attack scripts, and maps which attack modified which file.  
It’s a practical example of **host-based intrusion detection** and **file integrity monitoring**.

---

## ⚙️ Features
✅ Custom audit rules for `/protected_files`  
✅ Attack simulations (`attack-a`, `attack-b`, `attack-c`)  
✅ Log filtering with `ausearch`  
✅ Real findings summary (file ↔ attack mappings)  
✅ Reflection and analysis  

---

## 🧰 Tools & Commands Used
| Tool | Purpose |
|------|----------|
| `auditd` | Logs file access and write operations |
| `auditctl` | Manages audit rules |
| `ausearch` | Searches and filters audit logs |
| `chmod`, `wget`, `unzip` | File permissions and setup |

---

## 🧩 Process Overview

```mermaid
flowchart TD
    A[Setup Auditd] --> B[Add Rules for /protected_files]
    B --> C[Run Attack Scripts]
    C --> D[Logs Captured by Auditd]
    D --> E[Filter with ausearch]
    E --> F[Identify Modified Files]
    F --> G[Summarize Findings]
