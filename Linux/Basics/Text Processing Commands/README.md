# Advanced Text Processing Commands: `grep`, `sed`, and `awk`

## 1. `grep` Command

The grep command is used for searching text using patterns. It searches a file or command output for a specific string or regular expression and outputs lines that match.

### Syntax:
```bash
grep [options] pattern [file]
```

### Options for `grep`:
- **`-i`**: Perform a case-insensitive search.
- **`-v`**: Invert the match (display lines that do not match the pattern).
- **`-r` or `-R`**: Recursively search directories.
- **`-l`**: Display only the names of files with matching lines.
- **`-L`**: Display names of files without matching lines.
- **`-n`**: Display line numbers with matching lines.
- **`-c`**: Display only the count of matching lines.
- **`-H`**: Show the filename with matching lines (default when searching multiple files).
- **`-h`**: Suppress the filename in the output (useful when searching multiple files).
- **`-o`**: Show only the matched part of the line.
- **`-q`**: Quiet mode. Suppress output; only returns exit status.
- **`-w`**: Search for whole words (matches exactly).
- **`-x`**: Match whole lines only (i.e., the entire line must match the pattern).
- **`-A [num]`**: Print [num] lines of trailing context after the match.
- **`-B [num]`**: Print [num] lines of leading context before the match.
- **`-C [num]`**: Print [num] lines of context (both before and after the match).
- **`-e`**: Use multiple patterns to search for.
- **`-f`**: Read patterns from a file.
- **`--color`**: Highlight the matching text in the output.

### Example (case-insensitive search for "error"):
```bash
grep -i "error" logfile.txt
```

### Example (search recursively in a directory):
```bash
grep -r "error" /home/user/logs
```

---

## 2. `sed` Command

The sed (stream editor) command is used for modifying and transforming text in a file or stream. It supports basic text manipulation, such as search and replace, text insertion, and deletion.

### Syntax:
```bash
sed [options] 'command' [file]
```

### Options for `sed`:
- **`-e`**: Add multiple editing commands.
- **`-i`**: Edit files in place (directly modify the file).
- **`-n`**: Suppress automatic printing of pattern space (useful with `p` command).
- **`-r` or `-E`**: Use extended regular expressions (default uses basic regular expressions).
- **`-f`**: Read commands from a file.
- **`-u`**: Unbuffered output (useful for large files).
- **`--version`**: Display the version of `sed`.
- **`--help`**: Display help information for `sed`.

### Example (substitute "old" with "new" in place):
```bash
sed -i 's/old/new/' file.txt
```

### Example (delete lines containing "pattern"):
```bash
sed '/pattern/d' file.txt
```

---

## 3. `awk` Command

The awk command is a powerful text-processing language for pattern scanning and processing. It is used for processing and analyzing text files, and for extracting and reporting specific fields from structured text, especially tabular data.

### Syntax:
```bash
awk [options] 'pattern { action }' [file]
```

### Options for `awk`:
- **`-F [field separator]`**: Specify the input field separator (default is whitespace).
- **`-v var=value`**: Assign a value to a variable before executing the program.
- **`-f [program file]`**: Read the `awk` program from a file.
- **`-W compat`**: Enable compatibility mode (for older versions of `awk`).
- **`-W error`**: Make `awk` exit with an error if an undefined variable is used.
- **`-W posix`**: Enable POSIX mode (strict adherence to the POSIX standard).
- **`--version`**: Display version information.
- **`--help`**: Display help information for `awk`.

### Example (print the first and third columns):
```bash
awk '{ print $1, $3 }' file.txt
```

### Example (print lines where the second column equals "hello"):
```bash
awk '$2 == "hello" { print $0 }' file.txt
```

### Example (use a custom field separator):
```bash
awk -F ':' '{ print $1, $3 }' file.txt
```
This command splits the file using `:` as the delimiter and prints the first and third columns.

---

## Summary of Options:

- **`grep` Options**: Includes options for case-insensitive search, recursion, output formatting, and displaying file matches.
- **`sed` Options**: Allows for in-place file editing, extended regex support, and custom text manipulation commands.
- **`awk` Options**: Provides control over field separators, variable assignment, and allows reading programs from files.
