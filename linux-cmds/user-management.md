# User Management

Comprehensive guide to managing users, groups, permissions, and authentication in Linux.

## User Information

### Current user information
```bash
whoami                            # Current username
id                                # User and group IDs
id username                       # Specific user's IDs
groups                            # Current user's groups
groups username                   # Specific user's groups
finger username                   # User information (if available)
```

### Logged-in users
```bash
who                               # Currently logged in users
w                                 # Detailed user activity
users                             # List logged in usernames
last                              # Login history
last username                     # Specific user's login history
lastlog                           # Last login times for all users
```

## User Account Management

### `useradd` - Add new user
```bash
sudo useradd username             # Basic user creation
sudo useradd -m username          # Create with home directory
sudo useradd -m -s /bin/bash username # Specify shell
sudo useradd -m -G sudo,users username # Add to multiple groups
sudo useradd -m -d /custom/home username # Custom home directory
sudo useradd -m -e 2024-12-31 username # Set expiration date
sudo useradd -r system_user       # Create system user (no home)
```

### `usermod` - Modify user account
```bash
sudo usermod -l newname oldname   # Change username
sudo usermod -d /new/home -m username # Change and move home directory
sudo usermod -s /bin/zsh username # Change shell
sudo usermod -G group1,group2 username # Set user groups (replaces existing)
sudo usermod -aG sudo username    # Add user to sudo group
sudo usermod -L username          # Lock user account
sudo usermod -U username          # Unlock user account
sudo usermod -e 2024-12-31 username # Set expiration date
sudo usermod -e "" username       # Remove expiration
```

### `userdel` - Delete user
```bash
sudo userdel username             # Delete user (keep home directory)
sudo userdel -r username          # Delete user and home directory
sudo userdel -f username          # Force deletion (even if logged in)
```

### User password management
```bash
passwd                            # Change own password
sudo passwd username              # Change another user's password
sudo passwd -l username           # Lock user account
sudo passwd -u username           # Unlock user account
sudo passwd -d username           # Delete user password
sudo passwd -e username           # Force password change on next login
sudo chage -l username            # Show password aging info
sudo chage -M 90 username         # Set password expiration (90 days)
sudo chage -E 2024-12-31 username # Set account expiration
```

## Group Management

### `groupadd` - Add new group
```bash
sudo groupadd groupname           # Create new group
sudo groupadd -g 1001 groupname   # Create with specific GID
sudo groupadd -r systemgroup      # Create system group
```

### `groupmod` - Modify group
```bash
sudo groupmod -n newname oldname  # Rename group
sudo groupmod -g 1002 groupname   # Change group ID
```

### `groupdel` - Delete group
```bash
sudo groupdel groupname           # Delete group
```

### Group membership
```bash
sudo gpasswd -a username groupname # Add user to group
sudo gpasswd -d username groupname # Remove user from group
sudo gpasswd -A admin_user groupname # Set group administrator
newgrp groupname                  # Switch to group (temporary)
```

## File Permissions and Ownership

### `chmod` - Change file permissions
```bash
# Numeric method
chmod 755 file                    # rwxr-xr-x
chmod 644 file                    # rw-r--r--
chmod 600 file                    # rw-------
chmod 777 file                    # rwxrwxrwx (avoid this!)

# Symbolic method
chmod u+x file                    # Add execute for user
chmod g-w file                    # Remove write for group
chmod o=r file                    # Set other to read only
chmod a+r file                    # Add read for all
chmod u=rwx,g=rx,o=r file         # Set specific permissions
chmod -R 755 directory            # Recursive permission change
```

### Permission meanings
```bash
# File permissions:
# r (4) - read file content
# w (2) - write/modify file
# x (1) - execute file

# Directory permissions:
# r (4) - list directory contents
# w (2) - create/delete files in directory
# x (1) - enter directory
```

### `chown` - Change file ownership
```bash
sudo chown user file              # Change owner
sudo chown user:group file        # Change owner and group
sudo chown :group file            # Change group only
sudo chown -R user:group directory # Recursive ownership change
sudo chown --reference=ref_file target_file # Copy ownership from reference
```

### `chgrp` - Change group ownership
```bash
chgrp group file                  # Change group (if you're member)
sudo chgrp group file             # Change group (with sudo)
chgrp -R group directory          # Recursive group change
```

### Special permissions
```bash
# Set-UID (SUID) - run with owner's permissions
chmod u+s file                    # Set SUID
chmod 4755 file                   # Set SUID with numeric

# Set-GID (SGID) - run with group's permissions or inherit group
chmod g+s file                    # Set SGID on file
chmod g+s directory               # Set SGID on directory (inherit group)
chmod 2755 directory              # Set SGID with numeric

# Sticky bit - only owner can delete files
chmod +t directory                # Set sticky bit
chmod 1755 directory              # Set sticky bit with numeric (/tmp has this)
```

## Access Control Lists (ACLs)

### `setfacl` - Set file ACLs (if supported)
```bash
setfacl -m u:username:rwx file    # Give user specific permissions
setfacl -m g:groupname:rx file    # Give group specific permissions
setfacl -m o::r file              # Set other permissions
setfacl -x u:username file        # Remove user ACL entry
setfacl -b file                   # Remove all ACL entries
setfacl -R -m u:username:rwx dir  # Recursive ACL setting
setfacl -d -m u:username:rwx dir  # Set default ACL for directory
```

### `getfacl` - View file ACLs
```bash
getfacl file                      # Show file ACLs
getfacl -R directory              # Show ACLs recursively
```

## Sudo and Privilege Escalation

### `sudo` - Execute as another user
```bash
sudo command                      # Run as root
sudo -u username command          # Run as specific user
sudo -g groupname command         # Run as specific group
sudo -i                           # Login as root
sudo -s                           # Shell as root
sudo -l                           # List allowed commands
sudo -v                           # Refresh sudo timestamp
sudo -k                           # Clear sudo timestamp
```

### `su` - Switch user
```bash
su                                # Switch to root (requires root password)
su username                       # Switch to another user
su -                              # Login shell as root
su - username                     # Login shell as another user
su -c "command" username          # Run command as another user
```

### Sudo configuration
```bash
sudo visudo                       # Edit sudoers file safely
sudo visudo -f /etc/sudoers.d/custom # Edit custom sudo rules

# Common sudoers entries:
# username ALL=(ALL:ALL) ALL        # Full sudo access
# %admin ALL=(ALL) ALL               # Group-based access
# username ALL=(ALL) NOPASSWD: ALL  # No password required
# username ALL=(ALL) /usr/bin/systemctl # Specific commands only
```

## User Environment

### Login shells and profiles
```bash
chsh                              # Change own shell
chsh -s /bin/zsh username         # Change shell for user (sudo required)
cat /etc/shells                   # List available shells
echo $SHELL                       # Current shell
```

### Environment variables
```bash
env                               # Show all environment variables
printenv                          # Show all environment variables
printenv HOME                     # Show specific variable
export VAR=value                  # Set environment variable
unset VAR                         # Remove environment variable
```

### User configuration files
```bash
~/.bashrc                         # Bash configuration (non-login)
~/.bash_profile                   # Bash login configuration
~/.profile                        # Shell-agnostic profile
~/.bash_logout                    # Bash logout script
~/.ssh/                          # SSH configuration directory
~/.ssh/authorized_keys           # SSH public keys for login
```

## User and Group Information Files

### System files
```bash
cat /etc/passwd                   # User account information
cat /etc/shadow                   # Password hashes (root only)
cat /etc/group                    # Group information
cat /etc/gshadow                  # Group passwords (root only)
cat /etc/login.defs               # Login defaults
cat /etc/default/useradd          # Default useradd values
cat /etc/skel/                    # Default files for new users
```

### Analyzing user information
```bash
# List all users
cut -d: -f1 /etc/passwd

# List all groups
cut -d: -f1 /etc/group

# Find users with UID 0 (should only be root)
awk -F: '$3 == 0 {print $1}' /etc/passwd

# List users with login shells
grep -E '/bin/(bash|zsh|sh)$' /etc/passwd

# Find users without passwords
sudo awk -F: '$2 == "" {print $1}' /etc/shadow

# List system users (UID < 1000)
awk -F: '$3 < 1000 {print $1}' /etc/passwd

# List regular users (UID >= 1000)
awk -F: '$3 >= 1000 && $3 != 65534 {print $1}' /etc/passwd
```

## Authentication and Security

### Password policies
```bash
sudo chage -l username            # View password aging info
sudo chage -m 1 username          # Minimum days between changes
sudo chage -M 90 username         # Maximum days before expiration
sudo chage -W 7 username          # Warning days before expiration
sudo chage -I 30 username         # Days to keep account active after expiration
```

### Account locking
```bash
sudo usermod -L username          # Lock account
sudo usermod -U username          # Unlock account
sudo passwd -l username           # Lock password
sudo passwd -u username           # Unlock password
sudo chage -E 0 username          # Disable account
sudo chage -E -1 username         # Enable account
```

### Failed login attempts
```bash
sudo pam_tally2 --user username   # Show failed login attempts
sudo pam_tally2 --user username --reset # Reset failed login counter
faillog -u username               # Show failure log for user
sudo faillog -r -u username       # Reset failure count
```

## Monitoring User Activity

### Active sessions
```bash
who -H                            # Show column headers
who -b                            # Show boot time
who -r                            # Show run level
w -h                              # Without header
w -s                              # Short format
```

### Login monitoring
```bash
last -n 10                        # Last 10 logins
last username                     # Specific user's logins
last reboot                       # System reboot history
lastb                             # Failed login attempts
ac -p                             # Show login time per user
```

### Process ownership
```bash
ps -u username                    # Processes by user
ps -U username                    # Processes by real user ID
pgrep -u username                 # PIDs of user's processes
pkill -u username                 # Kill all user's processes
```

## Bulk User Operations

### Create multiple users
```bash
# Using newusers (create users from file)
echo "user1:password1:1001:1001:User One:/home/user1:/bin/bash" | sudo newusers

# Using a script
for user in user1 user2 user3; do
    sudo useradd -m "$user"
    echo "$user:defaultpass" | sudo chpasswd
done
```

### Password changes
```bash
echo "username:newpassword" | sudo chpasswd  # Change password non-interactively
sudo chpasswd < passwords.txt     # Change multiple passwords from file
```

---

**💡 Pro Tips:**
- Always use `visudo` to edit sudoers file to prevent syntax errors
- Use `sudo -l` to check what commands a user can run with sudo
- Regular users typically have UIDs ≥ 1000, system users have UIDs < 1000
- Use groups for permission management rather than individual user permissions
- The sticky bit on directories (like `/tmp`) prevents users from deleting others' files
- Use `getent passwd username` to check if a user exists across all name services
- Always create a backup when modifying critical files like `/etc/passwd`
- Use `su -` for a complete login environment, `su` for partial
- Monitor `/var/log/auth.log` for authentication events
- Use strong passwords and consider implementing password complexity requirements