# 01 — Getting Started

> Dense summary based on the LabEx *Getting Started* module. This note consolidates the essentials, adds practical commands you can run in Kali (VirtualBox), and captures my takeaways. Subtopics included here: **Linux History, Choosing a Linux Distribution, Debian, Red Hat Enterprise Linux (RHEL), Ubuntu, Fedora, Linux Mint, Gentoo, Arch Linux, openSUSE**.

---

## Quick Explanations

### Linux History
- UNIX (1969) → GNU project → missing kernel → **Linux kernel (1991)** completed the free OS stack. The kernel mediates hardware ↔ software and manages CPU, memory, and devices. 

### Choosing a Distribution
- A **distribution (distro)** = Linux kernel + userland + package manager + desktop environment. Pick by goals, experience, package system, and support/community. Test live ISOs before installing. 

### Family Snapshots
- **Debian**: stability-first; `apt` and huge repositories; basis for many distros. 
- **RHEL**: enterprise support, long life cycles; RPM + `dnf`/`yum`; Fedora upstream, CentOS Stream for development. 
- **Ubuntu**: Debian-based, GNOME desktop, beginner-friendly. 
- **Fedora**: fast-moving, Red Hat–backed, `dnf`. 
- **Linux Mint**: Ubuntu-based, Cinnamon desktop, strong out-of-box UX. 
- **Gentoo**: source-based; Portage, USE flags; maximum customization. 
- **Arch Linux**: minimalist, rolling release; `pacman`.  
- **openSUSE**: Leap (stable) & Tumbleweed (rolling); YaST; `zypper`.  

---

## Command Examples

> Run these on any Linux; Debian-based equivalents highlighted for Kali.

### Identify System & Kernel
```bash
uname -r            # kernel version
uname -a            # full kernel and system info
cat /etc/os-release # distro identification (works on most distros)
lsb_release -a      # Debian/Ubuntu/Mint (package: lsb-release)
```

### Package Managers by Family
```bash
# Debian / Ubuntu / Mint / Kali
sudo apt update && sudo apt upgrade -y
sudo apt install htop curl git -y

# RHEL / Fedora (DNF)
sudo dnf check-update && sudo dnf upgrade -y
sudo dnf install htop curl git -y

# Arch
sudo pacman -Syu --noconfirm htop curl git

# openSUSE
sudo zypper refresh && sudo zypper update -y
sudo zypper install -y htop curl git

# Gentoo
sudo emerge --sync
sudo emerge --ask app-admin/htop net-misc/curl dev-vcs/git
```

### Hardware & Storage Quick Checks
```bash
lscpu           # CPU architecture summary
lsblk -f        # block devices & filesystems
free -h         # memory usage
sudo fdisk -l   # list disks/partitions (needs sudo)
```

---

## My Kali Linux Practice (VirtualBox)
- Verified distro & kernel with `cat /etc/os-release` and `uname -r`.
- Updated system with `sudo apt update && sudo apt upgrade`.
- Installed essentials: `git`, `curl`, `htop`; confirmed versions with `--version` flags.
- Snapshot in VirtualBox before/after major changes to keep states reproducible.
- Compared apt vs. other managers conceptually; recorded commands above as a cross-distro reference.

---

## LabEx Conclusions (What Matters)
- Linux is a **kernel**; a **distro** packages the kernel with userland, PM, and UX. 
- Choose a distro by **stability vs. freshness**, package ecosystem, and support. Try **Live USB/VM** first.
- Different families = different package managers; learn one well, be aware of others.
