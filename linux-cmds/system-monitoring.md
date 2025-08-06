# System Monitoring

Comprehensive tools for monitoring system performance, resources, and health in Linux.

## System Overview

### `uptime` - System load and uptime
```bash
uptime                            # System uptime and load averages
w                                 # Who is logged in and what they're doing
```

### `uname` - System information
```bash
uname -a                          # All system information
uname -r                          # Kernel version
uname -m                          # Machine architecture
uname -o                          # Operating system
```

### `hostnamectl` - System hostname and info (systemd)
```bash
hostnamectl                       # System hostname and info
hostnamectl status                # Detailed system information
```

## CPU Monitoring

### `top` - Real-time process and CPU monitor
```bash
top                               # Interactive process monitor
top -u username                   # Show processes for specific user
top -p PID                        # Monitor specific process
top -d 5                          # Update every 5 seconds
# Interactive commands:
# P - sort by CPU usage
# M - sort by memory usage
# 1 - show individual CPU cores
# k - kill process
# r - renice process
```

### `htop` - Enhanced process monitor (if installed)
```bash
htop                              # Enhanced interactive monitor
htop -u username                  # Show processes for specific user
htop -p PID                       # Monitor specific process
# Features: colored output, mouse support, tree view
```

### `vmstat` - Virtual memory statistics
```bash
vmstat                            # System statistics snapshot
vmstat 5                          # Update every 5 seconds
vmstat 5 10                       # 10 updates every 5 seconds
# Columns: r (runnable), b (blocked), swpd (swap), free, cache, si/so (swap in/out)
```

### `mpstat` - Multiprocessor statistics (if installed)
```bash
mpstat                            # CPU utilization
mpstat -P ALL                     # All processors
mpstat 5 10                       # 10 samples every 5 seconds
```

### `sar` - System Activity Reporter (if installed)
```bash
sar                               # CPU utilization from daily logs
sar -u 5 10                       # CPU utilization, 10 samples every 5 seconds
sar -q 5 10                       # Queue length and load averages
```

## Memory Monitoring

### `free` - Memory usage
```bash
free                              # Memory usage in KB
free -h                           # Human readable format
free -m                           # Memory usage in MB
free -s 5                         # Update every 5 seconds
free -t                           # Show totals
```

### `/proc/meminfo` - Detailed memory information
```bash
cat /proc/meminfo                 # Detailed memory statistics
grep MemTotal /proc/meminfo       # Total memory
grep MemAvailable /proc/meminfo   # Available memory
```

### `ps` - Process memory usage
```bash
ps aux --sort=-%mem               # Sort processes by memory usage
ps aux --sort=-%mem | head -10    # Top 10 memory consumers
ps -o pid,ppid,%mem,%cpu,cmd      # Custom output format
```

### `pmap` - Process memory map
```bash
pmap PID                          # Memory map of process
pmap -d PID                       # Show dirty pages
pmap -x PID                       # Extended format
```

### `smem` - Memory usage per process (if installed)
```bash
smem                              # Memory usage by process
smem -p                           # Show percentages
smem -s swap                      # Sort by swap usage
smem -u                           # Show users
```

## Disk I/O Monitoring

### `iostat` - I/O statistics (if installed)
```bash
iostat                            # I/O statistics
iostat -x                         # Extended statistics
iostat 5 10                       # 10 samples every 5 seconds
iostat -d                         # Show only disk statistics
```

### `iotop` - I/O usage by process (if installed)
```bash
sudo iotop                        # Interactive I/O monitor
sudo iotop -o                     # Show only processes doing I/O
sudo iotop -a                     # Show accumulated I/O
```

### `df` - Disk space usage
```bash
df -h                             # Human readable disk usage
df -i                             # Show inode usage
df -T                             # Show filesystem types
df --total                        # Show grand total
```

### `du` - Directory usage
```bash
du -sh *                          # Size of directories/files
du -ah /var/log                   # All files with sizes
du -sh --max-depth=1 /            # One level deep from root
du -x /                           # Stay on same filesystem
```

### `/proc/diskstats` - Disk statistics
```bash
cat /proc/diskstats               # Raw disk statistics
```

## Network Monitoring

### `ss` - Socket statistics
```bash
ss -i                             # Show internal TCP information
ss -s                             # Socket statistics summary
ss -tuln                          # All listening TCP/UDP ports
```

### `iftop` - Network bandwidth monitor (if installed)
```bash
sudo iftop                        # Monitor network traffic by connection
sudo iftop -i eth0                # Monitor specific interface
sudo iftop -n                     # Don't resolve hostnames
```

### `nethogs` - Network usage by process (if installed)
```bash
sudo nethogs                      # Network usage per process
sudo nethogs eth0                 # Monitor specific interface
```

### `nload` - Network traffic monitor (if installed)
```bash
nload                             # Monitor network traffic
nload eth0                        # Monitor specific interface
```

### `/proc/net/dev` - Network device statistics
```bash
cat /proc/net/dev                 # Network interface statistics
```

## System Logs and Events

### `journalctl` - systemd journal logs
```bash
journalctl                        # All journal entries
journalctl -f                     # Follow logs in real-time
journalctl -u service_name        # Logs for specific service
journalctl -p err                 # Only error messages
journalctl --since "1 hour ago"   # Recent logs
journalctl --boot                 # Logs from current boot
journalctl -k                     # Kernel messages
journalctl --disk-usage           # Journal disk usage
```

### `dmesg` - Kernel messages
```bash
dmesg                             # Kernel ring buffer
dmesg -T                          # Human readable timestamps
dmesg -l err                      # Only error messages
dmesg -f daemon                   # Filter by facility
dmesg -w                          # Follow kernel messages
```

### Traditional log files
```bash
tail -f /var/log/syslog           # Follow system log
tail -f /var/log/auth.log         # Follow authentication log
tail -f /var/log/kern.log         # Follow kernel log
less +F /var/log/messages         # Follow log with less
```

## Hardware Monitoring

### `lscpu` - CPU information
```bash
lscpu                             # CPU architecture info
lscpu | grep MHz                  # CPU frequency information
```

### `lshw` - Hardware information (if installed)
```bash
sudo lshw                         # Complete hardware info
sudo lshw -short                  # Brief hardware summary
sudo lshw -class memory           # Memory information
sudo lshw -class processor        # CPU information
```

### `lspci` - PCI devices
```bash
lspci                             # List PCI devices
lspci -v                          # Verbose output
lspci -k                          # Show kernel modules
lspci | grep VGA                  # Graphics cards
```

### `lsusb` - USB devices
```bash
lsusb                             # List USB devices
lsusb -v                          # Verbose output
lsusb -t                          # Tree format
```

### `lsblk` - Block devices
```bash
lsblk                             # List block devices
lsblk -f                          # Show filesystems
lsblk -m                          # Show permissions
```

### `fdisk` - Disk partitioning info
```bash
sudo fdisk -l                     # List all disk partitions
sudo fdisk -l /dev/sda            # List partitions on specific disk
```

### Hardware sensors (if lm-sensors installed)
```bash
sensors                           # Temperature and fan sensors
sensors-detect                    # Detect available sensors (run once)
```

## Process and Resource Analysis

### `strace` - System call tracing
```bash
strace command                    # Trace system calls of command
strace -p PID                     # Trace running process
strace -e trace=open command      # Trace specific system calls
strace -o output.txt command      # Save trace to file
```

### `ltrace` - Library call tracing
```bash
ltrace command                    # Trace library calls
ltrace -p PID                     # Trace running process
ltrace -e malloc command          # Trace specific library calls
```

### `perf` - Performance analysis tools (if installed)
```bash
perf top                          # Real-time performance counter
perf record command               # Record performance data
perf report                       # Analyze recorded data
perf stat command                 # Performance statistics
```

### `/proc` filesystem exploration
```bash
cat /proc/loadavg                 # Load averages
cat /proc/stat                    # CPU and system statistics
cat /proc/version                 # Kernel version
cat /proc/uptime                  # System uptime
cat /proc/cpuinfo                 # CPU information
cat /proc/meminfo                 # Memory information
cat /proc/PID/status              # Process status
cat /proc/PID/limits              # Process limits
```

## System Health Checks

### File system checks
```bash
sudo fsck /dev/sda1               # File system check
sudo e2fsck -f /dev/sda1          # Force ext2/3/4 check
df -i                             # Check inode usage
```

### System temperature and power
```bash
acpi -t                           # Temperature (if available)
acpi -b                           # Battery status (laptops)
```

### Service status
```bash
systemctl list-failed            # Failed services
systemctl status                  # System status
systemctl is-system-running       # Overall system state
```

## Performance Monitoring Scripts

### One-liner system overview
```bash
echo "=== System Overview ===" && uptime && echo && echo "=== Memory ===" && free -h && echo && echo "=== Disk ===" && df -h && echo && echo "=== Top Processes ===" && ps aux --sort=-%cpu | head -6
```

### Watch system resources
```bash
watch -n 2 'echo "CPU:" && cat /proc/loadavg && echo && echo "Memory:" && free -h && echo && echo "Disk:" && df -h /'
```

### Monitor specific process
```bash
watch -n 5 'ps aux | grep process_name'
```

## Historical Data

### `atop` - Advanced system monitor (if installed)
```bash
atop                              # Current system performance
atop -r /var/log/atop/atop_YYYYMMDD # Historical data
```

### System accounting (if installed)
```bash
sa -u                             # User statistics
sa -c                             # Command statistics
lastcomm                          # Recent commands
```

---

**💡 Pro Tips:**
- Use `htop` instead of `top` for better visualization and interactivity
- Monitor load averages: values should be below CPU count for good performance
- Watch for high `wa` (I/O wait) in `top` - indicates I/O bottlenecks
- Use `iotop` to identify processes causing high disk I/O
- Check `/proc/meminfo` for detailed memory analysis
- Use `dmesg` to check for hardware errors or issues
- Monitor disk space with `df -h` regularly
- Use `watch` command to monitor changing values over time
- Keep historical monitoring data for trend analysis
- Set up log rotation to prevent log files from filling disk space