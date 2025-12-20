# Linux Learning Documentation

Hi! I’m Ashton, and this repository documents my daily Linux practice and learning.
My goal is to build strong Linux fundamentals for Cloud / DevOps roles.

## What I’m Learning
- Using the shell
- Moving around the filesystem
- Working with Text Files
- Managing running processes
- Writing simple shell scripts

## Tools & Environment
- OS: Arch Linux x86_64
- Kernel: Linux 6.18.1-arch1-2
- Shell: Bash
- Editor: Vim
- Terminal: Kitty 0.44.0

## Repository Structure
```text
Linux-Learning/
├── README.md
└── bash-scripts/
    └── backup.sh

```
## 📌 Note
I studied Linux consistently before starting this log.
Daily logging begins here to keep track of progress going forward.

## Previous Topics I covered

## 📖 Learning Log

**Entry 1**
- Focus: Using locate to find files by name, Searching files with find, Finding files by user, Finding files by permission, Finding files by date and time, Using 'not' and 'or' when finding files, Finding files and executing commands, Searching in file with grep
- Commands / Concepts: `-not`,`-or`,`grep`,`locate`,`find`
- Practice:
+ Created a `TEST` directory in the home directory
+ Created files `one`, `two`, and `three`
+ Set full read, write, and execute permissions for user, group, and others
+ Used `find` to search for files writable by others from the home directory
+ Used `find` to locate files under `/usr/share/doc` not modified in over 300 days
+ Created `/tmp/FILES` directory
+ Used `find` with size filters to locate files between 5MB and 10MB under `/usr/share`
- Notes / Issues:
+ `chmod 777` grants full permissions to everyone
+ `-ctime +300` finds files older than 300 days
+ File size filters can be combined using `-size +5M -size -10M`
+ System directories like `/usr/share` often require elevated privileges
+ Copying files from `/usr/share` to `/tmp/FILES` was unsuccessful due to permission restrictions
+ Some files could not be accessed without `sudo`


