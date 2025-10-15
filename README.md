# Let's wget This Bread — Mehedi's Project 2

This repository documents my Project 2: using the Linux **auditd** daemon to monitor a protected directory (`/protected_files`), run attack scripts that modify files there, and use audit log analysis to determine which attack modified which file.

## Objective
- Configure auditd rules to watch 10 files in `/protected_files` for write/attribute changes.
- Run the three provided attack scripts (`attack-a`, `attack-b`, `attack-c`).
- Use `ausearch` to identify which file each attack modified.
- Record findings in `findings_summary.txt`.

## Quick setup (commands to run on the VM)
```bash
# from your home directory
wget https://github.com/Mehedih178/lets-wget-this-bread/archive/main.zip
unzip main.zip
cd lets-wget-this-bread   # or to the folder where the attack files are

# make attacks executable
chmod u+x attack-a attack-b attack-c

# copy example audit.rules into /etc/audit/rules.d/ (requires sudo)
sudo cp audit.rules /etc/audit/rules.d/lets-wget-this-bread.rules

# restart auditd to apply rules
sudo systemctl restart auditd

# verify rules are loaded
sudo auditctl -l
