# 06 — Permissions 

A clean, structured summary of the **Permissions** module from Linux Journey. This note explains Unix permission bits, ownership, special modes (SUID/SGID/sticky), umask, and process UIDs — with practical commands you can run in Kali (VirtualBox). 

---

## Quick Explanations

### 1) Reading Permission Strings
- `ls -l` shows a **type** + 9 permission characters: e.g., `drwxr-xr-x`. The leading letter indicates file type (`-` file, `d` directory). Then triplets for **user**, **group**, **others** with `r` (read), `w` (write), `x` (execute), or `-` (no permission). Execute on a **directory** means you can *enter/traverse* it.  

### 2) Changing Permissions — `chmod`
- **Symbolic**: target = `u` (user),  `g` (group),  `o` (others),  `a` (all);   operation `+` add,   `-` remove.   Examples: `chmod u+x file`,  `chmod g-w file`, `chmod ug+w file`.  
- **Octal**: `r=4`, `w=2`, `x=1`. Combine per class. Example: `chmod 755 file` → user `rwx`, group `r-x`, others `r-x`. Avoid reckless recursive `777`; use least‑privilege.  

### 3) Ownership — `chown` / `chgrp`
- Each file has an **owner** (user) and **group**. Change owner: `sudo chown patty file`. Change group: `sudo chgrp whales file`. Both at once: `sudo chown patty:whales file`.  

### 4) umask (Default Permissions)
- `umask` subtracts bits from the default creation perms. Common default: `022` (group/others cannot write). Persist by adding to a shell startup file (e.g., `.profile`/`.bashrc`).  

### 5) SUID (setuid)
- Special bit that makes a program run with the **owner’s** effective UID. Example: `/usr/bin/passwd` is `-rwsr-xr-x` so it can safely update `/etc/shadow` as root. Set with `chmod u+s file` or octal `chmod 4755 file`. Uppercase `S` indicates missing execute on user.  

### 6) SGID (setgid)
- Similar for **group**; program runs with the file’s group. Example: `-rwxr-sr-x` shows SGID in the group slot. Set with `chmod g+s file` or octal `2555`.  

### 7) Process UIDs
- Processes carry multiple IDs: **real UID** (who launched), **effective UID** (permissions used for access checks), and **saved UID** (allows toggling between real/effective). SUID programs elevate effective UID only for the operations that require it.  

### 8) Sticky Bit
- On **directories**, sticky (`t`) allows only the file owner, directory owner, or root to delete/rename files within (classic example: `/tmp` with `rwxrwxrwt`). Set via `chmod +t dir` or octal `1` prefix: `chmod 1755 dir`.  

---

## Command Examples

### Inspect Permissions & Ownership
```bash
ls -l
namei -l some/path        # optional: shows per-component perms if installed
stat file                  # detailed metadata including mode and owner
```

### Change Mode (Symbolic & Octal)
```bash
chmod u+x script.sh
chmod g-w notes.txt
chmod 640 secrets.txt      # rw- r-- ---
chmod 755 tool             # rwx r-x r-x
```

### Change Ownership
```bash
sudo chown patty file
sudo chgrp whales file
sudo chown patty:whales file
```

### Special Bits & umask
```bash
# SUID / SGID / Sticky
touch prog && chmod 4755 prog   # setuid
chmod 2555 prog                  # setgid
mkdir shared && chmod 1777 shared# sticky (like /tmp)

# Default creation mask
umask            # display current
umask 022        # typical restrictive default
```

### Practical Safety Checks
```bash
# Show effective identity for a running command
id

# Verify privileged program bits
ls -l /usr/bin/passwd    # expect: -rwsr-xr-x
ls -ld /tmp              # expect: ...t at end
```

---

## My Kali Linux Practice (VirtualBox)
- Listed files with `ls -l` to interpret type and triplet permissions; compared behavior on files vs directories.  
- Adjusted permissions using both symbolic and octal forms; validated results with `stat`.  
- Changed ownership with `chown`, `chgrp`, and combined `chown user:group`.  
- Experimented with `umask` and confirmed default creation modes by creating test files/dirs.  
- Observed SUID/SGID behavior (e.g., `/usr/bin/passwd`) and confirmed sticky bit on `/tmp`.  

---

## LabEx Conclusions
- Permissions (r/w/x), ownership, and special bits (SUID/SGID/sticky) form the **access‑control core** of Linux. Use least privilege and auditable elevation.  
- Defaults matter: understand `umask` and process UIDs so elevated rights are used **only** when necessary.  
