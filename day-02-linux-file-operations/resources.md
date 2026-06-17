# Day 2 - Resources

This file contains the resources, tools, and references I used during Day 2 of my Linux for DevOps learning journey.

---

## Main Learning Resource

### YouTube Course

**Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi**

This course helped me understand and practice Linux commands from beginner to advanced level, especially commands that are useful for DevOps work.

---

## Practice Environment

I practiced Day 2 Linux commands using the following environments:

| Environment           | Purpose                                               |
| --------------------- | ----------------------------------------------------- |
| Local Linux Terminal  | Practicing basic Linux commands                       |
| Ubuntu System         | Running file, directory, and text processing commands |
| AWS EC2 Ubuntu Server | Practicing SSH and remote server access               |
| GitHub                | Documenting my learning publicly                      |
| Hashnode              | Writing a technical blog about my learning            |
| LinkedIn              | Sharing daily learning progress                       |

---

## Tools Used

* Linux terminal
* Ubuntu
* AWS EC2 instance
* SSH private key
* GitHub repository
* Markdown files
* Hashnode blog
* LinkedIn learning post

---

## Commands for Help and Documentation

Linux provides built-in help using the `man` command.

```bash
man ls
man cd
man mkdir
man touch
man cat
man head
man tail
man less
man more
man cp
man mv
man rm
man rmdir
man wc
man cut
man sort
man diff
man tee
man ln
man ssh
man chmod
man df
man du
man ps
man fuser
man free
man nohup
man vmstat
```

---

## Useful Help Commands

Check command options:

```bash
ls --help
cp --help
mv --help
rm --help
wc --help
cut --help
sort --help
diff --help
ssh --help
df --help
du --help
free --help
vmstat --help
```

---

## Important Linux Documentation Topics

These topics are useful for revision:

* File and directory management
* File viewing commands
* Text processing commands
* Hard links and soft links
* File permissions
* SSH access
* Disk usage monitoring
* Memory monitoring
* Process monitoring
* Background processes

---

## DevOps Use Cases

The commands practiced on Day 2 are useful in real DevOps tasks.

| Task                          | Useful Commands               |
| ----------------------------- | ----------------------------- |
| Checking server files         | `ls`, `cd`, `pwd`             |
| Reading logs                  | `cat`, `head`, `tail`, `less` |
| Copying config files          | `cp`                          |
| Moving or renaming files      | `mv`                          |
| Removing temporary files      | `rm`, `rmdir`                 |
| Checking file size and lines  | `wc`                          |
| Extracting data from files    | `cut`                         |
| Sorting log or text data      | `sort`                        |
| Comparing config files        | `diff`                        |
| Saving command output         | `tee`                         |
| Connecting to server          | `ssh`                         |
| Checking disk space           | `df`, `du`                    |
| Checking memory               | `free`                        |
| Checking processes            | `ps`, `fuser`                 |
| Monitoring system performance | `vmstat`                      |

---

## Security Reminder

Private keys and secret files should never be uploaded to GitHub.

Do not upload:

```text
*.pem
*.key
.env
```

These files should be added to `.gitignore`.

Example:

```gitignore
*.pem
*.key
.env
```

---

## Learning Reminder

Linux is the foundation of DevOps. Before learning tools like Docker, Kubernetes, Jenkins, Terraform, and Ansible, it is important to become comfortable with Linux commands, file management, SSH, and system monitoring.

---

## Status

Day 2 resources added successfully.
