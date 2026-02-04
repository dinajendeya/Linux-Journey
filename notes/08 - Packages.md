# 08 — Packages 

A clean, structured summary of the **Packages** module from Linux Journey. This note covers package concepts, repositories, archives & compression (tar/gzip), dependencies, low‑level tools (`dpkg`/`rpm`), high‑level managers (`apt`/`yum`), and compiling from source — with practical commands you can run in Kali (VirtualBox).  

---

## Quick Explanations

### 1) Software Distribution & Package Formats
- A **package** bundles executables, configs, and docs for installation by a package manager.
- Two dominant formats: **`.deb`** (Debian/Ubuntu/Mint) and **`.rpm`** (RHEL/Fedora/CentOS).
- Package maintainers adapt upstream software for each distro.  

### 2) Package Repositories & Sources
- Repositories are curated servers of packages that your manager consults.
- Debian‑based systems use **APT sources** in `/etc/apt/sources.list` and `*.list`/`*.sources` files under `/etc/apt/sources.list.d/`.
- Third‑party vendors (e.g., Docker) provide their own repos that you can add.  

### 3) tar & gzip (Archiving vs Compression)
- **tar** *archives* multiple files into one `.tar`;
- **gzip** *compresses* a single file to `.gz`. Combined with `tar -z`, you create/extract `.tar.gz` in one step.
- Other compressors exist (`bzip2` -> `.bz2` with `-j`, `xz` -> `.xz` with `-J`).  

### 4) Package Dependencies
- Packages often depend on other packages (commonly shared libraries).
- Package managers resolve and install dependencies automatically;
- manual installs that miss deps result in **broken packages**.  

### 5) Low‑Level Tools — `dpkg` and `rpm`
- Installing local files directly: `dpkg -i file.deb` (Debian) or `rpm -i file.rpm` (RPM).
- Removal: `dpkg -r <pkg>` or `rpm -e <pkg>`.
- Listing: `dpkg -l` or `rpm -qa`.
- These tools **do not resolve dependencies**.  

### 6) High‑Level Managers — `apt` and `yum`
- APT (Debian family) and YUM (RPM family) install, update, remove packages **and** handle dependencies.
- Typical flows: `apt update && apt upgrade`, `apt install <pkg>`, `apt remove <pkg>`; on RPM systems: `yum update`, `yum install <pkg>`, `yum erase <pkg>`.
- Inspect metadata via `apt show <pkg>` or `yum info <pkg>`.  

### 7) Compiling from Source (when no package exists)
- Install build tools (`build-essential` on Debian/Ubuntu).
- Unpack source (`tar -xzvf package.tar.gz`), then **configure → make → sudo make install**.
- Prefer **`checkinstall`** to create and register a native package so it’s trackable/uninstallable by your manager.  

---

## Command Examples

### APT Sources & Updates (Debian/Ubuntu/Kali)
```bash
# View configured sources
cat /etc/apt/sources.list
ls -1 /etc/apt/sources.list.d/

# Update and upgrade
sudo apt update && sudo apt upgrade -y

# Install, remove, and inspect
sudo apt install htop
sudo apt remove htop
apt show htop
```

### RPM/YUM Basics (RHEL/Fedora/CentOS)
```bash
sudo yum update -y
sudo yum install htop -y
sudo yum erase htop -y
sudo yum info htop
```

### Local Package Files (no dependency resolution)
```bash
# Debian package
sudo dpkg -i package.deb
sudo dpkg -r packagename
sudo dpkg -l | less

# RPM package
sudo rpm -i package.rpm
sudo rpm -e packagename
rpm -qa | less
```

### tar & gzip
```bash
# Create compressed archive
tar czvf backup.tar.gz dir1 file2
# Extract
tar xzvf backup.tar.gz
# Compress/uncompress single file
gzip bigfile && gunzip bigfile.gz
```

### Build from Source (generic flow)
```bash
sudo apt install -y build-essential
 tar -xzvf foo-1.0.tar.gz && cd foo-1.0
 ./configure
 make
 sudo checkinstall   # preferred over: sudo make install
```

---

## My Kali Linux Practice (VirtualBox)
- Reviewed APT sources in `/etc/apt/sources.list` and `sources.list.d/`; added a vendor repo pattern similar to Docker’s as a dry run.  
- Practiced `apt update/upgrade`, `apt install/remove`, and `apt show` for metadata.  
- Compared low‑level (`dpkg`) vs high‑level (`apt`) behavior on dependency handling.  
- Created/extracted `.tar.gz` archives; distinguished archive vs compression roles.  
- Walked the `configure → make → checkinstall` flow to keep compiled software managed by APT.  

---

## LabEx Conclusions
- Package managers and repositories provide secure, repeatable software delivery with automatic dependency resolution; use low‑level tools only for special cases.  
- Prefer native packages (or `checkinstall`) for source builds so installs remain visible, updatable, and removable via the system’s package manager.  
