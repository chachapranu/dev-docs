# Common Bash Commands for Developers

## File and Directory Operations

```bash
ls                # List files and directories
cd <dir>          # Change directory
pwd               # Print working directory
mkdir <dir>       # Create a new directory
touch <file>      # Create an empty file
cp <src> <dest>   # Copy files or directories
mv <src> <dest>   # Move or rename files/directories
rm <file>         # Remove a file
rm -r <dir>       # Remove a directory and its contents
```

## Viewing and Editing Files

```bash
cat <file>        # View file contents
less <file>       # View file with paging
head <file>       # First 10 lines of a file
tail <file>       # Last 10 lines of a file
nano <file>       # Edit file in nano editor
vim <file>        # Edit file in vim editor
```

## Searching and Filtering

```bash
grep "text" <file>    # Search for text in a file
find . -name "*.py"   # Find files by name
sort <file>           # Sort lines in a file
uniq <file>           # Remove duplicate lines
wc -l <file>          # Count lines in a file
```

## System and Process Management

```bash
ps aux               # List running processes
top                  # Interactive process viewer
kill <pid>           # Kill a process by PID
df -h                # Disk space usage
du -sh <dir>         # Directory size
free -h              # Memory usage
```

## Networking

```bash
ping <host>          # Ping a host
curl <url>           # Fetch a URL
wget <url>           # Download a file
ifconfig             # Show network interfaces
```

## Permissions

```bash
chmod +x <file>      # Make file executable
chown user:group <file> # Change file owner
```

---

### Searching within command history

```bash
ctrl+r
```

### Searching for files

```bash
find . -name <file-name>
```

### Searching for a string in files

```bash
grep -r "string-to-search" .
```

### To get the path of a command

```bash
which <command-name>
```

### To see the manual for a command

```bash
man <command-name>
```

Add more commands as needed for your workflow!