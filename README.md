1. Understanding the Linux shell
A shell is a program that accepts commands from a user and executes them.

Think of it this way:
- Linux kernel: manages the computer's hardware and resources.
- Shell: accepts your commands and communicates with the operating system.
- Terminal: the interface through which you interact with the shell.
Examples of shells include:
- Bash
- Zsh
- Fish
- Dash
Important: Linux and Unix-like systems, including macOS, use shells. Windows also has command-line environments, such as PowerShell.
2. Files and directory navigation
Linux organises files in a single directory tree beginning at /, called the root directory.








blog.kubesimplify.com


Know these commands:
Command	Purpose
pwd	Displays current directory
ls	Lists files and directories
ls -l	Displays detailed file information
ls -a	Displays hidden files too
cd	Changes directory
cd ..	Moves one directory up
cd ~	Moves to your home directory
find	Searches for files and directories

Absolute vs relative paths
- Absolute path: starts at /.
- Relative path: starts from your current directory.
Example:
cd /var/log


This is an absolute path.
cd Documents


This is a relative path.

Finding files ending in .log:
find /var/log -type f -name "*.log"


Remember:
- -type f means regular files.
- -name specifies the filename pattern.
- *.log matches filenames ending in .log.
Files beginning with a dot, such as .bashrc, are hidden files.
3. Searching text with grep
grep searches for patterns in text and displays matching lines.
grep error app.log


Important options:
Command	Meaning
grep -i	Ignore uppercase/lowercase differences
grep -n	Show matching line numbers
grep -r	Search recursively through directories
grep -v	Show lines that do NOT match
grep -E	Use extended regular expressions

Examples:
grep error app.log


Finds lines containing error.
grep -i error app.log


Finds error, ERROR, Error, etc.
grep -n error app.log


Displays matching lines with their line numbers.
grep -v error app.log


Displays lines that do not contain error.

Exam trap: -v does not mean verbose. It inverts the match.
4. Streams, redirection and pipes
Every Linux command has three standard streams:
Stream	Number	Purpose
Standard input (stdin)	0	Receives input
Standard output (stdout)	1	Displays normal output
Standard error (stderr)	2	Displays error messages

Learn these operators carefully.

| Syntax | What it does |
|---|---|
| > | Redirects output, overwriting a file |
| >> | Appends output to a file |
| 2> | Redirects error messages |
| 2>&1 | Sends stderr to the same destination as stdout |
| | | Sends one command's output to another command |

Examples:
ls > files.txt


Saves normal output and overwrites files.txt.
ls >> files.txt


Adds output to the end of files.txt.
ls /wrongpath 2> errors.txt


Saves error messages in errors.txt.
ls /wrongpath > output.txt 2>&1


Redirects both standard output and standard error to output.txt.

Pipes

A pipe connects commands.
grep error app.log | wc -l


This searches for lines containing error and counts the matching lines.
ls -l | less


This lets you browse long output page by page.

Remember: > redirects output to a file. | sends output to another command.
5. Processes and process management
A process is a running instance of a program.
Command	Purpose
ps	Displays a snapshot of running processes
top	Displays continuously updating process information
kill	Sends a signal to a process
command &	Runs a command in the background
echo $?	Displays the previous command's exit status

Important differences:

ps versus top
- ps: one-time snapshot.
- top: continuously updating live display.
Example:
ps aux


Displays running processes.
top


Shows live system and process activity.
sleep 100 &


Starts a sleep process in the background.
kill 1234


Sends the default termination signal to process ID 1234.

Exit status

This is particularly important for scripting.
echo $?


- 0 means success.
- Any nonzero value means failure or another condition.
Example:
ls
echo $?


If ls succeeds, the result should be 0.
6. Linux permissions
Linux permissions control who can access files and directories.

There are three permission types:
Permission	Symbol	Numeric value
Read	r	4
Write	w	2
Execute	x	1

There are three permission categories:
- User/owner (u)
- Group (g)
- Others (o)
Example:
-rwxr-xr--


Breakdown:
- Owner: rwx = read, write, execute.
- Group: r-x = read and execute.
- Others: r-- = read only.
Numeric permissions
Number	Permissions
7	rwx
6	rw-
5	r-x
4	r--
3	-wx
2	-w-
1	--x
0	---

For example:
chmod 755 script.sh


Means:
- Owner: 7 = rwx
- Group: 5 = r-x
- Others: 5 = r-x
Another example:
chmod 644 file.txt


Means owner can read and write, while group and others can only read.

Symbolic permissions:
chmod +x script.sh


Adds execute permission.
chmod u-w file.txt


Removes write permission from the owner.

The 15 facts I would memorise tonight
1. The shell interprets and executes commands.
2. / is the root of the Linux filesystem.
3. pwd displays the current working directory.
4. ls -a displays hidden files.
5. find searches for files and directories.
6. grep searches text.
7. grep -v inverts a search.
8. stdin is 0, stdout is 1, stderr is 2.
9. > overwrites, while >> appends.
10. 2> redirects errors.
11. | connects commands.
12. ps provides a process snapshot.
13. top provides a live process view.
14. Exit status 0 means success.
15. chmod 755 gives the owner full permissions and gives group and others read and execute permissions.
