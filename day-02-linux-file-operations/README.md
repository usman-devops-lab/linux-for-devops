# Day 2 - Linux File Operations, Text Processing, SSH, and System Monitoring

## Overview

On Day 2 of my Linux for DevOps journey, I practiced important Linux commands used for managing files, directories, text data, links, remote server access, and basic system monitoring.

This day helped me understand how Linux commands are used in real DevOps workflows, especially when working with servers, logs, files, and system resources.

## Topics Covered

* File and directory creation
* Reading file content
* Copying, moving, and deleting files
* Viewing large files
* Word, line, and byte counting
* Hard links and soft links
* Extracting fields from text files
* Sorting and comparing files
* Saving command output into files
* SSH login to a remote Ubuntu server
* Disk, memory, and process monitoring

## Commands Practiced

| Category          | Commands                                             |
| ----------------- | ---------------------------------------------------- |
| Navigation        | `pwd`, `ls`, `cd`                                    |
| File Creation     | `touch`, `cat`, `echo`                               |
| File Reading      | `cat`, `head`, `tail`, `less`, `more`                |
| File Management   | `cp`, `mv`, `rm`, `rmdir`                            |
| Text Processing   | `wc`, `cut`, `sort`, `diff`, `tee`                   |
| Links             | `ln`, `ln -s`                                        |
| Editor            | `vi`                                                 |
| Remote Login      | `ssh`, `chmod`                                       |
| System Monitoring | `df`, `du`, `ps`, `fuser`, `free`, `nohup`, `vmstat` |

## Key Learnings

* `touch` is used to create empty files.
* `cat`, `head`, `tail`, `less`, and `more` are used to read file content.
* `cp` copies files and folders, while `mv` moves or renames them.
* `rm` deletes files, and `rm -r` deletes folders with content inside.
* `wc` counts lines, words, and bytes in a file.
* `cut` extracts specific fields from structured text.
* `tee` displays output on the terminal and saves it to a file.
* `sort` sorts lines alphabetically or numerically.
* `diff` compares two files and shows differences.
* Hard links and soft links are useful for file referencing.
* SSH is used to connect to remote Linux servers.
* `df`, `du`, `free`, `ps`, and `vmstat` help monitor Linux system resources.

## Practice Highlights

Today I created files and folders, practiced copy/move/delete operations, worked with text files, created hard and soft links, sorted file content, compared files, and connected to an AWS Ubuntu server using SSH.

## Important DevOps Reminder

Never upload private key files such as `.pem` files to GitHub. Sensitive files should always be added to `.gitignore`.

## Status

Day 2 completed successfully.
