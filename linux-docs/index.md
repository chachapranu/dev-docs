# Linux from First Principles

This guide is designed to build your understanding of Linux from the ground up. We will explore the "why" behind the architecture and concepts, not just the "what" and "how." By the end of this guide, you will have a strong first-principle understanding of Linux.

## Table of Contents

*   **[The Big Picture](./01-the-big-picture/index.md)**
    *   [What is an Operating System?](./01-the-big-picture/what-is-an-os.md)
    *   [The Linux Philosophy](./01-the-big-picture/philosophy.md)
    *   [Why Linux is Everywhere](./01-the-big-picture/linux-everywhere.md)
*   **[The Kernel: The Core of Control](./02-the-kernel/index.md)**
    *   [The Kernel's Job](./02-the-kernel/job-of-the-kernel.md)
    *   [Processes: The Units of Execution](./02-the-kernel/processes.md)
    *   [Memory Management](./02-the-kernel/memory.md)
    *   [System Calls: The Kernel's API](./02-the-kernel/syscalls.md)
*   **[The User Space: Where We Live](./03-the-user-space/index.md)**
    *   [The Shell: Your Command Center](./03-the-user-space/shell.md)
    *   [Users and Permissions: A Multi-User World](./03-the-user-space/users-and-permissions.md)
    *   [The C Library: The Bridge to the Kernel](./03-the-user-space/glibc.md)
*   **[The Filesystem: Everything is a File](./04-the-filesystem/index.md)**
    *   [The "Everything is a File" Concept](./04-the-filesystem/everything-is-a-file.md)
    *   [The Filesystem Hierarchy](./04-the-filesystem/hierarchy.md)
    *   [Virtual Filesystems: procfs and sysfs](./04-the-filesystem/virtual-filesystems.md)
*   **[The Hardware: Talking to the World](./05-the-hardware/index.md)**
    *   [Drivers: The Translators](./05-the-hardware/drivers.md)
    *   [Block Devices vs. Character Devices](./05-the-hardware/block-vs-char.md)
    *   [The `/dev` Directory](./05-the-hardware/dev.md)