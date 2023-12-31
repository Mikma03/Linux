- [[#Processes - intro|Processes - intro]]
- [[#Kill|Kill]]


## Processes - intro

A **process** in Linux is an instance of an executing program. When a program runs, it's loaded from the disk into the memory, and the kernel handles its execution. Each process is assigned a unique process ID (PID) by the system. The process that initiates another process is its parent, and the new process is the child. The first process, `init` (or `systemd` in many modern systems), has a PID of 1 and is the ancestor of all other processes.

**Here are some of the common commands used for interacting with processes in Linux**:

1. **ps**: This is one of the most basic commands for viewing the currently running processes. The command provides information about a selection of the active processes. `ps -aux` provides a more detailed view. The options `-a`, `-u`, and `-x` tell ps to list processes that belong to all users, provide detailed information, and include processes with no controlling terminal, respectively.
    
2. **top**: This command provides a live, real-time view of the running system. It shows system summary information and a list of processes currently being managed by the kernel. You can interact with the display, for example, to change the sort order, or to kill processes.
    
3. **htop**: This is an improved version of top, with a more user-friendly interface, color highlighting, and easier usage. It is not installed by default on all Linux distributions but is widely available for installation from repositories.
    
4. **pstree**: This command shows the running processes as a tree. The tree visualizes the parent-child relationship between processes.
    
5. **bg**: This command resumes suspended jobs in the background.
    
6. **fg**: This command moves a job running in the background to the foreground.
    
7. **jobs**: This command lists all jobs running in the background.
    
8. **kill**: This command is used to terminate a process manually. You need to know the PID of the process to use this command. For example, `kill 1234` will send a TERM signal to process 1234. If the process doesn't terminate after this (if it's stuck or ignoring the signal), you can use `kill -9 1234` to send a KILL signal, which will terminate the process immediately.
    
9. **killall**: This command terminates all processes with a certain name. For example, `killall firefox` would terminate all processes named "firefox".
    
10. **nice**: This command is used to run a program with modified scheduling priority. A lower nice value means higher priority.
    
11. **renice**: This command is used to change the priority of a running process.
    
12. **nohup**: This command is used to run a process that continues running even after the user has logged out.
    

These commands provide a basic toolkit for managing and interacting with processes on your Linux system. They are especially useful for system administration tasks, such as monitoring system load, killing unresponsive processes, and adjusting process priorities.


## Kill

  
The `kill` command in Linux is used to send a particular signal to a process. The default signal is `SIGTERM` (15). When you use the `kill` command without any signal specification, it sends the `SIGTERM` signal, requesting a process to terminate. However, a process is allowed to ignore this signal. Here are some common signals that you can use with the `kill` command:

1. **SIGTERM (15)**: This is the default signal sent by the `kill` command. It requests a process to terminate itself in a graceful manner, cleaning up resources in use before it exits.
    
2. **SIGKILL (9)**: This signal is used when a process is not responding to a `SIGTERM` signal or when a process needs to be terminated immediately. It forces the process to stop executing immediately. Processes cannot ignore this signal.
    
3. **SIGINT (2)**: This signal is sent when you press `Ctrl+C` in the terminal. It tells the process to terminate itself. This is similar to `SIGTERM`.
    
4. **SIGSTOP (19)**: This signal pauses the process. It's similar to `Ctrl+Z` but it can't be caught or ignored.
    
5. **SIGCONT (18)**: If a process is paused, you can continue its execution by sending the `SIGCONT` signal.
    
6. **SIGHUP (1)**: This signal is sent to a process when its controlling terminal is closed. It was originally designed to notify the process that the user had disconnected, but it's often used to instruct daemons to reload their configuration files.
    

Here is how you can use `kill` with a signal:

```bash
kill -SIGTERM 1234   # sends SIGTERM to process 1234
kill -SIGKILL 1234   # sends SIGKILL to process 1234
```

You can also use the signal numbers instead of their names:

```bash
kill -15 1234   # sends SIGTERM to process 1234
kill -9 1234    # sends SIGKILL to process 1234
```

You can view all available signals using `kill -l`:

```bash
kill -l
```

You'll see output similar to this (may vary by system):

 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM


Remember, be cautious when using `kill`, especially with the `-9` option, as it can lead to data loss or other unexpected behavior due to its abrupt nature.

