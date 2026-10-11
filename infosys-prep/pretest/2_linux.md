# Linux / Unix — Infosys SP L1 Pre-Test

[← Back to Pre-Test Roadmap](./README.md)

## Table of Contents

- [How to use this file](#how-to-use-this-file)
- [1. Shell, terminal and filesystem basics](#1-shell-terminal-and-filesystem-basics)
- [2. Paths and directory navigation](#2-paths-and-directory-navigation)
- [3. Listing, viewing and manipulating files](#3-listing-viewing-and-manipulating-files)
- [4. Wildcards, quoting and expansion](#4-wildcards-quoting-and-expansion)
- [5. grep, find and text processing](#5-grep-find-and-text-processing)
- [6. Redirection and pipes](#6-redirection-and-pipes)
- [7. Permissions and ownership](#7-permissions-and-ownership)
- [8. Processes and jobs](#8-processes-and-jobs)
- [9. Environment variables and exit status](#9-environment-variables-and-exit-status)
- [10. Archives, disk and system information](#10-archives-disk-and-system-information)
- [11. Bash scripts and conditionals](#11-bash-scripts-and-conditionals)
- [12. High-yield command traps](#12-high-yield-command-traps)
- [13. Practice MCQs](#13-practice-mcqs)
- [14. Study schedule and checklist](#14-study-schedule-and-checklist)
- [References](#references)

## How to use this file

Practise commands in a Linux shell (WSL is fine) and use safe sample files. Do not experiment with destructive commands on important directories. The exact Infosys question pattern is not confirmed, so prepare both command selection and command behavior.

## 1. Shell, terminal and filesystem basics

A **terminal** is the interface, a **shell** interprets commands, and the **kernel** manages hardware and system resources. Bash is a common shell. Linux is an operating-system kernel used by many distributions.

Common commands:
- `pwd`: print working directory.
- `whoami`: print effective username in typical interactive use.
- `uname -a`: kernel/system information.
- `man command`: manual page.
- `command --help`: often displays brief usage.

Commands are programs, shell built-ins, aliases, or functions. Use `type cd` or `type ls` to inspect how the shell resolves a name.

[↑ Back to TOC](#table-of-contents)

## 2. Paths and directory navigation

An absolute path starts from root `/`; a relative path is interpreted from the current directory. `.` refers to the current directory and `..` to its parent. A path beginning with `~` usually expands to the current user's home directory in Bash.

Commands:
- `cd /tmp`: change directory.
- `cd ..`: move to parent.
- `mkdir -p a/b`: create nested directories.
- `rmdir empty_dir`: remove an empty directory.
- `realpath file`: resolve a path when installed.

Remember: `cd` changes the shell's current directory, so it must normally be a shell built-in. A child process cannot change its parent shell's working directory.

[↑ Back to TOC](#table-of-contents)

## 3. Listing, viewing and manipulating files

- `ls -la`: list files, including hidden entries, with details.
- `touch file`: create an empty file if absent or update timestamps.
- `cp source dest`: copy.
- `mv old new`: move or rename.
- `rm file`: remove a file.
- `cat file`: print contents.
- `less file`: browse interactively.
- `head -n 5 file` / `tail -n 5 file`: show first/last lines.
- `wc -l file`: count newline characters/lines as reported by the utility.

Be careful: `>` truncates a regular output file before writing; `rm` can delete files without putting them in a graphical recycle bin. Commands and flags can differ slightly across Unix-like systems.

[↑ Back to TOC](#table-of-contents)

## 4. Wildcards, quoting and expansion

In Bash, common patterns:
- `*.py`: names matching the pattern in the current directory.
- `file?.txt`: one character in the `?` position.
- `[abc]`: one matching character from the set.

Single quotes largely preserve characters literally. Double quotes still permit parameter expansion (such as `$HOME`) and command substitution. Backslash escapes selected characters.

```bash
echo "$HOME"
echo '$HOME'
```

The first usually prints the home-directory path; the second prints the literal text `$HOME`.

Unquoted variables can undergo word splitting and pathname expansion. Prefer `"$variable"` unless splitting/globbing is intentionally needed.

[↑ Back to TOC](#table-of-contents)

## 5. grep, find and text processing

- `grep "error" app.log`: search for matching lines.
- `grep -i "error" app.log`: ignore case.
- `grep -n "error" app.log`: show line numbers.
- `grep -r "TODO" src/`: recursively search (implementation-specific options exist).
- `find . -name "*.py"`: find matching names below the current directory.
- `sort names.txt`: sort lines.
- `uniq`: collapse adjacent duplicate lines; commonly pair with `sort` to count repeated lines.
- `cut -d, -f2 data.csv`: select a delimiter-separated field in simple cases.
- `tr`: translate/delete characters.

Shell globs and `find -name` patterns are not identical to full regular expressions. Quote a pattern such as `"*.py"` when you need `find` to receive the wildcard rather than having the shell expand it first.

[↑ Back to TOC](#table-of-contents)

## 6. Redirection and pipes

- `>`: redirect standard output, replacing/truncating the target file.
- `>>`: append standard output.
- `<`: use a file as standard input.
- `2>`: redirect standard error.
- `|`: send standard output of the left command to standard input of the right command.
- `2>&1`: duplicate standard error to the current standard output destination (ordering matters).

Example:
```bash
grep "ERROR" app.log | wc -l
```

This counts the matching output lines from `grep`.

`command >out.txt 2>&1` typically sends both output streams to the file. In contrast, `command 2>&1 >out.txt` redirects standard error to the output destination that existed before standard output is changed, so it behaves differently.

[↑ Back to TOC](#table-of-contents)

## 7. Permissions and ownership

A typical `ls -l` permission string looks like `-rwxr-xr--`: file type followed by permissions for owner, group and others. The basic permissions are read (`r`), write (`w`) and execute (`x`).

Numeric values: read = 4, write = 2, execute = 1. Add them per category:
- `chmod 755 script.sh`: owner `rwx`, group and others `r-x`.
- `chmod 640 file.txt`: owner `rw-`, group `r--`, others no permissions.
- `chmod u+x script.sh`: add execute permission for owner.

`chown` changes ownership where permitted. Directory execute permission means traversal/search access; read permission allows listing names, subject to other conditions. The effective access can also be affected by ACLs, mount options and privileges.

[↑ Back to TOC](#table-of-contents)

## 8. Processes and jobs

- `ps`: display process information.
- `top`: interactive process monitor.
- `kill PID`: send SIGTERM by default on common systems; it requests termination.
- `kill -9 PID`: send SIGKILL; cannot be caught or handled by the target process.
- `jobs`: list shell jobs.
- `command &`: run a command asynchronously in the shell.
- `Ctrl+C`: usually sends an interrupt to the foreground process group.
- `Ctrl+Z`: usually suspends the foreground job.

A process ID (PID) identifies a process. Do not assume that `kill` immediately removes a process: SIGTERM can be handled or ignored, and a process may take time to exit.

[↑ Back to TOC](#table-of-contents)

## 9. Environment variables and exit status

- `echo "$HOME"`: print the home variable.
- `export NAME=value`: make a variable available to child processes.
- `PATH`: directories searched for executable commands.
- `$?`: exit status of the last foreground command.
- In common shell convention, status 0 means success; non-zero usually signals failure.

```bash
false
echo $?
```

Output: `1` in Bash for this example.

A normal child process cannot set an environment variable in its parent shell. An exit status of 0 does not mean the output is useful; it means the command reports success.

[↑ Back to TOC](#table-of-contents)

## 10. Archives, disk and system information

- `tar -czf archive.tar.gz folder/`: create a gzip-compressed tar archive.
- `tar -xzf archive.tar.gz`: extract such an archive.
- `df -h`: filesystem space.
- `du -sh folder/`: approximate space used by a path.
- `free -h`: memory information on Linux.
- `date`: display date/time.
- `history`: show shell command history in common interactive shells.

Understand the difference between filesystem capacity (`df`) and space attributed to a directory tree (`du`). Flags may vary by platform, so check the local manual page when using non-Linux Unix systems.

[↑ Back to TOC](#table-of-contents)

## 11. Bash scripts and conditionals

A basic Bash script starts with a shebang such as `#!/usr/bin/env bash`. Run a script using `bash script.sh` or make it executable and run it directly when permissions and the shebang allow.

Example:
```bash
#!/usr/bin/env bash
name="Sai"
if [ "$name" = "Sai" ]; then
  echo "hello"
fi
```

In `[ ... ]`, spaces around brackets are significant. Use `=` for string comparison in portable `test` syntax; numeric comparison often uses `-eq`, `-lt`, and related operators. Learn `&&`, `||`, `if`, `case`, `for`, `while`, and positional parameters such as `$1`.

[↑ Back to TOC](#table-of-contents)

## 12. High-yield command traps

1. `>` replaces/truncates; `>>` appends.
2. `grep` searches file content; `find` searches directory entries.
3. `chmod 755` is not the same as `chmod 644`.
4. `kill` sends a signal; it is not synonymous with force-kill.
5. `$?` is the previous command's exit status and can be overwritten by the next command.
6. Single quotes prevent variable expansion in Bash; double quotes allow it.
7. `find . -name "*.txt"` should keep the pattern quoted.
8. A pipe passes stdout, not automatically stderr.
9. `uniq` only detects adjacent duplicates.
10. `cd` affects the current shell.
11. `df` reports filesystem capacity; `du` reports usage of paths.
12. Permission bits have different implications for files and directories.
13. `rm -r` is destructive; practise only on a disposable directory.
14. The order of redirections matters.
15. Command options can differ between GNU/Linux and BSD/macOS.

[↑ Back to TOC](#table-of-contents)

## 13. Practice MCQs

### Q1. Search text

Which command searches for `warning` in `system.log`?

A. `chmod warning system.log`  
B. `grep "warning" system.log`  
C. `cd warning system.log`  
D. `mkdir warning system.log`

**Answer: B.**

### Q2. Append output

Which operator appends stdout to a file?

A. `>`  
B. `>>`  
C. `|`  
D. `<`

**Answer: B.**

### Q3. Permissions

What do `chmod 640 report.txt` permissions give the owner?

A. Read only  
B. Read and write  
C. Read, write and execute  
D. No permissions

**Answer: B.**

### Q4. Exit status

What does exit status 0 conventionally indicate?

A. Failure  
B. Success  
C. A process ID  
D. A signal number

**Answer: B.**

### Q5. Duplicate lines

What is a common way to count repeated lines in a file?

A. `uniq -c file` always counts all duplicates regardless of position  
B. `sort file | uniq -c`  
C. `chmod file`  
D. `pwd file`

**Answer: B.** Sorting first groups identical lines.

### Q6. Find files

Which command searches below the current directory for names ending in `.log`?

A. `grep .log`  
B. `find . -name "*.log"`  
C. `chmod "*.log"`  
D. `cd "*.log"`

**Answer: B.**

### Q7. Signal

What does `kill -9 PID` send on typical Unix-like systems?

A. SIGTERM  
B. SIGKILL  
C. SIGSTOP only  
D. No signal

**Answer: B.**

### Q8. Variable expansion

Which command prints the literal characters `$HOME` in Bash?

A. `echo "$HOME"`  
B. `echo '$HOME'`  
C. `echo $HOME`  
D. `pwd $HOME`

**Answer: B.**

### Q9. Filesystem capacity

Which command reports filesystem free/used space in a readable format?

A. `df -h`  
B. `grep -h`  
C. `chmod -h`  
D. `cd -h`

**Answer: A.**

### Q10. Pipe

By default, what does the pipe `|` pass from the left command to the right command?

A. Standard input  
B. Standard output  
C. Standard error only  
D. Environment variables

**Answer: B.**

[↑ Back to TOC](#table-of-contents)

## 14. Study schedule and checklist

### Recommended two-week pass

- **Days 1–3:** navigation, paths, file operations and viewing files.
- **Days 4–5:** wildcards, quoting, grep/find and text processing.
- **Days 6–8:** redirection, pipes, permissions and ownership.
- **Days 9–10:** processes, environment variables and exit status.
- **Days 11–12:** archives, system information and shell scripts.
- **Days 13–14:** mixed questions, command drills and review.

### Checklist

- [ ] I can explain common commands without looking them up.
- [ ] I can predict redirection and pipe behavior.
- [ ] I can translate numeric permission modes.
- [ ] I understand signals, processes, jobs and exit codes.
- [ ] I can use grep and find for different tasks.
- [ ] I use safe sample directories for practice.
- [ ] I score at least 85% on two fresh quizzes.

[↑ Back to TOC](#table-of-contents)

## References

- [Linux man-pages](https://www.kernel.org/doc/man-pages/)
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [GNU Coreutils manual](https://www.gnu.org/software/coreutils/manual/)
- [GNU Findutils manual](https://www.gnu.org/software/findutils/manual/)
- [Pro Git book](https://git-scm.com/book/en/v2)

[← Back to Pre-Test Roadmap](./README.md)
