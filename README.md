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

## 📖 Learning Log

**Entry 1**
- Focus: Searching files with find, Finding files by user, Finding files by permission, Finding files by date and time, Finding files and executing commands 
- Commands / Concepts: Working with text files,`find`, `mkdir`, `chmod`, `cd`,`-ctime`, `-perm`
- Practice:
    - Created a `TEST` directory in the home directory
        - `mkdir TEST`
    - Created files `one`, `two`, and `three`
        - `cd TEST`,`touch one two three` 
    - Set full read, write, and execute permissions for user, group, and others
        - `chmod ugo+rwx one two three` 
    - Used `find` to search for files writable by others from the home directory
        - `find /home/ashton -perm 777 -ls` 
    - Used `find` to locate files under `/usr/share/doc` not modified in over 300 days
        - `find /usr/share/doc -ctime +300` 
    - Created `/tmp/FILES` directory
        - `mkdir /tmp/FILES` 
    - Used `find` with size filters to locate files between 5MB and 10MB under `/usr/share`
        - `find /usr/share -size +5M -size -10M` 
- Notes / Issues:
    - `chmod 777` grants full permissions to everyone
    - `-ctime +300` finds files older than 300 days
    - System directories like `/usr/share` often require elevated privileges
    - Copying files from `/usr/share` to `/tmp/FILES` was unsuccessful due to permission restrictions
    - Some files could not be accessed without `sudo`
##

**Entry 2**
- Focus: File location, searching, directory creation, and copying files/directories
- Commands / Concepts:
    - `locate` – quickly find files using the system database
    - `find` – search files/directories by path and size
    - `mkdir` – create directories
    - `cp -r -a` – copy files/directories recursively while preserving attributes
    - Absolute vs relative paths
    - Navigating system directories (`/usr/share`, `/tmp`, home directory)

- Practice:
    - Used locate to search for passwd and /tmp/FILES
    - Created /tmp/FILES directory
    - Used find to list files and search by size range
    - Copied various system files (PDFs, .gir, .jar, .txt) from /usr/share into /tmp/FILES
    - Verified copied files using find
    - Copied selected files from /tmp/FILES into a hidden backup directory (.mybackup) in the home directory

- Notes / Issues:
    - locate may return no results if the database is not updated
    - Some cp commands initially failed due to incorrect paths
    - Learned the importance of using full absolute paths when copying system files
    - Confirmed successful file transfers by listing contents after copying
##
**Entry 3**
- Focus: Managing running processes, understanding processes, listing processes
- Command / Concepts: 
    - `ps u`
    - `ps ux | less`
    - `ps uax | less`
    - `ps -eo`
    - listing and changing processes with htop
    
- Practice:
    - List all processes running on my system, showing a full set of columns
        - `ps u`
    - sort those processes by the name of the user
        - `ps u --sort=-user | less`
    - List all display the following columns: process ID, username, group name, virtual memory size, resident memory size, and the command.
        - `ps -eo pid,user,group,vsz,rss,comm | head`
    - Run the htop command to view processes running on my system. Go back and forth between CPU and memory.
        - `htop` - M keybind to switch to memory
        
- Notes / Issues:
    - VSZ shows the size of the image process, the amount of memory allocated for the process.
    - RSS shows the size of the program in memory, the amount that is actually being used.
    

##
**Entry 4**
- Focus: Starting background processes, Killing and renicing processes
- Command / Concepts: `jobs`, `fg %`,`bg %`, `nice`, `renice`, `kill`, `killall`

- Practice:
    - Used `kill -SIGSTOP <pid>` to pause the `gedit` process
    - Ran `gedit` with an initial nice value of 5 using the `nice` command 
    - Using the `renice` command change value to 7
    - Verified the updated nice value using the `top` command
    
- Notes / Issues: 
    - SIGSTOP immediately pauses a process and cannot be ignored by the process
    - Lower nice values give a process higher priority, while higher nice values lower its priority
    - Only privileged users can decrease a nice value (increase priority)
    - The top command displays the current nice value under the NI column
jobs, fg, and bg only work with processes started from the current shell

##
**Entry 5**
- Focus: Executing and degbugging shell scripts
- Commands / Concepts: `touch myscript`, `sudo vim myscript`, `bash -x myscript`

- Practice: 
    - Created a script file using `touch myscript` in my home directory
    - Edited the script multiple times with `sudo vim`
    - Executed the script using `bash -x myscript` to trace commands line by line

- Notes: 
    - `bash -x myscript` executes commands from a file
    - `bash -x` prints each command before executing it, which is useful for debugging

##
**Entry 6**
- Focus: Creating and executing a bash script, passing arguments, and running it via PATH.
- Commands / Concepts: `mv`, `chmod 755`, Executable scripts $PATH, Positional parameters ($1, $2),`bash -x`, Variable defaults (${VAR:-default})

- Practice:
    - Create a script named myscript
        - Used the read command to prompt the user for information and store that information to use later in the script.
    - Make it executable
    - Run the script with arguments (foo bar)
    - Debug execution
    - Rename and execute the script
    - Typed commands in shell to test how parameter expansion works 
        - `${var:-value}`- uses value if var is unset or empty

- Notes:
    - Script arguments are accessed using positional parameters:
    - $1 → first argument (foo)
    - $2 → second argument (bar)
    - Arguments do nothing unless explicitly used inside the script.
    - A script can be run without ./ only if it is located in a directory included in $PATH (e.g. ~/bin).
    - chmod 755 myscript is required to allow direct execution.
    - bash -x myscript prints each command as it runs and is useful for debugging.
    - ${VAR:-"Not Set"} assigns a default value when a variable is unset or empty.
    - File extensions like .sh are optional; execution depends on permissions and the shebang.

##
**Entry 7**

### Focus
Bash parameter expansion, arithmetic operations, command history, script execution, and file permissions.

### Commands / Concepts
- Clearing the terminal and using `history`
- Variable assignment and expansion
- Filename parsing using parameter expansion:
  - `${VAR##*/}` – extract filename
  - `${VAR%/*}` – extract directory path
  - `${VAR%.*}` – remove file extension
  - `${VAR##*.}` – extract file extension
- Integer arithmetic methods:
  - `let`
  - `expr`
  - `bc`
- Increment operators:
  - `++I` (pre-increment)
  - `I++` (post-increment)
- Script execution and debugging:
  - `./script`
  - `bash -x script`
- File permissions and ownership:
  - `chmod`
  - `chown`
- Using `~/bin` for user scripts

### Practice
- Defined `MYFILENAME` and extracted:
  - filename
  - directory path
  - base name
  - file extension
- Verified variable expansion using `echo`
- Performed arithmetic division on `BIGNUM=1024` using:
  - `let`
  - `expr`
  - `bc`
- Generated random numbers using `$RANDOM`
- Tested pre-increment vs post-increment behavior
- Created and executed `ifthen.sh`
- Debugged script execution with `bash -x`
- Set executable permissions with `chmod 755`
- Moved script to `~/bin` and renamed it
- Verified permissions and ownership using `ls -ld` and `chown`

### Notes
- Parameter expansion is faster and safer than external commands
- `bc` requires variables to be expanded (e.g. `echo "$BIGNUM / 16" | bc`)
- `++I` increments before evaluation, `I++` increments after evaluation
- Scripts must have execute permission to run directly
- `~/bin` is a standard location for personal scripts included in `PATH`
