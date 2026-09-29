# Day 1 & 2: Linux Processes and Bash Scripting

## Day 1: Processes

### What I built
Hands-on practice managing Linux processes: listing all running processes, filtering for a specific service, monitoring live resource use, and starting/stopping background processes both gracefully and forcefully.

### Commands used
- `ps aux` — list all running processes
- `ps aux | grep ssh` — filter for a specific process
- `top` — live view of resource usage
- `sleep 300 &` — start a background process
- `jobs` — list background jobs in the current session
- `kill <PID>` — gracefully stop a process
- `kill -9 <PID>` — force-stop a process immediately
- `ps -ef` — view processes with parent process IDs (PPID)

### What I learned
Every running process has a unique PID. `kill` sends a polite stop signal the process can respond to; `kill -9` forces an immediate stop with no cleanup. Every process has a parent (PPID) — unusual or unexplained process chains are one of the first things checked when investigating a potentially compromised system.

## Day 2: Bash Scripting

### What I built
A Bash script combining variables, conditional logic (`if`), and loops (`for`) — including a loop that reads real usernames from the system instead of a hardcoded list.

### What broke
Typed a multi-line `if` block directly into the terminal prompt instead of into the script file. This caused a `command not found` error from hidden characters — the logic itself was correct. Fixed by always editing multi-line scripts inside `nano`, never typing them raw at the prompt. Also had a case where new content got pasted above old content in the same file instead of replacing it — fixed by clearing the file and rewriting it in one clean pass, then verifying with `cat`.

### Commands used
```bash
#!/bin/bash

name="Sipho"
echo "Hello, $name"

count=1
if [ $count -gt 3 ]
then
    echo "count is more than 3"
fi

for user in Sipho Thabo Naledi
do
    echo "Hello, $user"
done

for user in $(cat my_users_list.txt)
do
    echo "Checking user: $user"
done
```

### What I learned
Scripts belong in files, not typed line-by-line at a prompt. `if` only runs its block when the condition is true. `for` loops repeat an action across a list, and combining a loop with `$(cat file)` means processing real, live data instead of values typed by hand.
