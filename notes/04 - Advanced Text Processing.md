# 04 — Advanced Text Processing (LabEx: Advanced Text‑Fu)

A polished, structured summary of the **Advanced Text‑Fu** module from Linux Journey. This section builds on core text manipulation and introduces powerful pattern‑matching and text‑editing tools like regex and advanced editors (Vim & Emacs).

---

## Quick Explanations

### 1. Regular Expressions (regex)
- Regex provides **pattern‑based matching**, enabling precise text selection and filtering.  
- Anchors:
  - `^pattern` → match at line start
  - `pattern$` → match at line end
- Wildcards:
  - `.` → any single character
- Character sets:
  - `[ae]` → match a or e
  - `[^e]` → match NOT e
  - `[a-c]` → match a range
- Regex is widely used in tools like `grep`, `sed`, `awk`, Vim, and programming languages.

### 2. Text Editors Overview
- Two legendary CLI editors dominate Linux: **Vim** and **Emacs**.  
- Both support deep customization, efficient workflows, and powerful editing modes.
- Choosing one is mostly preference — both are essential tools in server and terminal environments.

### 3. Vim (Vi Improved)
- Vim is a fast, lightweight, and ubiquitous editor designed for keyboard‑driven text manipulation.  
- Start Vim: `vim`
- Open a file: `vim file.txt`
- Features include syntax highlighting, undo levels, motions, operators, and plugins.

### 4. Vim Search Patterns
- `/pattern` → search forward.  
- `?pattern` → search backward.
- `n` → next match; `N` → previous match.
- Efficient search is essential for navigating large files.

### 5. Vim Navigation
- Cursor movement keys (in Normal mode):
  - `h` left
  - `j` down
  - `k` up
  - `l` right
- All motion is designed around keeping your hands on the keyboard.  

### 6. Vim Inserting & Appending
- Switch to Insert mode: `i`, `a`, `I`, `A`.  
- Open new lines:
  - `o` (below)
  - `O` (above)
- Insert vs Append distinctions help you type efficiently at any position.

### 7. Vim Editing Operations
- Vim editing is based on **operator + motion**. Examples:  
  - `dw` → delete word
  - `2dd` → delete two lines
  - `cw` → change word
  - `yy` → yank (copy) line
  - `p` / `P` → paste
- Advanced tools:
  - `r{char}` → replace one character
  - `R` → replace mode
  - `J` → join lines
  - `.` → repeat last action

### 8. Vim Saving & Exiting
- Save: `:w`
- Quit: `:q`
- Save & quit: `:wq` or `ZZ`  
- Force quit (discard changes): `:q!`
- Undo/redo: `u`, `Ctrl+r`

### 9. Emacs Overview
- Emacs is a powerful, highly extensible editor — often described as *an OS inside an editor*.  
- Start: `emacs`
- Files open in **buffers**, which you can switch and manage dynamically.

### 10. Emacs File Operations
- Save: `C-x C-s`
- Save as: `C-x C-w`
- Save all: `C-x s`
- Open file: `C-x C-f` citeturn24search1

### 11. Emacs Buffer Navigation
- Switch buffers: `C-x b`
- Cycle buffers: `C-x` + arrow keys
- Split window: `C-x 2`
- Move between windows: `C-x o`
- Close other windows: `C-x 1`
- Kill buffer: `C-x k`

### 12. Emacs Editing
- Navigation:
  - `C-left/right` → move by words
  - `C-up/down` → move by paragraphs
  - `M->` → end of buffer
- Selection: `C-space`, then move cursor
- Cut: `C-w`
- Paste: `C-y`

---

## Command Examples

### Regex
```bash
grep '^error' logfile.txt
grep 'end$' report.txt
grep 's[ae]lls' text.txt
grep '[^0-9]' data.txt
```

### Vim Essentials
```bash
vim file.txt
/keyword
n
cw            # change word
yy            # yank line
p             # paste
:wq
```

### Emacs Essentials
```bash
emacs file.txt
# In Emacs:
# C-x C-s (save)
# C-x C-f (open)
# C-x b (switch buffer)
```

---

## My Kali Linux Practice (VirtualBox)
- Practiced regex matching with `grep` on logs and sample text.
- Navigated and edited files in Vim: insertion, deletion, yanking, and search operations.
- Experimented with Emacs buffers, windows, and basic editing.
- Created quick workflows combining regex + editors for efficient text manipulation.

---

## LabEx Conclusions
- Regex provides unmatched power for pattern detection and filtering.  
- Vim and Emacs form the backbone of advanced text‑editing workflows in Linux.  
- Understanding these tools dramatically improves speed and efficiency when working in terminal‑based environments.  
