# File Operations

Comprehensive guide to file and directory management, navigation, and manipulation commands.

## Navigation & Directory Operations

### `pwd` - Print working directory
```bash
pwd              # Show current directory path
pwd -P           # Show physical path (resolve symlinks)
```

### `cd` - Change directory
```bash
cd               # Go to home directory
cd ~             # Go to home directory
cd /             # Go to root directory
cd ..            # Go up one directory
cd ../..         # Go up two directories
cd -             # Go to previous directory
cd /path/to/dir  # Go to specific directory
```

### `ls` - List directory contents
```bash
ls               # List files and directories
ls -l            # Long format (permissions, owner, size, date)
ls -la           # Include hidden files
ls -lh           # Human readable sizes
ls -lt           # Sort by modification time
ls -lS           # Sort by file size
ls -lR           # Recursive listing
ls *.txt         # List files matching pattern
ls -d */         # List only directories
```

### `tree` - Directory tree view
```bash
tree             # Show directory tree
tree -a          # Include hidden files
tree -d          # Directories only
tree -L 2        # Limit depth to 2 levels
tree -h          # Human readable sizes
```

## File Creation & Editing

### `touch` - Create empty files or update timestamps
```bash
touch file.txt            # Create empty file or update timestamp
touch file1 file2 file3   # Create multiple files
touch -d "2024-01-01" file.txt  # Set specific timestamp
```

### `mkdir` - Create directories
```bash
mkdir dirname             # Create directory
mkdir -p path/to/nested   # Create nested directories
mkdir {dir1,dir2,dir3}    # Create multiple directories
mkdir -m 755 dirname      # Create with specific permissions
```

### Quick file editing
```bash
nano file.txt    # Simple text editor
vim file.txt     # Advanced text editor
emacs file.txt   # Emacs editor
code file.txt    # VS Code (if installed)
```

## File Copying & Moving

### `cp` - Copy files and directories
```bash
cp source dest            # Copy file
cp -r source_dir dest_dir # Copy directory recursively
cp -p source dest         # Preserve permissions and timestamps
cp -u source dest         # Copy only if source is newer
cp *.txt backup/          # Copy files matching pattern
cp -i source dest         # Interactive (ask before overwrite)
cp -v source dest         # Verbose output
```

### `mv` - Move/rename files and directories
```bash
mv oldname newname        # Rename file or directory
mv file /path/to/dest/    # Move file to directory
mv *.txt archive/         # Move files matching pattern
mv -i source dest         # Interactive (ask before overwrite)
mv -v source dest         # Verbose output
```

### `rsync` - Advanced copying with sync capabilities
```bash
rsync -av source/ dest/           # Archive mode, verbose
rsync -av --delete source/ dest/  # Delete files in dest not in source
rsync -av --exclude='*.log' src/ dst/  # Exclude files
rsync -n -av source/ dest/        # Dry run (preview changes)
```

## File Deletion

### `rm` - Remove files and directories
```bash
rm file.txt              # Remove file
rm -i file.txt           # Interactive removal
rm -f file.txt           # Force removal (no prompt)
rm -r directory          # Remove directory recursively
rm -rf directory         # Force remove directory
rm *.tmp                 # Remove files matching pattern
rm -- -filename          # Remove file starting with dash
```

### `rmdir` - Remove empty directories
```bash
rmdir dirname            # Remove empty directory
rmdir -p path/to/empty   # Remove empty directory path
```

## File Permissions & Ownership

### `chmod` - Change file permissions
```bash
chmod 755 file.sh        # rwxr-xr-x permissions
chmod +x script.sh       # Add execute permission
chmod -w file.txt        # Remove write permission
chmod u+rw,g+r,o-rwx file.txt  # User: rw, Group: r, Other: none
chmod -R 644 /var/www/   # Recursive permission change
```

### `chown` - Change file ownership
```bash
sudo chown user file.txt         # Change owner
sudo chown user:group file.txt   # Change owner and group
sudo chown -R user:group dir/    # Recursive ownership change
sudo chown :group file.txt       # Change group only
```

### `chgrp` - Change group ownership
```bash
chgrp group file.txt     # Change group
chgrp -R group dir/      # Recursive group change
```

## File Information & Attributes

### `stat` - Detailed file information
```bash
stat file.txt            # File statistics
stat -c '%n %s %Y' *     # Custom format: name, size, mtime
```

### `file` - Determine file type
```bash
file filename            # Show file type
file -i filename         # MIME type
file *                   # File types of all files
```

### `wc` - Word, line, character, and byte counts
```bash
wc file.txt              # Lines, words, characters
wc -l file.txt           # Line count only
wc -w file.txt           # Word count only
wc -c file.txt           # Character count
wc -m file.txt           # Byte count
```

### `du` - Disk usage
```bash
du file.txt              # File size
du -h file.txt           # Human readable size
du -sh directory         # Total directory size
du -ah directory         # All files with sizes
```

## File Linking

### `ln` - Create links
```bash
ln source link           # Hard link
ln -s source link        # Symbolic (soft) link
ln -sf source link       # Force symbolic link
readlink link            # Show symlink target
```

## File Comparison

### `diff` - Compare files
```bash
diff file1 file2         # Show differences
diff -u file1 file2      # Unified format
diff -r dir1 dir2        # Compare directories
diff -q file1 file2      # Brief output (files differ or not)
```

### `cmp` - Compare files byte by byte
```bash
cmp file1 file2          # Compare files
cmp -s file1 file2       # Silent mode (exit code only)
```

## File Finding

### `find` - Search for files and directories
```bash
find /path -name "*.txt"          # Find files by name
find /path -type f -name "*.log"  # Find files only
find /path -type d -name "cache"  # Find directories only
find /path -size +100M            # Find large files
find /path -mtime -7               # Modified in last 7 days
find /path -user username          # Files owned by user
find /path -perm 755               # Files with specific permissions
find /path -name "*.tmp" -delete   # Find and delete
```

### `locate` - Quick file search (if available)
```bash
locate filename          # Find files by name
locate -i filename       # Case insensitive search
updatedb                 # Update locate database (sudo required)
```

### `which` & `whereis` - Find commands
```bash
which command            # Find command location
whereis command          # Find command, source, manual
type command             # Show command type
```

## Archive Operations

### `tar` - Archive files
```bash
tar -cf archive.tar files/       # Create archive
tar -czf archive.tar.gz files/   # Create compressed archive (gzip)
tar -cjf archive.tar.bz2 files/  # Create compressed archive (bzip2)
tar -tf archive.tar              # List archive contents
tar -xf archive.tar              # Extract archive
tar -xzf archive.tar.gz          # Extract gzip archive
tar -xjf archive.tar.bz2         # Extract bzip2 archive
tar -xf archive.tar -C /path/    # Extract to specific directory
```

### `zip` & `unzip` - ZIP archives
```bash
zip -r archive.zip directory/    # Create ZIP archive
zip archive.zip file1 file2      # Add files to ZIP
unzip archive.zip                # Extract ZIP archive
unzip -l archive.zip             # List ZIP contents
unzip archive.zip -d /path/      # Extract to directory
```

## File Monitoring

### `watch` - Execute commands periodically
```bash
watch ls -la             # Watch directory changes
watch -n 5 df -h         # Watch disk space every 5 seconds
watch -d 'ps aux'        # Highlight differences
```

### `inotifywait` - Wait for file system events (if installed)
```bash
inotifywait -m /path     # Monitor directory for changes
inotifywait -e modify file.txt  # Wait for file modification
```

## Bulk Operations

### Rename multiple files
```bash
# Using rename command (if available)
rename 's/old/new/' *.txt        # Rename pattern in filenames
rename 's/\.jpeg$/.jpg/' *.jpeg  # Change file extensions

# Using bash parameter expansion
for file in *.txt; do mv "$file" "${file%.txt}.bak"; done
```

### Create multiple files/directories
```bash
touch file{1..10}.txt    # Create file1.txt through file10.txt
mkdir -p project/{src,docs,tests}/{js,css}  # Nested directory structure
```

---

**💡 Pro Tips:**
- Use tab completion to avoid typing full filenames
- Use `*` and `?` wildcards for pattern matching
- Use `{}` for brace expansion: `file{1,2,3}.txt`
- Use `~` for home directory: `~/Documents/`
- Use `.` for current directory and `..` for parent directory
- Use `Ctrl+C` to cancel long-running operations
- Always use quotes around filenames with spaces: `"file name.txt"`