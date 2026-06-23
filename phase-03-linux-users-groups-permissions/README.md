# Phase 3: Linux Users, Groups, Permissions, Package Management, Compression, and File Transfer

## Overview

In Phase 3 of my Linux for DevOps learning journey, I practiced important Linux commands related to system information, package management, user and group management, file permissions, compression, and file transfer.

This phase was more practical because these commands are used regularly when managing Linux servers, installing tools, handling users, controlling access, and transferring files between systems.

---

## Topics Covered

* Basic system information commands
* Linux package management
* User management
* Group management
* File ownership
* File permissions
* Default permissions using `umask`
* Compression and archive commands
* File transfer using `scp`

---

## Commands Practiced

| Category           | Commands                                                       |
| ------------------ | -------------------------------------------------------------- |
| System Information | `uname`, `uptime`, `date`, `who`, `whoami`, `id`               |
| Package Management | `apt`, `apt update`, `apt install`, `apt remove`, `apt search` |
| User Management    | `useradd`, `passwd`, `su`, `userdel`                           |
| Group Management   | `groupadd`, `gpasswd -a`, `gpasswd -d`, `groupdel`             |
| File Permissions   | `ls -l`, `chmod`, `umask`                                      |
| Ownership          | `chown`, `chgrp`                                               |
| Compression        | `zip`, `gzip`, `gunzip`, `tar`                                 |
| File Transfer      | `scp`                                                          |

---

## What I Practiced

In this phase, I practiced checking system details, managing Linux packages, creating and deleting users, creating groups, adding users to groups, removing users from groups, changing file permissions, changing ownership, compressing files, extracting archives, and transferring files between systems.

I also practiced commands that are useful for real DevOps tasks, especially when working with servers, users, permissions, packages, and files.

---

## Key Learnings

* `uname` shows system information.
* `uptime` shows how long the system has been running.
* `whoami` shows the current logged-in user.
* `id` shows user ID, group ID, and group membership.
* `apt` is used to manage packages on Ubuntu/Debian-based systems.
* `useradd` is used to create a new user.
* `passwd` is used to set or change a user password.
* `groupadd` is used to create a new group.
* `gpasswd -a` adds a user to a group.
* `gpasswd -d` removes a user from a group.
* `chmod` changes file permissions.
* `chown` changes file ownership.
* `chgrp` changes group ownership.
* `umask` controls default permissions for newly created files and directories.
* `zip`, `gzip`, `gunzip`, and `tar` are used for compression and archiving.
* `scp` is used to securely copy files between systems.

---

## DevOps Use Case

These commands are important for DevOps because Linux servers require proper package installation, secure user access, correct file permissions, and safe file transfer.

For example, when working on a server, a DevOps engineer may need to install tools, create users, assign permissions, manage groups, compress logs, or copy files from one system to another.

---

## Files in This Phase

```text
phase-03-linux-users-groups-permissions/
├── README.md
├── commands.md
├── errors-and-fixes.md
├── resources.md
└── handwritten-notes/
```

---

## Status

Phase 3 completed successfully.
