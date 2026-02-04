# 07 — Processes 

A clean, structured summary of the **Processes** module from Linux Journey. This note covers listing and monitoring processes, terminals (TTY), creation and termination, signals, priority (niceness), states, `/proc`, and shell job control — with practical commands you can run in Kali (VirtualBox). 

---

## Quick Explanations

### 1) `ps` — Listing Processes
- A **process** is a running program instance with a unique **PID**.
- `ps` shows a snapshot of processes.
- Common views: `ps` (current TTY), **BSD** style `ps aux`, and **SysV** style `ps -ef` (full format with PPID, UID, STIME)
- `top` provides a real‑time view.  

### 2) Controlling Terminal (TTY)
- **TTY** indicates the terminal that controls a process (e.g., `pts/0` for pseudo‑terminals in GUIs).
- Processes tied to a TTY typically die when the terminal closes.
- **Daemons** run without a TTY (TTY shows `?`).  

### 3) Process Details
- The kernel schedules and tracks each process (owner, status, resources, signals).
- Multiple instances of the same program are distinct processes (each with its own PID).  

### 4) Process Creation — fork/exec and Init
- New processes are created by **fork** (clone) then often **exec** (replace image).
- Parent/child relationships are visible via **PPID**.
- **init** (PID 1) is the ancestor adopted parent for orphans and starts many services.  

### 5) Process Termination
- Processes exit via `_exit(status)`;
- parent collects status with `wait` (reaping).
- **Orphan** = live child whose parent died (adopted by PID 1).
- **Zombie** = dead child awaiting `wait` (occupies a table slot until reaped).  

### 6) Signals
Signals notify or control processes. 
Processes can ignore/catch many signals; defaults often terminate.  
- **SIGINT** (Ctrl‑C)
- **SIGTSTP** (Ctrl‑Z)
- **SIGTERM** (polite terminate)
- **SIGKILL** (immediate, non‑catchable)
- **SIGHUP** (reload)
- **SIGSTOP/SIGCONT** (stop/continue)

### 7) `kill` — Sending Signals
- `kill <PID>` sends **SIGTERM** by default.
- `kill -9 <PID>` sends **SIGKILL`.
- `kill -0 <PID>` checks existence/permission without signaling.
- `kill %1` You can also target jobs.  

### 8) Niceness (Priority)
- Scheduler priority can be influenced with **niceness** (−20 highest priority, 19 lowest).
- Start with `nice -n <N> cmd` or adjust running processes with `renice`.
- View NI column in `top`.  

### 9) Process States
Common STAT codes:  
**R** (running/runnable)  
**S** (interruptible sleep)  
**D** (uninterruptible sleep)  
**T** (stopped)  
**Z** (zombie). 
Helpful for diagnosing blocking I/O, paused jobs, or zombie buildup.  

### 10) `/proc` filesystem
- Virtual, in‑memory filesystem that exposes kernel and process data.
- Each PID has a directory `/proc/<pid>` with `status`, `cmdline`, etc.
- Many tools (`ps`, `top`) read from `/proc`.  

### 11) Job Control (Shell)
Manage foreground/background jobs within a shell: 
- `&` to run in background;
- `Ctrl‑Z` to suspend
- `bg` to continue in background
- `fg` to bring to foreground
- `jobs` to list
- `%<id>` Target a job 

---

## Command Examples

### Snapshot vs Real‑Time
```bash
ps            # processes on current TTY
ps aux        # all processes (BSD format)
ps -ef        # all processes (full SysV format)
top           # dynamic, real-time view
```

### TTY & Hierarchy
```bash
ps -o pid,ppid,tty,stat,cmd | head
ps l          # long format; shows PPID
```

### Creation & Termination
```bash
# Demonstrate parent/child relationships
bash -c 'ps -o pid,ppid,cmd | head'

# Observe zombies/orphans (rare on healthy systems)
ps -o pid,ppid,stat,cmd | grep -E ' Z |<defunct>'
```

### Signals & kill
```bash
kill 12345        # SIGTERM by default
kill -9 12345     # SIGKILL (force)
kill -0 12345     # probe existence/permissions
```

### Niceness
```bash
nice -n 10 long_task
renice 5 -p 3245
```

### /proc
```bash
ls /proc
cat /proc/$$/status   # current shell process info
```

### Job Control
```bash
sleep 1000 &
jobs
fg %1        # bring job 1 to foreground
bg %1        # send it back to background
```

---

## My Kali Linux Practice (VirtualBox)
- Compared `ps aux` vs `ps -ef` and identified PPIDs; used `top` to watch CPU and NI changes.
- Observed TTY values (`pts/*`) and noted daemons with `?`.  
- Sent `SIGTERM`/`SIGKILL` to test processes; tried `kill -0` to probe existence.  
- Practiced `nice`/`renice` adjustments and read `/proc/$$/status`.  
- Used shell job control: `&`, `Ctrl-Z`, `bg`, `fg`, `jobs`.  

---

## LabEx Conclusions
 Processes have lifecycles: 
- creation (fork/exec)
- execution (states/priority)
- signaling
- termination (wait/reap)
Mastering these tools is essential for diagnosing performance and stability.  
`/proc` and job control give you deep visibility and flexible control from the shell without extra tools.  
