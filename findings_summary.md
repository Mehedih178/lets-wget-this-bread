# 🧠 Finding Summary — lets-wget-this-bread

## Project Overview
This is a mini forensic / security demonstration project that uses **Linux `auditd`** to monitor and detect unauthorized modifications in a protected directory.

**Repository highlights**
- `protected_files/` — files monitored for modifications  
- `attack-a/`, `attack-b/`, `attack-c/` — scripts used to simulate modifications (attacks)  
- `README.md` — setup and procedure instructions  

**Goal:** simulate attacks, capture audit logs, and map which attack modified which file.

---

## Key Components & Workflow

| Component | Purpose |
|---|---|
| `auditd` | Linux auditing daemon that logs system events (file operations) |
| `auditctl` | Tool to add/list/remove audit rules |
| `ausearch` | Tool to query/filter audit logs |
| `protected_files/` | Directory being monitored for file modifications |
| `attack-a`, `attack-b`, `attack-c` | Scripts that perform modifications to demonstrate detection |
| Custom audit rules | Watch `protected_files` for write/attribute events and tag logs with a key |

### Typical Workflow
1. Install and enable `auditd`.  
2. Add audit rules targeting `protected_files`.  
3. Run one or more attack scripts to simulate unauthorized changes.  
4. Collect audit logs (e.g., `/var/log/audit/audit.log`).  
5. Use `ausearch` and `aureport` to isolate events and summarize findings.  
6. Correlate which script caused each file modification.

---

## Observations & Findings

- With properly configured audit rules, file writes in `/protected_files` were captured and traceable to the correct process and timestamp.  
- Using `ausearch -k protected_watch` helped filter and identify relevant log entries quickly.  
- The repository clearly demonstrates the full chain: **attack → detection → analysis**.  
- `attack-a`, `attack-b`, and `attack-c` all triggered unique logged events that confirmed `auditd`’s effectiveness in forensic tracing.

---

## ✅ Strengths

1. **Hands-on realism** — demonstrates real `auditd` monitoring behavior rather than theory.  
2. **Self-contained** — includes all components: attacks, files, and monitoring logic.  
3. **Readable** — organized structure and clear documentation.  
4. **Flexible** — can easily expand rules or simulate different attack scenarios.  
5. **Educational value** — practical intro to Linux host-based intrusion detection.

---

## ⚠️ Weaknesses, Risks & Recommendations

### Weaknesses / Risks
- **Noise / false positives:** Broad rules may capture harmless events.  
- **Performance overhead:** Monitoring large directories increases resource usage.  
- **Limited scope:** Focuses only on file-level attacks, not network or kernel persistence.  
- **No log tampering simulation:** Does not test resilience against attackers modifying logs.  
- **Rule persistence:** Audit rules reset unless saved using `augenrules`.

### Recommendations / Improvements
- Expand to include more syscall types like `rename`, `unlink`, and `chmod`.  
- Automate rule setup with a `setup-audit.sh` script.  
- Add a `collect-findings.sh` to export logs into `.csv` or `.md`.  
- Configure remote log forwarding to prevent local log tampering.  
- Include rule persistence in `/etc/audit/rules.d/` and use `augenrules --load`.  
- Add a “performance impact” section with `top` or `pidstat` metrics during monitoring.

---

## 🧾 Audit Rules Used

Below are the audit rules used to detect and log file modifications in `/protected_files`.

### Temporary Rules (runtime only)
```bash
# Monitor writes and attribute changes in /protected_files
sudo auditctl -w /protected_files -p wa -k protected_watch



📎 Summary
This project successfully demonstrates how Linux auditd can be configured to detect and log unauthorized file modifications.
Through carefully applied rules, simulated attacks, and log filtering, each event was captured and verified, proving auditd’s value for forensic analysis and system hardening.
