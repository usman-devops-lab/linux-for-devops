# Phase 3 - Errors and Fixes

This file contains the errors and small mistakes I faced while practicing Phase 3 Linux commands.

I am keeping this section because errors are part of real terminal practice. Sometimes the command works in notes, but while practicing it in the terminal, small things like permissions, spelling, missing packages, or wrong paths can create issues.

---

## 1. Permission Denied While Accessing System Directories

### What happened

While checking system directories like `/root` or protected files, I noticed that normal users do not always have permission to access everything.

Example:

```bash
cd /root
```

or:

```bash
cat /etc/shadow
```

### Why it happened

Linux protects important system files and directories. A normal user cannot access everything because it can create security risks.

### Fix

Use `sudo` only when it is actually required:

```bash
sudo cat /etc/shadow
```

For normal practice, I used safe files like:

```bash
cat /etc/passwd
cat /etc/group
```

### What I learned

Linux permissions are strict for a reason. As a DevOps learner, I should understand when to use `sudo` and when not to use it.

---

## 2. Package Installation Needed `sudo`

### What happened

When installing packages, a normal user cannot install or remove system packages without admin permission.

Example:

```bash
apt install tree
```

### Why it happened

Installing packages changes the system, so Linux requires administrator privileges.

### Fix

Use:

```bash
sudo apt install tree
```

Before installing packages, update the package list:

```bash
sudo apt update
```

### What I learned

For package management on Ubuntu, commands like install, remove, and update usually need `sudo`.

---

## 3. Package Not Found or Package List Not Updated

### What happened

Sometimes a package may not install properly if the package list is old.

Example:

```bash
sudo apt install package-name
```

### Fix

First update the package list:

```bash
sudo apt update
```

Then install the package again:

```bash
sudo apt install package-name
```

To search for a package:

```bash
apt search package-name
```

### What I learned

Before installing software on Ubuntu, it is a good habit to run `sudo apt update`.

---

## 4. Switching User Without Setting Password

### What happened

While practicing user management, switching to a newly created user can fail if the password is not set.

Example:

```bash
su username
```

### Why it happened

The user was created, but the password was not configured yet.

### Fix

Set the password first:

```bash
sudo passwd username
```

Then switch user:

```bash
su username
```

### What I learned

Creating a user and setting a password are two separate steps.

---

## 5. Creating a User Without Home Directory

### What happened

I learned that using only `useradd` may create a user without a proper home directory.

Example:

```bash
sudo useradd testuser
```

### Better command

Create the user with a home directory:

```bash
sudo useradd -m testuser
```

Check the user:

```bash
id testuser
```

### What I learned

For normal user creation practice, `useradd -m` is better because it creates the user with a home directory.

---

## 6. Group Command Did Not Work Without Correct User or Group

### What happened

While practicing group management, commands can fail if the user or group name does not exist.

Example:

```bash
sudo gpasswd -a testuser devops
```

### Why it happened

Either the user was not created yet, or the group was not created yet.

### Fix

Create the group first:

```bash
sudo groupadd devops
```

Create or confirm the user:

```bash
id testuser
```

Add user to group:

```bash
sudo gpasswd -a testuser devops
```

Verify:

```bash
groups testuser
```

or:

```bash
grep devops /etc/group
```

### What I learned

Before adding a user to a group, both the user and group should exist.

---

## 7. Confusion Between `gpasswd -a`, `gpasswd -d`, and `gpasswd -M`

### What happened

At first, group management options looked similar.

### Meaning

Add a user to a group:

```bash
sudo gpasswd -a username groupname
```

Remove a user from a group:

```bash
sudo gpasswd -d username groupname
```

Set group members directly:

```bash
sudo gpasswd -M user1,user2 groupname
```

### What I learned

`-a` adds, `-d` deletes from group, and `-M` sets group members.

---

## 8. Permission Changes Did Not Work Without Correct Syntax

### What happened

While practicing `chmod`, I had to understand symbolic and numeric permissions properly.

Examples:

```bash
chmod u+x script.sh
chmod g-w file.txt
chmod o-rwx file.txt
```

Numeric examples:

```bash
chmod 755 script.sh
chmod 644 file.txt
chmod 600 private.txt
```

### What I learned

In numeric permissions:

```text
read = 4
write = 2
execute = 1
```

So:

```text
7 = read + write + execute
6 = read + write
5 = read + execute
4 = read only
```

This made permission numbers easier to understand.

---

## 9. Ownership Change Needed `sudo`

### What happened

Changing file owner or group may fail for a normal user.

Example:

```bash
chown username file.txt
```

### Fix

Use:

```bash
sudo chown username file.txt
```

For owner and group:

```bash
sudo chown username:groupname file.txt
```

For group ownership:

```bash
sudo chgrp groupname file.txt
```

### What I learned

Ownership changes affect file access, so they usually require admin permission.

---

## 10. `umask` Was Confusing at First

### What happened

The `umask` command was a little confusing because it does not directly show permissions. It controls what permissions are removed from default permissions.

Check current umask:

```bash
umask
```

Set temporary umask:

```bash
umask 022
```

Then create a file and check permission:

```bash
touch test.txt
ls -l test.txt
```

### What I learned

`umask` controls default permissions for newly created files and directories. It is useful for understanding Linux security and default access control.

---

## 11. Compression Command Needed Correct Tool

### What happened

Different compression commands work differently, so it is important to choose the right one.

For zip:

```bash
zip files.zip file1.txt file2.txt
```

For gzip:

```bash
gzip file.txt
```

For tar archive:

```bash
tar -cvf archive.tar foldername
```

For compressed tar archive:

```bash
tar -czvf archive.tar.gz foldername
```

### What I learned

`zip` creates zip files, `gzip` compresses single files, and `tar` is commonly used to archive folders.

---

## 12. Extracting Archives Needed Correct Options

### What happened

While learning archive commands, I had to remember that creating and extracting use different options.

Create tar:

```bash
tar -cvf archive.tar foldername
```

Extract tar:

```bash
tar -xvf archive.tar
```

Create tar.gz:

```bash
tar -czvf archive.tar.gz foldername
```

Extract tar.gz:

```bash
tar -xzvf archive.tar.gz
```

### What I learned

In `tar`, `c` is for create and `x` is for extract.

---

## 13. SCP Requires Correct Path and Remote User

### What happened

While learning file transfer, I understood that `scp` needs the correct local path, remote user, server IP, and destination path.

Example:

```bash
scp file.txt username@server-ip:/home/username/
```

Using an SSH key:

```bash
scp -i key.pem file.txt ubuntu@server-public-ip:/home/ubuntu/
```

### What I learned

If the username, server address, key file, or destination path is wrong, `scp` will not work correctly.

---

## 14. Private Key Files Should Not Be Public

### What happened

While practicing SSH and SCP, I learned that private key files must be protected.

Private keys should not be uploaded to GitHub.

Do not upload:

```text
*.pem
*.key
.env
```

Add these to `.gitignore`:

```gitignore
*.pem
*.key
.env
```

### What I learned

Security is important in DevOps. A private key should always stay private.

---

## Final Learning

Phase 3 helped me understand that Linux administration is not only about running commands. It is also about knowing permissions, users, groups, packages, and safe access.

The errors I faced helped me understand the commands better, especially around `sudo`, users, groups, permissions, package management, compression, and file transfer.
