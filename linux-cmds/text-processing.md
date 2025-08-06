# Text Processing

Essential commands for text manipulation, searching, filtering, and processing in Linux.

## Text Viewing & Display

### `cat` - Display file contents
```bash
cat file.txt                      # Display entire file
cat -n file.txt                   # Display with line numbers
cat -A file.txt                   # Show all characters (tabs, ends)
cat -s file.txt                   # Squeeze multiple blank lines
cat file1 file2 > merged.txt      # Concatenate files
```

### `less` & `more` - Paginated file viewing
```bash
less file.txt                     # View file with scrolling
less +F file.txt                  # Follow file (like tail -f)
less +/pattern file.txt           # Start at first match
# Less navigation: q (quit), / (search), n (next), p (previous)

more file.txt                     # Basic pager (less preferred)
```

### `head` & `tail` - View file beginnings and ends
```bash
head file.txt                     # First 10 lines
head -n 20 file.txt               # First 20 lines
head -c 100 file.txt              # First 100 characters

tail file.txt                     # Last 10 lines
tail -n 20 file.txt               # Last 20 lines
tail -f file.txt                  # Follow file (watch for changes)
tail -F file.txt                  # Follow file even if rotated
tail +10 file.txt                 # Start from line 10
```

## Text Searching

### `grep` - Pattern searching
```bash
grep pattern file.txt             # Search for pattern
grep -i pattern file.txt          # Case insensitive search
grep -v pattern file.txt          # Invert match (exclude lines)
grep -n pattern file.txt          # Show line numbers
grep -c pattern file.txt          # Count matching lines
grep -l pattern *.txt             # List files containing pattern
grep -r pattern directory/        # Recursive search
grep -w pattern file.txt          # Match whole words only
grep -A 3 pattern file.txt        # Show 3 lines after match
grep -B 3 pattern file.txt        # Show 3 lines before match
grep -C 3 pattern file.txt        # Show 3 lines around match
```

### Advanced `grep` patterns
```bash
grep '^pattern' file.txt          # Lines starting with pattern
grep 'pattern$' file.txt          # Lines ending with pattern
grep '[0-9]' file.txt             # Lines containing digits
grep '^$' file.txt                # Empty lines
grep -E 'pattern1|pattern2' file.txt  # Multiple patterns (extended regex)
grep -P '\d+' file.txt            # Perl-compatible regex
```

### `rg` (ripgrep) - Fast alternative to grep (if installed)
```bash
rg pattern                        # Search current directory
rg -i pattern                     # Case insensitive
rg -A 3 -B 3 pattern              # Context lines
rg --type py pattern              # Search only Python files
rg -v pattern                     # Invert match
```

### `ack` - Programmer-friendly search tool (if installed)
```bash
ack pattern                       # Search in current directory
ack --python pattern              # Search only Python files
ack -i pattern                    # Case insensitive
ack -v pattern                    # Invert match
```

## Text Manipulation

### `sed` - Stream editor
```bash
sed 's/old/new/' file.txt         # Replace first occurrence per line
sed 's/old/new/g' file.txt        # Replace all occurrences
sed 's/old/new/gi' file.txt       # Case insensitive global replace
sed '2s/old/new/' file.txt        # Replace only on line 2
sed '/pattern/s/old/new/' file.txt # Replace only on lines matching pattern
sed '2,5s/old/new/' file.txt      # Replace on lines 2-5
sed '/^#/d' file.txt              # Delete lines starting with #
sed -i 's/old/new/g' file.txt     # Edit file in place
sed -n '2,5p' file.txt            # Print only lines 2-5
```

### `awk` - Pattern scanning and processing
```bash
awk '{print $1}' file.txt         # Print first column
awk '{print $1, $3}' file.txt     # Print columns 1 and 3
awk '{print NF}' file.txt         # Print number of fields per line
awk '{print NR, $0}' file.txt     # Print line number and entire line
awk '/pattern/ {print $1}' file.txt # Print first column of matching lines
awk -F: '{print $1}' /etc/passwd  # Use colon as field separator
awk 'NR==2' file.txt              # Print line 2
awk 'length > 80' file.txt        # Print lines longer than 80 characters
awk '{sum += $1} END {print sum}' file.txt # Sum first column
```

### Advanced `awk` examples
```bash
awk '{count[$1]++} END {for (word in count) print word, count[word]}' file.txt # Count words
awk 'BEGIN{OFS=","} {$1=$1; print}' file.txt # Convert spaces to commas
awk '!seen[$0]++' file.txt         # Remove duplicate lines
awk 'FNR==NR{a[$0];next} ($0 in a)' file1 file2 # Print lines in file2 that exist in file1
```

### `tr` - Translate or delete characters
```bash
tr 'a-z' 'A-Z' < file.txt         # Convert to uppercase
tr 'A-Z' 'a-z' < file.txt         # Convert to lowercase
tr -d '0-9' < file.txt            # Delete all digits
tr -s ' ' < file.txt              # Squeeze repeated spaces
tr '\n' ' ' < file.txt            # Replace newlines with spaces
tr -cd '[:alnum:]' < file.txt     # Keep only alphanumeric characters
echo "text" | tr 'a-zA-Z' 'n-za-mN-ZA-M' # ROT13 encoding
```

### `cut` - Extract columns from text
```bash
cut -d: -f1 /etc/passwd           # Extract first field (delimiter: colon)
cut -c1-10 file.txt               # Extract characters 1-10
cut -d' ' -f2,4 file.txt          # Extract fields 2 and 4 (delimiter: space)
cut -d, -f2- file.txt             # Extract from field 2 to end
ps aux | cut -c1-20               # Extract first 20 characters
```

### `sort` - Sort lines of text
```bash
sort file.txt                     # Sort lines alphabetically
sort -n file.txt                  # Numeric sort
sort -r file.txt                  # Reverse sort
sort -u file.txt                  # Sort and remove duplicates
sort -k 2 file.txt                # Sort by second field
sort -k 2,2 -k 3,3n file.txt      # Sort by field 2, then by field 3 numerically
sort -t: -k3n /etc/passwd         # Sort by third field numerically (delimiter: colon)
sort -h file.txt                  # Human numeric sort (1K, 2M, 3G)
```

### `uniq` - Remove or report duplicate lines
```bash
uniq file.txt                     # Remove consecutive duplicate lines
uniq -c file.txt                  # Count occurrences
uniq -d file.txt                  # Show only duplicate lines
uniq -u file.txt                  # Show only unique lines
sort file.txt | uniq              # Remove all duplicates (sort first)
sort file.txt | uniq -c | sort -nr # Count and sort by frequency
```

## Text Comparison

### `diff` - Compare files line by line
```bash
diff file1 file2                  # Show differences
diff -u file1 file2               # Unified format
diff -c file1 file2               # Context format
diff -y file1 file2               # Side-by-side format
diff -w file1 file2               # Ignore whitespace
diff -r dir1 dir2                 # Compare directories recursively
diff -q file1 file2               # Brief output (files differ or not)
```

### `comm` - Compare sorted files line by line
```bash
comm file1 file2                  # Three columns: unique to file1, unique to file2, common
comm -1 file1 file2               # Suppress lines unique to file1
comm -2 file1 file2               # Suppress lines unique to file2
comm -3 file1 file2               # Suppress lines common to both
```

### `cmp` - Compare files byte by byte
```bash
cmp file1 file2                   # Compare files
cmp -l file1 file2                # Show all differences
cmp -s file1 file2                # Silent mode (exit status only)
```

## Column and Field Processing

### `column` - Format text into columns
```bash
column -t file.txt                # Align columns
column -t -s: /etc/passwd         # Use colon as separator
mount | column -t                 # Format mount output
```

### `paste` - Merge lines of files
```bash
paste file1 file2                 # Merge lines side by side
paste -d: file1 file2             # Use colon as delimiter
paste -s file.txt                 # Merge all lines into one
```

### `join` - Join lines based on common field
```bash
join file1 file2                  # Join on first field
join -1 2 -2 1 file1 file2        # Join field 2 of file1 with field 1 of file2
join -t: file1 file2              # Use colon as field separator
join -a 1 file1 file2             # Include unmatched lines from file1
```

## String Processing

### `wc` - Word, line, character, and byte counts
```bash
wc file.txt                       # Lines, words, characters
wc -l file.txt                    # Line count only
wc -w file.txt                    # Word count only
wc -c file.txt                    # Character count
wc -m file.txt                    # Byte count
echo "text" | wc -c               # Count characters in string
```

### `fold` - Wrap text to specified width
```bash
fold -w 80 file.txt               # Wrap at 80 characters
fold -s file.txt                  # Break only at spaces
```

### `expand` & `unexpand` - Convert tabs and spaces
```bash
expand file.txt                   # Convert tabs to spaces
expand -t 4 file.txt              # Use 4-space tabs
unexpand file.txt                 # Convert spaces to tabs
```

## Advanced Text Processing

### `xargs` - Build and execute command lines
```bash
find . -name "*.txt" | xargs grep pattern  # Search pattern in found files
echo "file1 file2 file3" | xargs rm       # Remove multiple files
find . -name "*.log" | xargs -I {} mv {} backup/ # Move files to backup
ls | xargs -n 1 echo "Processing:"        # Process one item at a time
```

### Text processing pipelines
```bash
# Count word frequency
cat file.txt | tr ' ' '\n' | sort | uniq -c | sort -nr

# Extract email addresses
grep -oE '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' file.txt

# Process CSV file
awk -F, '{print $2}' data.csv | sort | uniq -c

# Extract URLs from text
grep -oP 'https?://[^\s"]+' file.txt

# Remove comments and empty lines
sed '/^#/d; /^$/d' config.file
```

### `tee` - Write output to both stdout and files
```bash
command | tee output.txt          # Write to file and display
command | tee -a output.txt       # Append to file and display
command | tee file1 file2         # Write to multiple files
ps aux | tee >(grep python) >(grep java) # Process substitution
```

## Text Encoding and Conversion

### Character encoding
```bash
iconv -f latin1 -t utf8 file.txt  # Convert from latin1 to UTF-8
iconv -l                          # List available encodings
file -i file.txt                  # Detect file encoding
```

### Line ending conversion
```bash
dos2unix file.txt                 # Convert Windows to Unix line endings
unix2dos file.txt                 # Convert Unix to Windows line endings
tr -d '\r' < file.txt             # Remove carriage returns
```

## Regular Expressions Quick Reference

### Basic patterns
```bash
^           # Start of line
$           # End of line
.           # Any character
*           # Zero or more of preceding
+           # One or more of preceding (extended regex)
?           # Zero or one of preceding (extended regex)
[abc]       # Any of a, b, or c
[^abc]      # Any except a, b, or c
[a-z]       # Any lowercase letter
[0-9]       # Any digit
\d          # Digit (Perl-compatible regex)
\w          # Word character (Perl-compatible regex)
\s          # Whitespace (Perl-compatible regex)
```

---

**💡 Pro Tips:**
- Use `less +F` instead of `tail -f` for following files with search capability
- Combine `sort | uniq` to remove duplicates from unsorted text
- Use `grep -P` for Perl-compatible regex when basic regex isn't enough
- Use `awk 'NF'` to remove empty lines
- Use `sed -i.bak` to create backups when editing files in place
- Combine multiple text processing commands with pipes for complex operations
- Use `rg` (ripgrep) as a faster alternative to `grep` for large codebases
- Remember that `sed` and `awk` can read from stdin, making them great for pipelines
- Use `column -t` to make tabular data more readable