# Process Management

Essential commands for managing processes, jobs, and system services in Linux.

## Process Viewing & Monitoring

### `ps` - Process status
```bash
ps               # Processes in current session
ps aux           # All processes (BSD style)
ps -ef           # All processes (UNIX style)
ps -u username   # Processes by specific user
ps -C processname # Processes by command name
ps --forest      # Process tree view
ps -o pid,ppid,cmd,pcpu,pmem  # Custom output format
```

### `pstree` - Process tree visualization
```bash
pstree           # Show process tree
pstree -p        # Include process IDs
pstree username  # Process tree for specific user
pstree -a        # Show command line arguments
```

### `top` - Real-time process monitor
```bash
top              # Interactive process monitor
top -u username  # Show processes for specific user
top -p PID       # Monitor specific process
# Interactive commands in top:
# k - kill process
# r - renice process
# q - quit
# M - sort by memory
# P - sort by CPU
```

### `htop` - Enhanced process monitor (if installed)
```bash
htop             # Enhanced interactive monitor
htop -u username # Show processes for specific user
# Interactive features:
# F9 - kill process
# F6 - sort options
# F4 - filter
# F5 - tree view
```

## Process Control

### Process IDs and Information
```bash
pidof process_name    # Get PID of process by name
pgrep pattern         # Find PIDs matching pattern
pgrep -f pattern      # Search full command line
pgrep -u username     # PIDs for specific user
echo $$               # Current shell PID
echo $PPID            # Parent process PID
```

### `kill` - Terminate processes
```bash
kill PID              # Terminate process (SIGTERM)
kill -9 PID           # Force kill process (SIGKILL)
kill -STOP PID        # Suspend process
kill -CONT PID        # Resume suspended process
kill -HUP PID         # Send hangup signal (reload config)
kill -USR1 PID        # Send user-defined signal 1
kill -l               # List all available signals
```

### `pkill` - Kill processes by name
```bash
pkill process_name    # Kill processes by name
pkill -f pattern      # Kill by command line pattern
pkill -u username     # Kill all processes by user
pkill -9 process_name # Force kill by name
pkill -STOP pattern   # Suspend processes
```

### `killall` - Kill all processes by name
```bash
killall process_name  # Kill all instances
killall -9 process_name # Force kill all instances
killall -i process_name # Interactive mode
killall -u username   # Kill all processes by user
```

## Job Control

### Background and Foreground Jobs
```bash
command &             # Run command in background
jobs                  # List active jobs
jobs -l               # List jobs with PIDs
fg                    # Bring last job to foreground
fg %1                 # Bring job 1 to foreground
bg                    # Send last job to background
bg %1                 # Send job 1 to background
```

### Job Control Signals
```bash
# Keyboard shortcuts:
# Ctrl+Z - Suspend current process
# Ctrl+C - Interrupt current process
# Ctrl+\ - Quit current process

disown %1             # Remove job from job table
nohup command &       # Run command immune to hangups
```

## Process Priority

### `nice` & `renice` - Process priority
```bash
nice -n 10 command    # Start with lower priority (higher nice value)
nice -n -5 command    # Start with higher priority (lower nice value)
renice 10 PID         # Change priority of running process
renice -5 -u username # Change priority for all user processes
```

### Priority levels
- Nice values: -20 (highest priority) to +19 (lowest priority)
- Default nice value: 0
- Only root can set negative nice values

## Service Management (systemd)

### `systemctl` - System and service manager
```bash
# Service status and control
systemctl status service_name     # Check service status
systemctl start service_name      # Start service
systemctl stop service_name       # Stop service
systemctl restart service_name    # Restart service
systemctl reload service_name     # Reload configuration
systemctl enable service_name     # Enable at boot
systemctl disable service_name    # Disable at boot

# System-wide operations
systemctl list-units              # List all units
systemctl list-units --failed     # List failed units
systemctl list-unit-files         # List unit files
systemctl daemon-reload           # Reload systemd configuration
systemctl poweroff                # Shutdown system
systemctl reboot                  # Restart system
```

### Service logs with `journalctl`
```bash
journalctl -u service_name        # Logs for specific service
journalctl -u service_name -f     # Follow service logs
journalctl -u service_name --since "1 hour ago"
journalctl -u service_name -n 50  # Last 50 log entries
```

## Legacy Service Management (SysV)

### `service` command (older systems)
```bash
service service_name status       # Check service status
service service_name start        # Start service
service service_name stop         # Stop service
service service_name restart      # Restart service
```

### `chkconfig` - Service configuration (RHEL/CentOS)
```bash
chkconfig --list                  # List services
chkconfig service_name on         # Enable service
chkconfig service_name off        # Disable service
```

## Process Monitoring Tools

### `watch` - Execute commands periodically
```bash
watch ps aux                      # Watch process list
watch -n 5 'ps aux | head -20'    # Update every 5 seconds
watch -d df -h                    # Highlight differences
```

### `lsof` - List open files
```bash
lsof                              # List all open files
lsof -p PID                       # Files opened by specific process
lsof -u username                  # Files opened by user
lsof /path/to/file                # Processes using specific file
lsof -i :80                       # Processes using port 80
lsof -i tcp                       # All TCP connections
```

### `fuser` - Show processes using files/sockets
```bash
fuser /path/to/file               # Processes using file
fuser -v /path/to/file            # Verbose output
fuser -k /path/to/file            # Kill processes using file
fuser 80/tcp                      # Processes using TCP port 80
```

## Process Information

### `/proc` filesystem exploration
```bash
cat /proc/PID/cmdline             # Command line of process
cat /proc/PID/environ             # Environment variables
cat /proc/PID/status              # Process status
cat /proc/PID/fd/                 # Open file descriptors
cat /proc/loadavg                 # System load average
cat /proc/meminfo                 # Memory information
```

### Process relationships
```bash
pstree -p PID                     # Process tree from specific PID
ps -o pid,ppid,cmd --pid PID      # Parent-child relationship
ps --ppid PPID                    # Child processes of PPID
```

## Advanced Process Management

### `screen` - Terminal multiplexer
```bash
screen                            # Start new screen session
screen -S session_name            # Start named session
screen -ls                        # List sessions
screen -r session_name            # Reattach to session
# Inside screen:
# Ctrl+A, D - Detach session
# Ctrl+A, C - Create new window
# Ctrl+A, N - Next window
```

### `tmux` - Terminal multiplexer (modern alternative)
```bash
tmux                              # Start new session
tmux new -s session_name          # Start named session
tmux list-sessions                # List sessions
tmux attach -t session_name       # Attach to session
tmux kill-session -t session_name # Kill session
# Inside tmux:
# Ctrl+B, D - Detach session
# Ctrl+B, C - Create new window
# Ctrl+B, N - Next window
```

### Process limits
```bash
ulimit -a                         # Show all limits
ulimit -n                         # File descriptor limit
ulimit -u                         # Process limit
ulimit -c unlimited               # Enable core dumps
```

## Troubleshooting Processes

### Stuck or zombie processes
```bash
ps aux | grep defunct             # Find zombie processes
ps -eo stat,ppid,pid,comm | grep -E '^[Zz]'  # Zombie processes
kill -9 PPID                      # Kill parent of zombie process
```

### Resource-intensive processes
```bash
ps aux --sort=-%cpu | head -10    # Top CPU consumers
ps aux --sort=-%mem | head -10    # Top memory consumers
pgrep -f process | xargs ps -o pid,pcpu,pmem,time,comm
```

### Process debugging
```bash
strace -p PID                     # Trace system calls
ltrace -p PID                     # Trace library calls
gdb -p PID                        # Attach debugger to process
```

## Automation and Scheduling

### `cron` - Scheduled tasks
```bash
crontab -l                        # List current user's cron jobs
crontab -e                        # Edit current user's cron jobs
crontab -r                        # Remove all cron jobs
sudo crontab -u username -l       # List another user's cron jobs

# Cron format: minute hour day month weekday command
# Example: 0 2 * * * /backup.sh  # Run at 2 AM daily
```

### `at` - One-time scheduled tasks
```bash
at 14:30                          # Schedule command at 2:30 PM
at now + 1 hour                   # Schedule in 1 hour
at -l                             # List scheduled jobs
at -r job_number                  # Remove scheduled job
atq                               # Queue of scheduled jobs
```

---

**💡 Pro Tips:**
- Use `Ctrl+Z` to suspend a process, then `bg` to continue it in background
- Use `nohup command &` for processes that should survive logout
- Use `pgrep -f` to find processes by their full command line
- Use `systemctl --user` for user-level services
- Monitor system load with `uptime` - values above CPU count indicate high load
- Use `kill -0 PID` to check if a process exists without affecting it