# User-Related Commands

## 1. Create a New User

```bash
sudo adduser <username>
```
- Replace `<username>` with the desired username.

## 2. Add User to a Group

```bash
sudo usermod -aG <groupname> <username>
```
- Example: Add user `alice` to the `sudo` group:
  ```bash
  sudo usermod -aG sudo alice
  ```

## 3. Set/Change User Password

```bash
sudo passwd <username>
```

## 4. Grant Sudo Permissions

To give a user sudo privileges, add them to the `sudo` group:

```bash
sudo usermod -aG sudo <username>
```

## 5. Remove a User

```bash
sudo deluser <username>
```

## 6. Remove a User and Their Home Directory

```bash
sudo deluser --remove-home <username>
```

## 7. List All Users

```bash
cut -d: -f1 /etc/passwd
```

## 8. List All Groups

```bash
cut -d: -f1 /etc/group
```

---

**Note:** Replace `<username>` and `<groupname>` with actual names as needed.