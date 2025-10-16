# Finding Summary — lets-wget-this-bread

## Project Overview
This is a mini forensic / security demonstration project that uses **Linux `auditd`** to monitor and detect unauthorized modifications in a protected directory.

**Repository highlights**
- `protected_files/` — files monitored for modifications  
- `attack-a/`, `attack-b/`, `attack-c/` — scripts used to simulate modifications (attacks)  
- `README.md` — setup and procedure instructions

**Goal:** simulate attacks, capture audit logs, then map which attack modified which file.

---

## Key Components & Workflow

| Component | Purpose |
|---|---|
| `auditd` | Linux auditing daemon that logs system events (file operations) |
| `auditctl` | Tool to add/list/remove audit rules |
| `ausearch` | Tool to query/filter audit logs |
| `protected_files/` | Directory being monitored for file modifications |
| `attack-a`, `attack-b`, `attack-c` | Scripts that perform modifications to demonstrate detection |
| Audit rules (custom) | Watch `protected_files` for write/attribute events and tag logs with a key |

**Typical workflow**
1. Install/enable `auditd` and add audit rules targeting `protected_files`.  
2. Run one or more attack scripts to simulate unauthorized activity.  
3. Collect audit logs (e.g., `/var/log/audit/audit.log`).  
4. Use `ausearch` (filter by rule key, path, syscall, or time) to find relevant events.  
5. Map the findings — which attack script / process modified which file and when.

---

## Observations & Findings

- With properly configured audit rules, file writes in the targeted directory are captured and traceable to a process and timestamp.  
- Logs can be verbose; `ausearch` filters (by key/path/event) are essential to isolate meaningful events.  
- The repo demonstrates the attack → logging → detection chain clearly and compactly, making it a good learning tool.

---

## Strengths

1. **Practical & hands-on** — demonstrates real `auditd` behavior rather than theory.  
2. **Self-contained** — attacks, files, and detection steps live in the same repo.  
3. **Readable** — clear structure and an approachable README.  
4. **Extensible** — attack scripts and rules can be swapped or expanded for testing.

---

## Weaknesses, Risks & Recommendations

**Weaknesses / Risks**
- **Noise / false positives:** Host systems produce many file events; overly-broad rules cause alert fatigue.  
- **Performance overhead:** Monitoring many files or broad syscalls can impact performance.  
- **Limited scope:** Host-based file auditing doesn’t cover network-based attacks or non-file-based persistence.  
- **Log tampering not covered:** Advanced attackers may try to modify or delete logs; this demo doesn't simulate that.  
- **Rule persistence:** Audit rules need to be persisted (e.g., `augenrules`) to survive reboots — confirm repo covers this.

**Recommendations / Improvements**
- Monitor additional event types (rename, unlink/delete, attribute changes) not just writes.  
- Add automated rule in
