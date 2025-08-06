# Processes: The Units of Execution

A **process** is the kernel's abstraction for a running program. It's more than just the program's code; it's a complete, self-contained environment for that code to execute in.

### What Makes Up a Process?

When the kernel creates a process, it bundles together several key resources:

*   **An Address Space:** A private slice of virtual memory that the process can use. From the process's point of view, it has a clean, linear block of memory all to itself. This is a powerful illusion maintained by the kernel.
*   **File Descriptors:** A list of the "files" the process has open. This could be actual files on disk, but it could also be the keyboard, a network connection, or a pipe to another process, thanks to the "everything is a file" philosophy.
*   **A Program Counter:** This keeps track of which instruction in the program is currently being executed.
*   **A Stack:** A region of memory used for local variables and function calls.
*   **A Heap:** A region of memory for dynamically allocated data.
*   **Security Context:** Information about the user and group that own the process, which determines its permissions.

### The `fork()` and `exec()` Model

Linux creates new processes in a unique and powerful two-step way:

1.  **`fork()`:** A process can make a `fork()` system call, which tells the kernel to create a nearly identical copy of itself. The new process (the **child**) has a copy of the parent's memory, file descriptors, etc. The only difference is that it has a new, unique Process ID (PID).

2.  **`exec()`:** After forking, the child process often wants to run a *different* program. The `exec()` system call replaces the child's current memory and code with a new program loaded from disk. The PID stays the same.

**Why this two-step process?** It's incredibly flexible. It allows the parent process to modify the environment of the child before the new program is executed. For example, a shell can `fork()`, set up file redirections (`> output.txt`), and then `exec()` the new program. The new program doesn't need to know anything about redirection; it just writes to its standard output, which the kernel has already pointed to the file.

This is how the shell works. When you type `ls -l`, the shell `forks()`, the child process calls `exec("/bin/ls", "-l")`, and the parent process usually waits for the child to complete.

[Back to The Kernel](./index.md)