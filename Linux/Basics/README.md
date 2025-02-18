# Linux Basics

Linux is a powerful, open-source, Unix-like operating system widely used in the tech industry, especially for cloud computing, DevOps, and server administration. This README will guide you through some foundational concepts and basic Linux commands that are essential for working with Linux.

---

## What is Linux?

Linux is an open-source, Unix-like operating system known for its stability, security, and flexibility. It is commonly used on servers, desktops, and embedded systems. 

- The core of Linux is the **Linux kernel**.
- Linux distributions (such as Ubuntu, CentOS, Fedora, etc.) package the kernel with different software to provide a full operating system.

---

## Basic Linux Commands

Here are some of the most common commands in Linux:

### 1. `pwd` - Print Working Directory
Prints the current working directory.
```bash
pwd
```

### 2. `ls` - List Files and Directories
Lists files and directories.
```bash
ls
ls -l    # Detailed listing
ls -a    # Includes hidden files
```

### 3. `cd` - Change Directory
Changes the current directory.
```bash
cd /path/to/directory
cd ..    # Move one level up
cd ~     # Go to home directory
```

### 4. `mkdir` - Make Directory
Creates a new directory.
```bash
mkdir new_directory
```

### 5. `rm` - Remove Files or Directories
Removes files or directories.
```bash
rm file_name
rm -r directory_name  # To remove directories recursively
```

### 6. `touch` - Create an Empty File
Creates an empty file or updates the timestamp of a file.
```bash
touch newfile.txt
```

### 7. `cat` - Concatenate and Display File Content
Displays the contents of a file.
```bash
cat file_name
```

### 8. `man` - Manual Pages
Shows the manual page for a command (helps with command documentation).
```bash
man ls
```

### 9. `cp` - Copy Files or Directories
Copies files or directories.
```bash
cp source_file destination
cp -r source_directory destination_directory  # For directories
```

### 10. `mv` - Move or Rename Files or Directories
Moves or renames files or directories.
```bash
mv old_name new_name
mv file_name /path/to/destination
```

---

## Navigating the File System

Linux has a hierarchical file system that starts from the root directory (`/`). Here is a simple example of the Linux directory structure:

- `/`: The root directory, where everything starts.
- `/home`: Contains home directories for users.
- `/etc`: Configuration files for the system.
- `/var`: Variable files such as logs.
- `/usr`: User programs and files.
- `/bin`: Essential system binaries.
- `/tmp`: Temporary files.

---
