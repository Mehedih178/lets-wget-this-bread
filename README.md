# 🧠 CodePath CYB102 - Week 2 Project 2: Let's wget This Bread

This repository documents **Project 2** from CodePath’s CYB102 course, where we use the **Linux Audit Daemon (auditd)** to monitor filesystem changes in a protected directory and identify which attack scripts modify which files.

---

## 🚀 Objective
The goal of this project is to:
- Set up custom **auditd rules** to monitor file changes in `/protected_files`
- Run **three attack scripts** (`attack-a`, `attack-b`, and `attack-c`)
- Use `ausearch` to filter logs and identify which files were altered by which attack

---

## 🧩 Tasks Summary

| Step | Task | Command / Notes |
|------|------|-----------------|
| 1 | Download starter repo | `wget https://github.com/codepath/project2/archive/main.zip` |
| 2 | Unzip contents | `unzip main.zip && cd project2-main` |
| 3 | Make attacks executable | `chmod u+x attack-a attack-b attack-c` |
| 4 | Configure auditd rules | Watch `/protected_files` for write activity |
| 5 | Run attacks | `./attack-a`, `./attack-b`, `./attack-c` |
| 6 | Analyze logs | `ausearch -k <filter_key>` |
| 7 | Identify modified files | Note file paths and corresponding attack scripts |

---

## ⚙️ Example Audit Rules (audit.rules)
```bash
-w /protected_files/file1.txt -p wa -k file1_watch
-w /protected_files/file2.txt -p wa -k file2_watch
...
-w /protected_files/file10.txt -p wa -k file10_watch
