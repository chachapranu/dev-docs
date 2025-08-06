# The Kernel's Job

The kernel is the heart of the operating system. It is the first program to load when you boot the computer, and it has complete control over the hardware. Its primary purpose is to act as a secure and fair intermediary between applications and the hardware.

Think of the kernel as the government of the computer. It doesn't do the useful work itself (that's for the applications), but it creates the laws and infrastructure that allow everything else to function smoothly and safely.

### The Four Core Functions

1.  **Process Management:** The kernel is the ultimate puppet master. It manages the lifecycle of **processes** (running applications). It decides which process gets to use the CPU, for how long (**scheduling**), and what to do when a process wants to sleep, wake up, or terminate. This ensures that even on a computer with one CPU, you can run many programs at once (concurrently) without any single one locking up the system.

2.  **Memory Management:** The kernel is a meticulous accountant for the system's memory (RAM). It gives each process its own private section of memory, creating a **virtual address space**. This is a crucial concept: the process thinks it has all the memory to itself. This prevents a buggy program from crashing other programs or, even worse, the kernel itself. The kernel manages the mapping between these virtual addresses and the physical RAM chips.

3.  **Device Management:** The kernel is the sole entity that is allowed to talk directly to the hardware (disks, network cards, GPUs, etc.). It does this through **drivers**. It exposes a simple, unified interface to applications so they don't have to worry about the specific hardware they are running on. For example, an application doesn't need to know whether it's writing to a SATA SSD or an NVMe drive; it just tells the kernel to "write this data to this file."

4.  **System Calls & Security:** The kernel provides the only legitimate way for user-space applications to request services, such as creating a new process or opening a file. This is done through **system calls**. This is the fundamental security boundary of the OS. By forcing all requests to go through this controlled interface, the kernel can check permissions and ensure that the application is allowed to do what it's asking to do.

[Back to The Kernel](./index.md)