# Users and Permissions: A Multi-User World

Linux was designed from the ground up to be a **multi-user** system. This is not just a feature; it's a core part of its security and administrative model. Every process and every file on the system is owned by a **user** and a **group**.

### Why Does This Matter?

This model provides **isolation and security**. It prevents users from interfering with each other's files and processes, and it protects the core system files from being damaged by regular users.

### The Key Players

*   **User:** An account that can own files and run processes. You are logged in as a user. The most powerful user is **`root`**, which is the system administrator account. The `root` user can bypass all permission checks.
*   **Group:** A collection of users. Groups provide a way to manage permissions for multiple users at once. For example, you could create a `developers` group and give it write access to a project directory.

### The Three Levels of Permissions

For every file and directory, there are three sets of permissions you can define:

1.  **User (Owner):** What the owner of the file can do.
2.  **Group:** What members of the file's group can do.
3.  **Other:** What everyone else can do.

### The Three Types of Permissions

For each of the levels above, you can grant or deny three basic permissions:

*   **Read (`r`):**
    *   On a file: Allows viewing the contents of the file.
    *   On a directory: Allows listing the contents of the directory (e.g., with `ls`).
*   **Write (`w`):**
    *   On a file: Allows modifying or deleting the file.
    *   On a directory: Allows creating, deleting, or renaming files within the directory (regardless of the permissions on the files themselves!).
*   **Execute (`x`):**
    *   On a file: Allows running the file as a program or script.
    *   On a directory: Allows entering the directory (e.g., with `cd`). You must have execute permission on a directory to access any files within it.

### How it All Comes Together

When you try to access a file, the kernel performs a series of checks:

1.  Are you the **owner** of the file? If yes, the kernel looks at the **user** permissions and stops. If you have the required permission, the access is granted; otherwise, it's denied.
2.  If you are not the owner, are you a member of the file's **group**? If yes, the kernel looks at the **group** permissions and stops. If you have the required permission, access is granted; otherwise, it's denied.
3.  If you are neither the owner nor in the group, the kernel looks at the **other** permissions. If you have the required permission, access is granted; otherwise, it's denied.

This simple but powerful system is the foundation of security on Linux.

[Back to The User Space](./index.md)