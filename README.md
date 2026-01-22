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
    └── bin

```
## 📌 Note
I studied Linux consistently before starting this log.
Daily logging begins here to keep track of progress going forward.

# 📖 Learning Log

## **Entry 1**

### Focus: 
Searching files with find, Finding files by user, Finding files by permission, Finding files by date and time, Finding files and executing commands 

### Commands / Concepts: 
Working with text files,`find`, `mkdir`, `chmod`, `cd`,`-ctime`, `-perm`

### Practice:
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
    
### Notes / Issues:
- `chmod 777` grants full permissions to everyone
- `-ctime +300` finds files older than 300 days
- System directories like `/usr/share` often require elevated privileges
- Copying files from `/usr/share` to `/tmp/FILES` was unsuccessful due to permission restrictions
- Some files could not be accessed without `sudo`

## **Entry 2**

### Focus: 
File location, searching, directory creation, and copying files/directories

### Commands / Concepts:
- `locate` – quickly find files using the system database
- `find` – search files/directories by path and size
- `mkdir` – create directories
- `cp -r -a` – copy files/directories recursively while preserving attributes
- Absolute vs relative paths
- Navigating system directories (`/usr/share`, `/tmp`, home directory)

### Practice:
- Used locate to search for passwd and /tmp/FILES
- Created /tmp/FILES directory
- Used find to list files and search by size range
- Copied various system files (PDFs, .gir, .jar, .txt) from /usr/share into /tmp/FILES
- Verified copied files using find
- Copied selected files from /tmp/FILES into a hidden backup directory (.mybackup) in the home directory

### Notes / Issues:
- locate may return no results if the database is not updated
- Some cp commands initially failed due to incorrect paths
- Learned the importance of using full absolute paths when copying system files
- Confirmed successful file transfers by listing contents after copying

## **Entry 3**

### Focus: 
Managing running processes, understanding processes, listing processes

### Command / Concepts: 
- `ps u`
- `ps ux | less`
- `ps uax | less`
- `ps -eo`
- listing and changing processes with htop
    
### Practice:
- List all processes running on my system, showing a full set of columns
  - `ps u`
- sort those processes by the name of the user
  - `ps u --sort=-user | less`
- List all display the following columns: process ID, username, group name, virtual memory size, resident memory size, and the command.
  - `ps -eo pid,user,group,vsz,rss,comm | head`
- Run the htop command to view processes running on my system. Go back and forth between CPU and memory.
  - `htop` - M keybind to switch to memory
        
### Notes / Issues:
- VSZ shows the size of the image process, the amount of memory allocated for the process.
- RSS shows the size of the program in memory, the amount that is actually being used.
    
## **Entry 4**

### Focus: 
Starting background processes, Killing and renicing processes

### Command / Concepts:
`jobs`, `fg %`,`bg %`, `nice`, `renice`, `kill`, `killall`

### Practice:
- Used `kill -SIGSTOP <pid>` to pause the `gedit` process
- Ran `gedit` with an initial nice value of 5 using the `nice` command 
- Using the `renice` command change value to 7
- Verified the updated nice value using the `top` command
    
### Notes / Issues: 
- SIGSTOP immediately pauses a process and cannot be ignored by the process
- Lower nice values give a process higher priority, while higher nice values lower its priority
- Only privileged users can decrease a nice value (increase priority)
- The top command displays the current nice value under the NI column
jobs, fg, and bg only work with processes started from the current shell

## **Entry 5**

### Focus:
Executing and degbugging shell scripts

### Commands / Concepts: 
`touch myscript`, `sudo vim myscript`, `bash -x myscript`

### Practice: 
- Created a script file using `touch myscript` in my home directory
- Edited the script multiple times with `sudo vim`
- Executed the script using `bash -x myscript` to trace commands line by line

### Notes: 
- `bash -x myscript` executes commands from a file
- `bash -x` prints each command before executing it, which is useful for debugging

## **Entry 6**

### Focus: 
Creating and executing a bash script, passing arguments, and running it via PATH.

### Commands / Concepts:
`mv`, `chmod 755`, Executable scripts $PATH, Positional parameters ($1, $2),`bash -x`, Variable defaults (${VAR:-default})

### Practice:
- Create a script named myscript
  - Used the read command to prompt the user for information and store that information to use later in the script.
- Make it executable
- Run the script with arguments (foo bar)
- Debug execution
- Rename and execute the script
- Typed commands in shell to test how parameter expansion works 
  - `${var:-value}`- uses value if var is unset or empty

### Notes:
- Script arguments are accessed using positional parameters:
- $1 → first argument (foo)
- $2 → second argument (bar)
- Arguments do nothing unless explicitly used inside the script.
- A script can be run without ./ only if it is located in a directory included in $PATH (e.g. ~/bin).
- chmod 755 myscript is required to allow direct execution.
- bash -x myscript prints each command as it runs and is useful for debugging.
- ${VAR:-"Not Set"} assigns a default value when a variable is unset or empty.
- File extensions like .sh are optional; execution depends on permissions and the shebang.

## **Entry 7**

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

## **Entry 8**

### Focus
Writing and debugging Bash scripts using conditional statements and the `test` command.

### Commands / Concepts
- `mkdir`, `cd`, `ls`
- `touch`
- `vim`
- `mv`
- `bash -x`
- `./scriptName`
- `if` / `then`
- `test`
-  File test operators: `-x`, `-w`
- `help test`

### Practice
- Created a `bin/` directory to store scripts
- Wrote multiple Bash scripts:
  - [scriptOne](https://github.com/ashtonguevarra/linux-learning/blob/main/bash-scripts/bin/scriptOne)
  - [scriptTwo](https://github.com/ashtonguevarra/linux-learning/blob/main/bash-scripts/bin/scriptTwo)
  - [scriptThree](https://github.com/ashtonguevarra/linux-learning/blob/main/bash-scripts/bin/scriptThree) 
- Edited scripts repeatedly in `vim` to correct syntax and logic
- Renamed scripts for naming consistency
- Used `bash -x` to trace execution and debug errors
- Executed scripts directly once working

### Notes
- `bash -x` is useful for step-by-step debugging
- Direct execution requires a proper shebang and execute permissions
- The `test` command is commonly used inside `if` statements to evaluate conditions

## **Entry 9**

### Focus

* Bash scripting fundamentals
* Conditional logic and control flow
* Loop constructs
* Script debugging with execution tracing
* File permissions and execution


### Commands / Concepts

* `cd`, `touch`, `mv`, `ls`, `chmod`
* `bash -x`
* Test operators: `-d`, `-e`
* if statements
* case statements
* for loops
* Shebang (#!/bin/bash)
* File permission modes (rwx)


### Practice

scriptFour

* Created a directory only if it did not already exist
* First execution created /tmp/testdir
* Subsequent executions detected the directory and skipped creation

scriptFive

* Checked for file existence
* Script always printed "already exists" due to a missing filename in the test condition
* Learned that test operators require valid variables or paths

scriptSix (renamed to caseCommand)

* Implemented a case statement using the output of date +%a
* Assigned different backup paths and tape devices based on the day
* Verified correct behavior using bash -x

forLoop

* Implemented a for loop to iterate over values
* Initial execution failed due to missing execute permissions
* Added a shebang and updated permissions to allow execution
* Used bash -x to trace loop execution
* Corrected invalid variable usage
* Final script executed successfully and produced repeated output


### Notes

* Scripts must include a shebang to be executed directly
* Execute permission is required when running scripts with ./script
* bash -x is useful for understanding execution flow and debugging

## **Entry 10**

### Focus
Practicing loop constructs (`while`, `until`), file permissions, script execution, debugging with `bash -x`, and using `grep` to inspect system and environment information.

### Commands / Concepts
- `cd`
- `touch`
- `chmod`
- `ls -l`
- `./scriptName`
- `bash -x`
- `while` loop
- `until` loop
- Numeric test operators: `-lt`, `-eq`
- `grep`
- `/etc/passwd`
- `env`
- Environment variables (`HOME`)
- `man grep`

### Practice
- Navigated to `~/bin` directory
- Created executable scripts:
  - `whileDo`
  - `untilLoop`
- Modified permissions using `chmod a+rwx` and `chmod u+rwx`
- Verified permissions with `ls -l`
- Executed scripts directly using `./scriptName`
- Used `bash -x` to trace loop execution step-by-step
- Observed loop counters incrementing from `0` to `9`

- Practiced `while` loop behavior using a less-than condition (`-lt`)
- Practiced `until` loop behavior using an equality condition (`-eq`)
- Encountered and corrected an invalid Bash option (`-X` vs `-x`)

- Used `grep` to search `/etc/passwd` for home directory entries
- Confirmed user home directory and login shell
- Used `env | grep` to filter environment variables by prefix
- Identified the `HOME` environment variable and related values
- Consulted `man grep` for command reference

### Notes
- `bash -x` prints each command as it executes, useful for debugging loops
- `while` loops run while the condition is true
- `until` loops run until the condition becomes true
- File permissions mus

## **Entry 11**

### Focus
Using `for` loops to process multiple files, renaming files safely, understanding script execution context, and debugging unexpected `mv` behavior.

### Commands / Concepts
- `cd`
- `ls -l`
- `vim`
- `chmod`
- `./scriptName`
- `bash -x`
- `for` loop
- Filename handling
- `mv`
- Wildcards (`*`)
- Script execution paths (`./script`, `./bin/script`)
- Current working directory context

### Practice
- Navigated to `~/bin`
- Created and edited scripts:
  - `touchScript`
  - `testScript`
- Verified execute permissions on `testScript`
- Executed `testScript` directly from inside `~/bin`
- Used `bash -x` to trace script execution

- Observed `for file in *` iterating over all files in the directory
- Used `tr` to replace whitespace with underscores in filenames
- Noted repeated warnings when source and destination filenames were identical
- Identified that `mv` reports errors when attempting to rename a file to itself

- Ran `testScript` from the home directory using `./bin/testScript`
- Observed unintended behavior where the script attempted to rename files and directories in `$HOME`
- Learned that wildcard expansion (`*`) depends on the current working directory
- Returned to `~/bin` to edit and correct the script logic

### Notes
- `for file in *` operates on the current directory, not the script’s directory
- Running a script from a different location can change its effects
- `bash -x` is essential for understanding loop behavior and command expansion
- Scripts that modify files should include safeguards to avoid acting on unintended directories
- Renaming logic should check whether source and destination filenames differ before calling `mv`

## **Entry 12**

### Focus
Using `sed` for text processing, stream editing and redirection, command history reuse, and building a simple Bash phone list utility with arguments, conditionals, and file storage.

### Commands / Concepts
- `sed`
- `touch`
- `cat`
- Redirection (`>`)
- Pipes (`|`)
- `rm`
- `history`, `!n`
- `grep`
- `vim`
- `chmod`
- Script arguments (`$1`, `$2`, `$3`)
- `shift`
- Conditional tests
- Exit codes
- `bash -x`

### Practice
- Used `sed -n '/home/p' /etc/passwd` to print matching lines
- Created temporary files for text manipulation practice
- Replaced strings using:
  - `sed 's/Mac/Linux/g'`
- Removed trailing whitespace using:
  - `sed 's/ *$//'`
- Redirected output to new files instead of modifying originals
- Compared direct `sed` usage vs piping input from `cat`
- Opened files in `vim` to verify changes
- Removed temporary files after testing
- Reused commands from history using `!n`
- Observed errors when running commands on deleted files

- Created a script named `telephoneList`, later renamed to `ph`
- Set executable permissions with `chmod`
- Executed the script interactively and via command-line arguments
- Implemented a phone list stored in `~/.phonelist.txt`
- Added new entries using:
  - `./ph new "Name" number`
- Queried existing entries using:
  - `./ph name`
- Used `grep -i` for case-insensitive searching
- Used `grep -q` to test for matches without output
- Debugged script logic using `bash -x`
- Verified correct behavior for missing and existing entries

### Notes
- `sed` processes input streams and does not modify files unless redirected
- Redirection (`>`) overwrites files; missing input files cause errors
- `!n` reruns a command from history by number
- Scripts should validate argument count before processing
- `shift` is useful for handling subcommands like `new`
- `bash -x` is essential for tracing script logic and argument handling
- Storing data in hidden files keeps user directories clean

## **Entry 13**

### Focus
Creating and executing a custom Bash script to display system information such as date, time, current directory, and hostname.

### Commands / Concepts
- `chmod`
- `./scriptName`
- Execute permissions (`755`)
- Command substitution
- `date`
- `pwd`
- `hostname`
- Environment awareness

### Practice
- Set execute permissions on a custom script using:
  - `chmod 755 myownscrpt`
- Executed the script directly from the terminal
- Displayed system information using a Bash script

#### Script: `myownscript`
```bash
# !/bin/bash
# Displays, date/time, current working directory, and hostname.

DATE=`date`
DIRECTORY=/home/ashton
HOST="abc.example.com"

echo "Today is $DATE."
echo "You are in $DIRECTORY and your host is $HOST."
   ```
## **Entry 14**

### Focus 
Understanding positional parameters by writing a shell script.

### Commands / Concepts
- `cd`
- `chmod 755`
- `./pp`
- `./pp par1 par2 par3`
- Positional Parameters (`$1`,`$2`,`$3`)
- Special Parameters (`$#`,`$@`)
- Setting variables
- Arguments in command line

### Practice
- Set execute permission on script `pp`
- Execute script from inside `~/bin`
- Write a Bash script that reads, counts, and displays three parameters

### Script

``` bash

#!/bin/bash 
# Script that reads in three special parameters in the command line

ONE=$1 
TWO=$2 
THREE=$3 
echo "There are $# parameters that include: $@" 
echo "The first is $ONE, the second is $TWO, the third is $THREE."

```

### Notes 
- Positional parameters are empty when arguments are not provided.

## **Entry 15**

### Focus
Using `read`, user input, and conditional statements in Bash scripting.

### Commands / Concepts
- `read`
- `echo`
- Variables
- `if`, `else`, `fi`
- String comparison (`=`)

### Practice
- Prompt the user for multiple inputs
- Store input in variables
- Use conditional logic to respond to user input

### Script 1: Street and Town Input

```bash
#!/bin/bash
# Prompts name of the street and town that you grew up on

read -p "Write the street and town you grew up on: " mystreet mytown

echo "The street I grew up on was $mystreet and the town was $mytown"
 
```
### Script 2:

``` bash
#!/bin/bash
# Asks your favorite operating system

read -p "Which is you favorite operating system? " OS

if [ $OS = "linux" ] ; then
    echo "you are a goat!"
else
    echo "not so gigachad of you lol"
fi

```

## **Entry 17**

### Focus
Using a **for loop** in Bash to iterate over a list of values and display formatted output.

### Commands / Concepts
- `for` loop 
- Loop variable 
- `do` / `done` 
- `bash -x` (debug mode)

### Practice
- Create a Bash script named `fltonee`
- Make the script executable
- Use a `for` loop to iterate through descriptive words
- Display output using a loop variable

### Script

```bash
#!/bin/bash
# a for loop for tonee

for TONEE in beautiful pretty pink sweet kind ; do
    echo "Tonee is $TONEE"
done
```

### Sample Output

``` bash
Tonee is beautiful
Tonee is pretty
Tonee is pink
Tonee is sweet
Tonee is kind
```

### Notes
- The for loop runs once for each word in the list.
- The variable TONEE stores the current value in each iteration.
- bash -x fltonee helps trace execution for debugging.

## **Entry 18**

### Focus
Managing system services using `systemctl` and checking logs through Cockpit.

### Commands / Concepts 
- `systemctl enable --now`
- Systemd services and sockets
- Root authentication
- `su` (switch user)
- Cockpit service
- Viewing system logs

### Practice 
- Enable and start the Cockpit socket
- Authenticate as root to manage system services
- Switch to root and exit safely
- Verify service activity and logs using Cockpit

### Commands Executed 

```bash
systemctl enable --now cockpit.socket
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-unit-files ====
Authentication is required to manage system service or unit files.
Authenticating as: root
==== AUTHENTICATION COMPLETE ====

```

``` bash
su
exit

```

### Notes

- enable --now enables the service at boot and starts it immediately
- Cockpit provides a web-based interface for monitoring and logs
- Always exit root after completing administrative tasks




