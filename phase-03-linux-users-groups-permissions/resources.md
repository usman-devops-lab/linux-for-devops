# Phase 3 - Resources

This file contains the resources and practice references I used during Phase 3 of my Linux for DevOps learning journey.

In this phase, I practiced Linux administration-related commands such as package management, users, groups, permissions, compression, and file transfer.

---

## Main Learning Resource

**Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi**

I continued learning from the same Linux for DevOps course and practiced the commands covered in this phase.

---

## Practice Environment

I practiced these commands using:

| Environment          | Purpose                                               |
| -------------------- | ----------------------------------------------------- |
| Local Linux Terminal | Practicing commands directly                          |
| Ubuntu System        | Running user, group, package, and permission commands |
| GitHub               | Documenting my learning                               |
| Hashnode             | Writing learning articles                             |
| LinkedIn             | Sharing learning progress                             |

---

## Handwritten Notes

I also prepared handwritten notes for this phase before documenting everything properly on GitHub.

* [Phase 3 Handwritten Notes](./handwritten-notes/phase-03-handwritten-notes.pdf)

---

## Topics Practiced

* System information commands
* Package management using `apt`
* User management
* Group management
* File permissions
* File ownership
* Default permissions using `umask`
* Compression using `zip`, `gzip`, `gunzip`, and `tar`
* File transfer using `scp`

---

## Useful Manual Commands

These commands can be used to read Linux manual pages:

```bash
man uname
man uptime
man useradd
man passwd
man userdel
man groupadd
man gpasswd
man groupdel
man chmod
man chown
man chgrp
man umask
man zip
man gzip
man gunzip
man tar
man scp
```

---

## Useful Help Commands

```bash
useradd --help
passwd --help
userdel --help
groupadd --help
gpasswd --help
chmod --help
chown --help
chgrp --help
tar --help
scp --help
```

---

## DevOps Use Case

These commands are useful for real Linux server administration.

As a DevOps learner, I need to understand how to install packages, create users, manage groups, control file access, compress files, and transfer files securely between systems.

These are basic but important skills before moving deeper into cloud, automation, Docker, Kubernetes, and CI/CD tools.

---

## Security Reminder

Sensitive files should never be uploaded to GitHub.

Do not upload:

```text
*.pem
*.key
.env
```

These should be added to `.gitignore`.

Example:

```gitignore
*.pem
*.key
.env
```

---

## Phase 3 Status

Phase 3 resources added successfully.
