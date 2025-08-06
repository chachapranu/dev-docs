# System Calls: The Kernel's API

A system call is the fundamental way that a user-space program asks the kernel to perform a privileged action on its behalf.

### The User/Kernel Divide

The CPU has different modes of operation. At a minimum, there are two: **user mode** and **kernel mode**.

*   **User Mode:** This is a restricted mode. Code running in user mode cannot directly access hardware or talk to devices. Your web browser, your text editor, and the games you play all run in user mode.
*   **Kernel Mode:** This is the privileged, all-powerful mode. The kernel runs in this mode. Code running in kernel mode has unrestricted access to all hardware.

This separation is the primary security boundary in the OS. If user programs could talk to hardware directly, they could crash the system, read data from other programs, or wipe the disk.

### Crossing the Boundary

So how does a user-space program do something useful, like open a file? It has to ask the kernel. The mechanism for this is the **system call**.

Here's the process:

1.  The user-space program (usually via a library function like `open()` from the C library) sets up the arguments for the system call (e.g., the filename and the desired access mode).
2.  It then executes a special instruction (`syscall` or `int 0x80` on older x86 systems) that causes a **trap**. A trap is a hardware event that immediately switches the CPU from user mode to kernel mode and jumps to a specific, predefined location in the kernel's code.
3.  The kernel's **system call handler** takes over. It looks at the arguments the user program provided.
4.  It performs a series of checks. For example, for an `open()` call, it checks if the user has permission to access the requested file.
5.  If the checks pass, the kernel performs the requested action (e.g., interacts with the disk driver to open the file).
6.  The kernel then prepares a return value (e.g., a file descriptor or an error code).
7.  The kernel executes a special instruction to return from the trap, which switches the CPU back to user mode and returns control to the user-space program.

This is a deliberate, carefully controlled process. It's like going through a security checkpoint. You can't just wander into a secure area; you have to present your request to a guard, who checks your credentials and performs the action for you.

The `strace` command is a powerful tool that lets you watch all the system calls a program makes. Running `strace ls` is an eye-opening experience that shows you what's really happening under the hood.

[Back to The Kernel](./index.md)