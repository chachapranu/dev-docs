# Daily Admin Commands

Essential commands that system administrators and developers use daily for server maintenance and operations.

## System Status & Information

### `uptime`
Show system uptime and load averages
```bash
uptime
# 14:23:15 up 5 days, 2:10, 3 users, load average: 0.15, 0.10, 0.05
```

### `whoami` & `who`
Current user and logged-in users
```bash
whoami           # Current username
who              # All logged-in users
w                # Detailed user activity
```

### `date`
Display or set system date
```bash
date                    # Current date and time
date +"%Y-%m-%d %H:%M"  # Custom format: 2024-01-15 14:23
```

### `hostname`
Display or set system hostname
```bash
hostname         # Display hostname
hostname -I      # Display IP addresses
```

## Disk Space Management

### `df` - Disk space usage
```bash
df -h            # Human readable disk usage
df -i            # Show inode usage
df -T            # Show filesystem type
```

### `du` - Directory usage
```bash
du -sh *         # Size of current directory contents
du -sh /var/log  # Size of specific directory
du -h --max-depth=1  # One level deep
```

### `ncdu` - Interactive disk usage (if installed)
```bash
ncdu /           # Interactive disk usage browser
```

## Log Management

### `journalctl` - systemd logs
```bash
journalctl -f              # Follow logs in real-time
journalctl -u nginx        # Logs for specific service
journalctl --since "1 hour ago"  # Recent logs
journalctl -p err          # Only error messages
```

### `tail` & `head` - Log monitoring
```bash
tail -f /var/log/syslog    # Follow log file
tail -n 50 /var/log/auth.log  # Last 50 lines
head -20 /var/log/messages # First 20 lines
```

## Service Management (systemd)

### `systemctl` - Service control
```bash
systemctl status nginx     # Service status
systemctl start nginx      # Start service
systemctl stop nginx       # Stop service
systemctl restart nginx    # Restart service
systemctl reload nginx     # Reload config
systemctl enable nginx     # Enable at boot
systemctl disable nginx    # Disable at boot
systemctl list-units       # All active units
```

## Package Management

### Ubuntu/Debian (apt)
```bash
sudo apt update            # Update package list
sudo apt upgrade           # Upgrade packages
sudo apt install package   # Install package
sudo apt remove package    # Remove package
sudo apt autoremove        # Remove unused packages
apt search keyword         # Search packages
apt list --upgradable      # Show upgradable packages
```

### CentOS/RHEL (yum/dnf)
```bash
sudo yum update            # Update packages
sudo yum install package   # Install package
sudo yum remove package    # Remove package
yum search keyword         # Search packages
yum list updates           # Show available updates
```

## Quick System Checks

### Memory and CPU
```bash
free -h          # Memory usage (human readable)
lscpu            # CPU information
nproc            # Number of processors
```

### Running processes
```bash
ps aux           # All running processes
pgrep process    # Find process ID by name
pkill process    # Kill process by name
```

### Network connectivity
```bash
ping -c 4 google.com      # Test connectivity
curl -I https://site.com  # Check HTTP response
ss -tuln                  # Show listening ports
```

## Archive & Backup

### `tar` - Archive files
```bash
tar -czf backup.tar.gz /path/to/backup    # Create compressed archive
tar -xzf backup.tar.gz                    # Extract archive
tar -tzf backup.tar.gz                    # List archive contents
```

### `rsync` - Sync files
```bash
rsync -av source/ destination/           # Sync directories
rsync -av --delete source/ dest/         # Sync with deletion
rsync -av user@host:/remote/ /local/     # Remote sync
```

## File Permissions Quick Fix

### `chmod` & `chown` - Common patterns
```bash
sudo chown -R user:group /path           # Change ownership recursively
chmod 755 script.sh                      # Make executable
chmod -R 644 /var/www/html               # Web files permissions
sudo chmod +x /usr/local/bin/script     # Make script executable
```

## Environment & Variables

### Environment management
```bash
env                        # Show all environment variables
echo $PATH                 # Show PATH variable
export VAR=value           # Set environment variable
which command              # Find command location
type command               # Show command type
```

## Quick Troubleshooting

### System resources
```bash
top                        # Real-time process monitor
htop                       # Enhanced process monitor (if installed)
iotop                      # I/O monitoring (if installed)
dmesg | tail              # Recent kernel messages
```

### File system
```bash
lsof | grep filename      # Find which process uses file
lsof -i :80              # Find process using port 80
find /var -name "*.log" -size +100M  # Find large log files
```

## Aliases for Efficiency

Add these to your `~/.bashrc` or `~/.zshrc`:
```bash
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias free='free -h'
alias psg='ps aux | grep'
alias ports='ss -tuln'
```

---

**💡 Pro Tips:**
- Use `history` to recall previous commands
- Use `!!` to repeat the last command
- Use `!$` to reference the last argument of the previous command
- Use `Ctrl+R` for reverse command search
- Use `screen` or `tmux` for persistent sessions