# 05 — User & Group Management  

A clean, structured summary of the **User Management** module from Linux Journey. This note covers users, groups, the superuser model, key account databases, and essential CLI tools.  

---

## Quick Explanations

### 1) Users & Groups
- Linux is multi‑user. Each user has a UID, a primary group (GID), and typically a home directory at `/home/<username>`.
- Groups collect users to simplify permission management.  
- **root** is the superuser with unrestricted access
- regular users elevate via `sudo` when permitted.  

### 2) root, `sudo`, and `su`
- **sudo** runs a single command with elevated privileges and logs actions to your user — safer than a persistent root shell.  
- **su** substitutes user identity (e.g., `su -` for a root login shell) but increases risk if left open.
- Prefer `sudo` for auditable, limited elevation.  
- Authorization is controlled by **`/etc/sudoers`**; edit safely with `visudo`.  

### 3) `/etc/passwd`
- World‑readable map of **username → UID, GID, GECOS, home, login shell**
- the password field is usually `x` (actual hashes live in `/etc/shadow`).  
- Contains system accounts for services (not just human users).
- Modify via tools (`useradd`, `usermod`) rather than manual edits.  

### 4) `/etc/shadow`
- Root‑readable file with **password hashes** and aging policy
- last change, min/max age, warning, inactivity, expiry.
- Locking often appears as `*`/`!` in the password field.  

### 5) `/etc/group`
- Lists groups and members: **group name**, **password placeholder**, **GID**, **comma‑separated user list**.  

### 6) Core User Management Tools
- `useradd` / `userdel` (with `-r` to remove home) — create/remove accounts.  
- `usermod` — change shell, groups, home, etc. (implied by module context).  
- `passwd` — set or change passwords (self or, as root, others).  

---

## Command Examples

### Inspect Accounts & Privileges
```bash
# Who am I and what groups am I in?
id
whoami

# View account databases (read‑only examples)
cat /etc/passwd | head
sudo cat /etc/shadow | head
cat /etc/group | head

# Test protected file access
cat /etc/shadow            # expect: Permission denied
sudo cat /etc/shadow       # with privileges
```

### `sudo` and `su`
```bash
# Run a single privileged command (preferred)
sudo apt update

# Open a root login shell (use sparingly)
su -

# Edit sudoers safely
sudo visudo
```

### Create / Modify / Remove Users
```bash
# Create user (uses system defaults)
sudo useradd bob
# Set password for user
sudo passwd bob

# Add to supplementary group (example: sudo)
sudo usermod -aG sudo bob

# Remove user; also remove home and mail spool
sudo userdel -r bob
```

### Useful Group Operations
```bash
# Show groups for a user
groups bob
# Add user to an existing group
sudo usermod -aG developers bob
```

---

## My Kali Linux Practice (VirtualBox)
- Reviewed real entries in `/etc/passwd`, `/etc/shadow`, and `/etc/group`; compared fields and meanings.  
- Practiced safe elevation with `sudo`, avoided persistent `su` shells; used `visudo` to understand sudo policy.  
- Created a test user, set a password, added to groups, and removed the account with home cleanup.  

---

## LabEx Conclusions
- Separate identity (UID/GID) from permissions via groups; elevate minimally with `sudo` for safety and auditability.  
- System databases `/etc/passwd`, `/etc/shadow`, and `/etc/group` underpin all account operations — manage them **via tools**, not manual edits.  
