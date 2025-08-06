# Block Devices vs. Character Devices

Linux divides the world of devices into two fundamental types: **block devices** and **character devices**. This distinction is based on how data is accessed and transferred.

### Block Devices

*   **What they are:** A block device is a piece of hardware that reads and writes data in fixed-size chunks called **blocks**. You can access any block on the device independently of the others.
*   **The key characteristic:** They are **addressable** or **seekable**. You can instantly jump to block number 5, then to block number 5000, and then back to block 200.
*   **Examples:**
    *   Hard Disk Drives (HDDs)
    *   Solid State Drives (SSDs)
    *   CD-ROM/DVD drives
    *   USB flash drives

Because you can seek to any position, block devices are the foundation for filesystems. A filesystem is a layer of software that maps files and directories onto the blocks of a block device.

When the kernel needs to read a file, the filesystem tells it which blocks contain the data, and the kernel can then command the block device to read those specific blocks.

### Character Devices

*   **What they are:** A character device is a piece of hardware that reads and writes data as a continuous **stream of bytes**, one character at a time.
*   **The key characteristic:** They are **not seekable**. They are a stream. You can't just jump to the 500th character from your keyboard; you have to read the first 499 characters first. The data is sequential.
*   **Examples:**
    *   Keyboards
    *   Mice
    *   Serial ports (`/dev/ttyS0`)
    *   Sound cards
    *   The null device (`/dev/null`), which just discards any data written to it.
    *   A random number generator (`/dev/urandom`), which produces an endless stream of random bytes.

### How to Tell the Difference

You can see the type of a device file by using `ls -l`:

```bash
# The 'b' at the beginning indicates a block device
ls -l /dev/sda
brw-rw---- 1 root disk 8, 0 Aug  4 12:34 /dev/sda

# The 'c' at the beginning indicates a character device
ls -l /dev/tty
crw-rw-rw- 1 root tty 5, 0 Aug  4 12:34 /dev/tty
```

This fundamental distinction allows the kernel to provide a consistent interface for each type of device. The `read()` and `write()` system calls work on both, but the underlying implementation by the driver is very different.

[Back to The Hardware](./index.md)