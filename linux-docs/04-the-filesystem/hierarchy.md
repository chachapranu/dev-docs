# The Filesystem Hierarchy

While "everything is a file," these files are not just thrown together randomly. They are organized into a standard, tree-like structure called the **Filesystem Hierarchy**. Having a standard layout is crucial because it allows software to know where to find things, and it allows users to know where to put things.

The single root of this tree is `/`.

### The Most Important Directories

Here is a tour of the most important top-level directories and their purpose. Understanding this layout is essential for navigating a Linux system.

*   **/bin (Essential User Binaries):**
    *   **What:** Contains the essential commands (`ls`, `cp`, `mv`, `cat`, etc.) needed for the system to function, even in single-user mode. These are the fundamental tools.
    *   **Why:** They are kept separate from other programs in `/usr/bin` so that if the `/usr` partition fails to mount, the system can still be booted and repaired.

*   **/sbin (Essential System Binaries):**
    *   **What:** Similar to `/bin`, but contains programs that are intended to be run by the system administrator (`root`), such as `fdisk`, `mkfs`, and `ifconfig`.

*   **/etc (Etcetera / Configuration):**
    *   **What:** Contains system-wide configuration files. This is where you will find files that control how the system boots, how networking is configured, and how services are started.
    *   **Why:** Centralizing configuration makes managing the system much easier. There is no central registry like in Windows; configuration is stored in human-readable text files.

*   **/home (User Home Directories):**
    *   **What:** Contains a home directory for each user on the system (e.g., `/home/alice`, `/home/bob`). This is where users store their personal files, documents, and user-specific configuration (in hidden "dotfiles" like `.bashrc`).
    *   **Why:** Separating user data from the rest of the OS makes backups and upgrades much easier.

*   **/var (Variable Files):**
    *   **What:** Contains data that is expected to grow and change as the system runs. This includes log files (`/var/log`), mail spools (`/var/mail`), and web server content (`/var/www`).
    *   **Why:** Separating this volatile data from the more static OS files in `/usr` prevents a runaway log file from filling up the entire disk and crashing the system.

*   **/usr (Unix System Resources):**
    *   **What:** This is one of the largest directories. It contains the majority of user-land applications and data. This includes non-essential binaries (`/usr/bin`), libraries (`/usr/lib`), and documentation (`/usr/share/doc`).
    *   **Why:** Historically, this was the directory for everything related to the user, as opposed to the core system. It can be thought of as the "read-only" part of the OS that is shared among all users.

*   **/tmp (Temporary Files):**
    *   **What:** A directory for programs to store temporary files. The contents of this directory are often deleted on reboot.

*   **/dev (Device Files):**
    *   **What:** Contains the special device files that represent hardware, as explained in the "everything is a file" concept.

*   **/proc (Process Filesystem):** and **/sys (System Filesystem):**
    *   **What:** These are not real directories on disk. They are virtual filesystems created by the kernel in memory to expose information about processes and the system's hardware.

[Back to The Filesystem](./index.md)