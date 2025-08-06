# Virtual Filesystems: procfs and sysfs

We've established that in Linux, everything is a file. But some of the most powerful "files" don't actually exist on your hard drive. These live in **virtual filesystems**, which are created by the kernel in memory and mounted on the filesystem just like a real one.

The two most important virtual filesystems are `procfs` (at `/proc`) and `sysfs` (at `/sys`). They are the kernel's way of presenting a massive amount of internal data and control knobs to the user space in a standard, file-based way.

### `procfs` - The Process Filesystem

*   **What it is:** `procfs` is a window into the state of the kernel and its running processes.
*   **How it works:** For every process running on the system, the kernel creates a directory in `/proc` named after the process ID (PID). For example, `/proc/1234` contains information about the process with PID 1234.

**What's inside?**

*   `/proc/1234/cmdline`: The command that was used to start the process.
*   `/proc/1234/status`: A detailed, human-readable summary of the process's state (memory usage, user ID, etc.). This is where tools like `top` and `ps` get their information.
*   `/proc/1234/fd/`: A directory containing links to the files that the process has open.

`procfs` also contains files that are not related to a specific process, but provide system-wide information:

*   `/proc/cpuinfo`: Information about the CPU.
*   `/proc/meminfo`: Detailed information about memory usage.
*   `/proc/uptime`: How long the system has been running.

By reading these files, you are directly reading data structures from within the kernel.

### `sysfs` - The System Filesystem

*   **What it is:** If `procfs` is about processes, `sysfs` is about **devices** and **drivers**. It provides a structured view of the system's hardware as seen by the kernel.
*   **How it works:** `sysfs` organizes devices into a hierarchy based on how they are connected to the computer. It shows the relationship between buses (like PCI or USB), devices, and the drivers that manage them.

**What's inside?**

The structure can be complex, but for example, you might find:

*   `/sys/class/net/`: A directory containing information about all the network interfaces on the system.
*   `/sys/class/power_supply/BAT0/`: Information about the system's battery, such as its current capacity.
*   `/sys/bus/pci/devices/`: A directory for all the devices connected to the PCI bus.

### Why are they so important?

`procfs` and `sysfs` are the ultimate expression of the "everything is a file" philosophy. They turn the abstract, internal state of the kernel into something that can be explored and manipulated with standard command-line tools like `cat`, `grep`, and `find`.

They provide the underlying data for a huge number of system utilities. Instead of creating a special tool to get memory info and another to get CPU info, Linux just exposes the data as files, and lets you use the tools you already know.

[Back to The Filesystem](./index.md)