# Phase 3 - Linux Commands

This file contains all commands I practiced in Phase 3 of my Linux for DevOps journey.

Phase 3 focused on system information, package management, user and group management, permissions, compression, and file transfer.

## 1. System Information Commands

```bash
uname
uname -a
uptime
date
who
whoami
id
```

### Purpose

These commands help check basic system and user information.

## 2. Directory and System File Checking

```bash
ls
ls -l
ls -la
pwd
cd /etc
cd /home
cd /root
cd /usr
```

Check important Linux system files:

```bash
cat /etc/passwd
cat /etc/group
```

View only first few lines:

```bash
head /etc/passwd
head /etc/group
```

View last few lines:

```bash
tail /etc/passwd
tail /etc/group
```

---

## 3. Package Management Commands

Update package list:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Install a package:

```bash
sudo apt install tree
sudo apt install nginx
sudo apt install docker.io
```

Search for a package:

```bash
apt search nginx
apt search docker
```

Show package information:

```bash
apt show nginx
apt show docker.io
```

Remove a package:

```bash
sudo apt remove nginx
sudo apt remove docker.io
```

Remove unused packages:

```bash
sudo apt autoremove
```

Check installed package:

```bash
dpkg -l
dpkg -l | grep nginx
dpkg -l | grep docker
```

---

## 4. Other Linux Package Managers

Ubuntu/Debian:

```bash
sudo apt update
sudo apt install package-name
sudo apt remove package-name
```

Red Hat/CentOS/Fedora:

```bash
sudo yum install package-name
sudo yum remove package-name
```

Fedora/RHEL newer versions:

```bash
sudo dnf install package-name
sudo dnf remove package-name
```

Arch Linux:

```bash
sudo pacman -S package-name
sudo pacman -R package-name
```

---

## 5. User Management Commands

Create a user:

```bash
sudo useradd username
```

Create a user with home directory:

```bash
sudo useradd -m username
```

Set or change user password:

```bash
sudo passwd username
```

Switch user:

```bash
su username
```

Check current user:

```bash
whoami
```

Check user ID and group information:

```bash
id username
```

Delete a user:

```bash
sudo userdel username
```

Delete a user with home directory:

```bash
sudo userdel -r username
```

---

## 6. Group Management Commands

Create a group:

```bash
sudo groupadd devops
```

Add user to group:

```bash
sudo gpasswd -a username devops
```

Remove user from group:

```bash
sudo gpasswd -d username devops
```

Set group members:

```bash
sudo gpasswd -M user1,user2 devops
```

Check group file:

```bash
cat /etc/group
```

Search group:

```bash
grep devops /etc/group
```

Delete a group:

```bash
sudo groupdel devops
```

---

## 7. File Permission Checking

Check file permissions:

```bash
ls -l
ls -la
```

Example output:

```text
-rw-r--r-- 1 user user 120 Jun 23 file.txt
```

Permission meaning:

```text
r = read
w = write
x = execute
```

User categories:

```text
u = user/owner
g = group
o = others
a = all
```

---

## 8. chmod Commands

Give execute permission to owner:

```bash
chmod u+x script.sh
```

Remove execute permission from owner:

```bash
chmod u-x script.sh
```

Give read and write permission to owner:

```bash
chmod u+rw file.txt
```

Give read permission to group:

```bash
chmod g+r file.txt
```

Remove write permission from group:

```bash
chmod g-w file.txt
```

Give read permission to others:

```bash
chmod o+r file.txt
```

Remove all permission from others:

```bash
chmod o-rwx file.txt
```

Give execute permission to all:

```bash
chmod a+x script.sh
```

---

## 9. Numeric chmod Permissions

Read, write, execute values:

```text
read    = 4
write   = 2
execute = 1
```

Common permission examples:

```bash
chmod 777 file.txt
chmod 755 script.sh
chmod 644 file.txt
chmod 600 private.txt
chmod 400 key.pem
```

Meaning:

```text
777 = full permission for user, group, and others
755 = full permission for owner, read/execute for group and others
644 = read/write for owner, read-only for group and others
600 = read/write only for owner
400 = read-only for owner
```

---

## 10. Ownership Commands

Change file owner:

```bash
sudo chown username file.txt
```

Change file owner and group:

```bash
sudo chown username:groupname file.txt
```

Change directory ownership recursively:

```bash
sudo chown -R username:groupname foldername
```

---

## 11. Group Ownership Commands

Change group ownership:

```bash
sudo chgrp groupname file.txt
```

Change group ownership recursively:

```bash
sudo chgrp -R groupname foldername
```

Check ownership:

```bash
ls -l
```

---

## 12. umask Commands

Check current umask:

```bash
umask
```

Set temporary umask:

```bash
umask 022
umask 027
umask 077
```

Create file and check default permission:

```bash
touch file.txt
ls -l file.txt
```

Create directory and check default permission:

```bash
mkdir test-dir
ls -ld test-dir
```

---

## 13. Compression Commands - zip

Create a zip file:

```bash
zip files.zip file1.txt file2.txt
```

Zip a folder:

```bash
zip -r backup.zip foldername
```

Extract a zip file:

```bash
unzip files.zip
```

---

## 14. Compression Commands - gzip and gunzip

Compress a file using gzip:

```bash
gzip file.txt
```

Decompress a gzip file:

```bash
gunzip file.txt.gz
```

Check compressed file:

```bash
ls -l
```

---

## 15. Archive Commands - tar

Create tar archive:

```bash
tar -cvf archive.tar foldername
```

Extract tar archive:

```bash
tar -xvf archive.tar
```

Create compressed tar archive:

```bash
tar -czvf archive.tar.gz foldername
```

Extract compressed tar archive:

```bash
tar -xzvf archive.tar.gz
```

List files inside tar archive:

```bash
tar -tvf archive.tar
```

---

## 16. File Transfer Commands - scp

Copy local file to remote server:

```bash
scp file.txt username@server-ip:/home/username/
```

Copy remote file to local system:

```bash
scp username@server-ip:/home/username/file.txt .
```

Copy folder to remote server:

```bash
scp -r foldername username@server-ip:/home/username/
```

Use private key with scp:

```bash
scp -i key.pem file.txt ubuntu@server-public-ip:/home/ubuntu/
```

---

## 17. File Transfer Commands - rsync

Copy file using rsync:

```bash
rsync file.txt username@server-ip:/home/username/
```

Copy folder using rsync:

```bash
rsync -av foldername/ username@server-ip:/home/username/foldername/
```

Use rsync with SSH key:

```bash
rsync -av -e "ssh -i key.pem" foldername/ ubuntu@server-public-ip:/home/ubuntu/foldername/
```

---

## 18. Safe Commands Before Deleting

Check files before deleting:

```bash
ls
ls -l
pwd
```

Remove file:

```bash
rm file.txt
```

Remove empty directory:

```bash
rmdir foldername
```

Remove directory with content:

```bash
rm -r foldername
```

Use with care:

```bash
rm -rf foldername
```

---

## 19. Helpful Commands for Practice

Clear terminal:

```bash
clear
```

Check command path:

```bash
which command-name
```

Check command manual:

```bash
man command-name
```

Examples:

```bash
man useradd
man chmod
man chown
man tar
man scp
```

Get command help:

```bash
command-name --help
```

Examples:

```bash
useradd --help
chmod --help
tar --help
scp --help
```

---

## 20. Security Reminder

Never upload sensitive files to GitHub.

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

---

## Phase 3 Completed

In this phase, I practiced Linux system commands, package management, users, groups, permissions, compression, and file transfer commands.
