# Processes

## Viewing Processes

To list all processes currently running on the system, you can use the following command:

```
ps -e
```

This command provides a basic list of processes.

If you need more detailed information about each process, you can use:

```
ps aux --sort -%mem
```

This command provides a more comprehensive view, including details such as memory and CPU usage.

##Monitoring Processes
For real-time monitoring of processes, you can use the top command:

```
top
```

top displays a dynamic view of system processes, updating periodically. It provides information such as CPU and memory usage.

Within top, you can press:

- M to sort processes by memory usage.
- P to sort processes by CPU usage.
- N to sort processes by PID (Process ID).

## Parent Processes
Every process in Linux has a parent process. When you execute a command from the terminal, the shell becomes the parent process of that command.

For example, running:

```
sleep 3
```

starts the sleep command as a child process of the shell.

##Running Processes in the Background
You can run processes in the background by appending & to the command. For instance:

```
sleep 5000 &
```

This command starts the sleep process in the background, allowing you to continue using the terminal.

To view background jobs, you can use:

```
jobs
```

This command lists the background jobs currently running.

For more detailed information about background jobs, including their PID (Process ID), you can use:
```
sleep 3000 &
jobs -l
```

## Terminating Processes
To terminate a process, you need to know its PID. You can find the PID of a process using ps or top. Once you have the PID, you can use the kill command to terminate it.

For example, to terminate a process with PID 1289, you would use:

```
kill 1289
```
Sometimes, a process may not respond to the standard termination signal. In such cases, you can force it to terminate using:

```
kill -9 PID
```
Replace PID with the actual Process ID.

This Markdown document provides an overview of basic Linux process management commands and concepts.
