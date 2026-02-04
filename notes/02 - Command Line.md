# 02 — Command Line

A clean, structured summary of the **Command Line** module from the Linux Journey course. This file includes clear explanations, practical examples you can run in Kali Linux (VirtualBox), and concise takeaways for each subtopic.  

---

## Quick Explanations

### 1. The Shell
- The **Linux shell** is a program that interprets your commands and communicates them to the OS. Terminal apps simply open a shell session.  
- **Bash** (Bourne Again SHell) is the default shell in most Linux distros.
- The shell prompt typically appears as: `username@hostname:directory$`. The `$` symbol indicates a regular user prompt.  

### 2. pwd (Print Working Directory)
- Linux uses a hierarchical filesystem starting at `/` (root).  
- `pwd` prints your **absolute current directory path**, helping you understand exactly where you are in the filesystem.  

### 3. cd (Change Directory)
- Paths can be **absolute** (starting with `/`) or **relative** (from your current location).  
- Navigation shortcuts:
  - `.` → current directory
  - `..` → parent directory
  - `~` → home directory
  - `-` → previous directory

### 4. ls (List Directory)
- `ls` shows files/directories in the current or specified path.  
- Useful flags:
  - `-a` → show hidden files
  - `-l` → long, detailed listing
  - `-r` → reverse order
  - Combined: `ls -la`, `ls -lar`, etc.

### 5. touch
- Creates an empty file or updates the timestamp of an existing one.  
- Supports advanced timestamp control via `-r` (reference file) and `-d` (specific date).  

### 6. file
- Identifies a file’s true type regardless of filename extension. Example: `file banana.jpg`.  

### 7. cat
- Displays file contents, concatenates files, or creates files via redirection (`>`).  
- Supports `-n` (number lines) and `-b` (number non-blank lines).

### 8. less
- Allows page-by-page file viewing for large files. Includes searching (`/term`, `?term`) and navigation (`g`, `G`, arrow keys).  

### 9. history
- Shows recently executed commands; enables re-running via arrows, `!!`, and reverse search (`Ctrl+R`).  
- Manage history with `history -c`, `history -w`, and `history -d N`.

### 10. cp (Copy)
- Copies files and directories.
- Useful flags:
  - `-r` → recursive (needed for directories)
  - `-i` → interactive
  - `-f` → force
  - `-p` → preserve timestamps & metadata  

### 11. mv (Move/Rename)
- Moves or renames files/directories.
- Useful flags: `-i` (interactive), `-b` (backup), `-v` (verbose).  

### 12. mkdir (Make Directory)
- Creates one or multiple directories.
- `-p` allows creating nested directories without errors.  

### 13. rm (Remove)
- Deletes files permanently (no trash). Use with extreme caution.  
- Dangerous combo: `rm -rf` recursively and forcefully removes everything.
- `-i` adds safety prompts; `-f` forces removal.
- `rmdir` removes empty directories only.

### 14. find
- Searches directories recursively for files by name, type, etc. Example: `find /home -name file.txt`.  

### 15. help
- `help` shows usage details for Bash built-in commands.
- Many executables support `--help` for quick usage info.  

### 16. man
- Opens detailed manual pages for commands. Example: `man ls`. Quit with `q`.  

### 17. whatis
- Shows a one‑line summary of a command from its man page. Example: `whatis cat`.  

### 18. alias
- Creates shortcuts for long/repeated commands.
- Temporary: `alias ll='ls -la'`
- Permanent: Add alias to `~/.bashrc` and reload with `source ~/.bashrc`.  

---

## Command Examples

### Basic Shell Navigation
```bash
pwd
cd /home
cd ..
cd ~
ls -la
```

### File Creation & Viewing
```bash
touch notes.txt
file notes.txt
cat notes.txt
less /etc/passwd
```

### Working with Files
```bash
cp file1.txt ~/Documents/
mv oldname.txt newname.txt
rm -i unused.txt
mkdir -p projects/linux/scripts
```

### Searching & Help
```bash
find /home -type f -name "*.log"
history
man cp
whatis grep
```

### Aliases
```bash
alias ll='ls -la'
source ~/.bashrc
```

---

## My Kali Linux Practice (VirtualBox)
- Verified shell environment and prompt behavior.
- Practiced path navigation using absolute & relative paths.
- Explored `ls` flags: `-a`, `-l`, and combined variations.
- Created and removed test files/directories with `touch`, `mkdir`, and `rm -i`.
- Used `find` to locate logs and config files.
- Added simple aliases to `~/.bashrc` and reloaded configuration.

---

## LabEx Conclusions
- Shell fundamentals build the core of Linux proficiency.  
- File navigation, inspection, and manipulation form the foundation for scripting and advanced topics.  
- Learning built-in help systems (`help`, `man`, `--help`) ensures self-sufficiency while exploring Linux.  
