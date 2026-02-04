# 03 — File Manipulation (LabEx: Text‑Fu)

A structured, clean summary of the **Text‑Fu** module from Linux Journey. This module focuses on processing, transforming, and manipulating text streams using the Linux command line. 

---

## Quick Explanations

### 1. stdout (Standard Output)
- Commands normally send their output to the terminal (stdout).  
- `>` redirects stdout into a file **(overwrites)**.
- `>>` appends stdout to a file **(without overwriting)**.
- Example: `echo Hello > file.txt`.

### 2. stdin (Standard Input)
- Programs read input from the keyboard unless redirected.  
- `<` sends file content to a command as stdin.
- Combined redirection: `cat < file1 > file2`.

### 3. stderr (Standard Error)
- Error messages are sent to stderr (file descriptor **2**).  
- Redirect stderr: `2> file`.
- Redirect both stdout + stderr: `> file 2>&1` or `&> file`.
- Suppress errors: `2> /dev/null`.

### 4. Pipe (`|`) and tee
- `|` sends stdout from one command to stdin of another. Example: `ls -la /etc | less`.  
- `tee` shows output and writes it to a file simultaneously.
- Example: `ls | tee list.txt`.

### 5. env (Environment)
- Environment variables store session info like `$HOME`, `$USER`, `$PATH`.  
- View all: `env`.
- Make new variables: `export VAR=value`.
- Make them persistent by adding to `~/.bashrc`.

### 6. cut
- Extracts sections of text. Works by **characters** (`-c`) or **fields** (`-f`).  
- Custom delimiters via `-d`.
- Example: `cut -f 1 -d ';' file`.

### 7. paste
- Merges lines of text horizontally.  
- `-s` merges all lines into one.
- `-d` sets a custom delimiter.

### 8. head
- Shows the first 10 lines of a file.  
- Custom lines: `head -n 20 file.txt`.

### 9. tail
- Shows the last 10 lines. Custom via `-n`.  
- `tail -f` follows a file in real‑time (common for logs).

### 10. expand and unexpand
- `expand` → tabs → spaces.  
- `unexpand` → spaces → tabs.
- Example: `expand file > newfile`.

### 11. join & split
- `join` merges files based on a shared field. Requires sorted input.  
- `split` breaks large files into chunks.

### 12. sort
- Sorts lines alphabetically or numerically.  
- Reverse sort: `sort -r`.

### 13. tr (Translate)
- Translates characters or deletes them.  
- Uppercase: `tr a-z A-Z`.
- Delete digits: `tr -d '0-9'`.

### 14. uniq
- Removes duplicate **adjacent** lines.  
- Use `sort | uniq` for unsorted files.
- Count occurrences: `uniq -c`.

### 15. wc & nl
- `wc` counts lines, words, bytes. Flags: `-l`, `-w`, `-c`.  
- `nl` numbers lines.

---

## Command Examples

### Redirection
```bash
echo "Hello" > msg.txt
echo "More text" >> msg.txt
ls 2> errors.log
cat < input.txt > output.txt
```

### Pipes & Tee
```bash
ls -la /etc | less
ls | tee list.txt
ls -la | tee all.txt | grep conf
```

### Text Processing
```bash
cut -d ';' -f 1 sample.txt
paste -s -d ' ' sample2.txt
head -n 15 /var/log/syslog
tail -f /var/log/syslog
sort file.txt | uniq
echo "hello" | tr a-z A-Z
```

### Environment Variables
```bash
echo $PATH
env
export TEST=value
source ~/.bashrc
```

---

## My Kali Linux Practice (VirtualBox)
- Practiced stdout, stdin, and stderr redirection using various files.
- Used pipes to chain commands effectively.
- Experimented with `tee` for simultaneous viewing and logging.
- Processed text using `cut`, `paste`, `sort`, `uniq`, and `tr`.
- Monitored logs in real‑time with `tail -f`.
- Explored environment variables and modified `$PATH` in a safe VM environment.

---

## LabEx Conclusions
- Text manipulation is central to real command‑line productivity.  
- Redirection, pipes, and environment variables form the backbone of scripting.  
- Tools like `cut`, `paste`, `sort`, and `uniq` offer powerful solutions for processing structured and unstructured data.  
