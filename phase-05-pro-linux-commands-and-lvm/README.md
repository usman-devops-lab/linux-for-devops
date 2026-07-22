# Phase 5: Pro Linux Commands and LVM for DevOps

This phase documents my learning and hands-on practice of **Pro Linux Commands** and **Linux Volume Management with LVM** for DevOps.

In this phase, I focused on powerful Linux text processing commands such as `grep`, `sed`, and `awk`. These commands are very important for working with logs, configuration files, command outputs, CSV files, monitoring data, and automation scripts.

I also studied Linux volume management concepts, AWS EBS, physical volumes, volume groups, logical volumes, mounting volumes, and extending logical volumes using LVM.

## Learning Source

This phase is based on:

**Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi**

I am learning Linux step by step and documenting important concepts, commands, notes, errors, fixes, handwritten notes, screenshots, and hands-on practice that are useful for DevOps, cloud infrastructure, automation, and server management.

## Phase 5 Focus

The focus of this phase is divided into two main parts:

## Part 1: Pro Linux Commands

- `grep`
- `sed`
- `awk`
- Regular expressions with `grep`
- Searching files and command output
- Editing and replacing text with `sed`
- Extracting and processing columns with `awk`
- Combining `grep`, `sed`, and `awk` using pipes
- DevOps use cases for logs, configuration files, monitoring, and automation

## Part 2: Linux Volume Management and LVM

- Introduction to Linux volumes
- Introduction to AWS EBS
- Physical volumes
- Volume groups
- Logical volumes
- Mounting volumes in Linux
- Managing AWS EBS on EC2 instances
- Introduction to LVM
- Using LVM with EBS for dynamic storage management
- Extending logical volumes

## Why This Phase Is Important for DevOps

DevOps engineers work with logs, configuration files, deployment files, monitoring output, command output, and server storage.

This phase is important because it helps in two major areas:

1. **Text processing and automation**
2. **Storage and volume management**

A DevOps engineer should know how to:

- Search application and system logs
- Find errors and warnings
- Extract useful information from command output
- Modify configuration files safely
- Process CSV and text files
- Automate deployment scripts
- Filter monitoring data
- Understand Linux storage
- Attach and mount AWS EBS volumes
- Create physical volumes, volume groups, and logical volumes
- Extend storage dynamically using LVM

# Part 1: Pro Linux Commands

## Simple Memory Trick

```text
grep = Search
sed  = Edit
awk  = Extract and process columns
```

# grep

`grep` stands for **Global Regular Expression Print**.

It searches for specific words, patterns, or regular expressions inside files or command output.

## Basic Syntax

```bash
grep [options] "pattern" filename
```

## Basic Example

```bash
grep "error" application.log
```

Meaning:

```text
Finds all lines containing the word error in application.log.
```

## Important grep Options

| Option | Purpose | Example |
|---|---|---|
| `-i` | Ignores uppercase and lowercase differences | `grep -i "error" application.log` |
| `-n` | Shows line numbers with matching lines | `grep -n "error" application.log` |
| `-v` | Shows lines that do not match the pattern | `grep -v "success" application.log` |
| `-c` | Counts matching lines | `grep -c "error" application.log` |
| `-w` | Matches complete word only | `grep -w "user" file.txt` |
| `-r` / `-R` | Searches recursively inside directories | `grep -r "database" /etc/` |
| `-l` | Shows only filenames containing a match | `grep -l "error" *.log` |
| `-L` | Shows filenames that do not contain the pattern | `grep -L "error" *.log` |
| `-A` | Shows lines after the matching line | `grep -A 3 "error" application.log` |
| `-B` | Shows lines before the matching line | `grep -B 3 "error" application.log` |
| `-C` | Shows lines before and after the match | `grep -C 2 "error" application.log` |
| `-E` | Enables extended regular expressions | `grep -E "error|warning" application.log` |
| `-F` | Searches fixed text instead of regex | `grep -F "192.168.1.10" access.log` |
| `--color=auto` | Highlights matching text | `grep --color=auto "error" application.log` |

## grep Regular Expressions

Regular expressions are patterns used for advanced searching.

| Pattern | Purpose | Example |
|---|---|---|
| `^` | Matches beginning of line | `grep "^ERROR" application.log` |
| `$` | Matches end of line | `grep "failed$" application.log` |
| `.` | Matches any single character | `grep "s.rv.r" file.txt` |
| `*` | Matches zero or more occurrences | `grep "go*d" file.txt` |
| `[Ee]` | Matches one character from group | `grep "[Ee]rror" application.log` |
| `[^0-9]` | Matches characters not in group | `grep "[^0-9]" file.txt` |
| `[0-9]` | Matches digits from 0 to 9 | `grep "[0-9]" file.txt` |
| `|` | Works as OR with `grep -E` | `grep -E "error|failed|warning" application.log` |

## Multiple Patterns with grep

Using multiple `-e` options:

```bash
grep -e "error" -e "warning" application.log
```

Using extended regular expression:

```bash
grep -E "error|warning" application.log
```
## Searching Command Output with grep

`grep` is frequently used with pipes.

```bash
ps aux | grep nginx
```

Meaning:

```text
Searches the process list for nginx.
```

```bash
systemctl list-units | grep running
```

Meaning:

```text
Shows running systemd units.
```

```bash
docker ps | grep nginx
```

Meaning:

```text
Searches running Docker containers for nginx.
```

## DevOps Uses of grep

DevOps engineers use `grep` to:

- Find errors in log files
- Search configuration files
- Check running processes
- Filter Docker and Kubernetes output
- Search deployment logs
- Find IP addresses and HTTP status codes
- Locate environment variables
- Check whether services are running

# sed

`sed` stands for **Stream Editor**.

It searches, replaces, deletes, inserts, and modifies text without opening the file in a text editor.

## Basic Syntax

```bash
sed [options] 'command' filename
```

## How sed Works

By default, `sed`:

1. Reads input line by line
2. Applies the specified operation
3. Prints the result on the terminal
4. Does not modify the original file unless `-i` is used

## Substitute Text

```bash
sed 's/old/new/' file.txt
```

Meaning:

```text
Replaces the first occurrence of old with new on each line.
```

## Substitute All Occurrences

```bash
sed 's/old/new/g' file.txt
```

Meaning:

```text
Replaces every occurrence of old with new.
```

The `g` means global replacement.

## Ignore Case

```bash
sed 's/error/issue/gI' application.log
```

Meaning:

```text
Replaces error, Error, or ERROR with issue.
```

## Modify the Original File

```bash
sed -i 's/old/new/g' file.txt
```

Meaning:

```text
Changes the original file directly.
```

## Important Warning

Always create a backup before editing an important configuration file.

```bash
sed -i.bak 's/old/new/g' file.txt
```

This creates:

```text
file.txt
file.txt.bak
```

## Print Specific Lines

Print only line 5:

```bash
sed -n '5p' file.txt
```

Print lines 5 to 10:

```bash
sed -n '5,10p' file.txt
```

## Delete Lines

Delete line 5:

```bash
sed '5d' file.txt
```

Delete lines 5 to 10:

```bash
sed '5,10d' file.txt
```

Delete lines containing `debug`:

```bash
sed '/debug/d' application.log
```

Modify the file directly:

```bash
sed -i '/debug/d' application.log
```

## Insert, Append, and Change Lines

Insert text before line 3:

```bash
sed '3i\new line added' file.txt
```

Append text after line 3:

```bash
sed '3a\new line added' file.txt
```

Change line 3 completely:

```bash
sed '3c\This is the replacement line' file.txt
```

## Use Pattern as Address

```bash
sed -n '/ERROR/p' application.log
```

Meaning:

```text
Prints lines matching ERROR.
```

Correct form with `-n` avoids duplicate output.

## Replace Text on Specific Lines

Replace only on line 5:

```bash
sed '5s/old/new/' file.txt
```

Replace from line 5 to line 10:

```bash
sed '5,10s/old/new/g' file.txt
```

## Delete Blank Lines

```bash
sed '/^$/d' file.txt
```

Meaning:

```text
Removes empty lines.
```

## Remove Leading Spaces

```bash
sed 's/^[[:space:]]*//' file.txt
```

## Remove Trailing Spaces

```bash
sed 's/[[:space:]]*$//' file.txt
```

## Remove Comments

Remove lines beginning with `#`:

```bash
sed '/^#/d' config.conf
```

Remove comments and blank lines:

```bash
sed '/^#/d; /^$/d' config.conf
```

## Use Another Delimiter

Normally `/` separates the search and replacement strings:

```bash
sed 's/old/new/g'
```

For paths and URLs, another delimiter is easier:

```bash
sed 's|/var/www/old|/var/www/new|g' file.txt
```

## Extended Regular Expressions

```bash
sed -E 's/error|warning/issue/g' file.txt
```

## Capturing Groups

```bash
sed -E 's/(user)=([^ ]+)/\1=hidden/' file.txt
```

Notes:

```text
\1 = first captured group
\2 = second captured group
```

## DevOps Uses of sed

DevOps engineers use `sed` to:

- Change ports in configuration files
- Update server names
- Replace environment values
- Delete comments and blank lines
- Modify deployment files
- Update version numbers
- Change URLs and paths
- Edit configuration files automatically in shell scripts

## Important sed Safety Rule

Before changing a production configuration file, test the command first:

```bash
sed 's/old/new/g' config.conf
```

Then use backup mode:

```bash
sed -i.bak 's/old/new/g' config.conf
```

This saves a backup.

# awk

`awk` is named after its creators:

```text
Aho, Weinberger, and Kernighan
```

`awk` processes text line by line and is mainly used to extract columns, filter records, calculate values, and create reports.

## Basic Syntax

```bash
awk 'pattern { action }' filename
```

Another common form:

```bash
command | awk '{ action }'
```

## How awk Reads Data

`awk` divides every line into fields or columns.

Example file:

```text
ali devops 50000
sara developer 60000
ahmed admin 45000
```

Fields:

```text
$1 = first column
$2 = second column
$3 = third column
$0 = complete line
```

## Print Complete Lines

```bash
awk '{print $0}' employees.txt
```

## Print First Column

```bash
awk '{print $1}' employees.txt
```

## Print Multiple Columns

```bash
awk '{print $1, $3}' employees.txt
```

## Important awk Built-in Variables

| Variable | Meaning |
|---|---|
| `$0` | Complete current line |
| `$1`, `$2`, `$3` | Individual fields |
| `NR` | Current line number |
| `NF` | Number of fields in current line |
| `$NF` | Last column |
| `$(NF-1)` | Second-last column |
| `FS` | Input field separator |
| `OFS` | Output field separator |
| `FILENAME` | Current filename |

## Print Line Number

```bash
awk '{print NR, $0}' file.txt
```

## Print Number of Fields

```bash
awk '{print NF}' file.txt
```

## Print Last Column

```bash
awk '{print $NF}' file.txt
```

## Print Second-Last Column

```bash
awk '{print $(NF-1)}' file.txt
```

## Field Separators

By default, `awk` separates fields using spaces or tabs.

Colon-separated data:

```bash
awk -F: '{print $1}' /etc/passwd
```

Comma-separated data:

```bash
awk -F, '{print $1, $3}' employees.csv
```

Pipe-separated data:

```bash
awk -F'|' '{print $1, $2}' file.txt
```

## Pattern Filtering with awk

Print lines containing `error`:

```bash
awk '/error/ {print $0}' application.log
```

Ignore case:

```bash
awk 'tolower($0) ~ /error/ {print}' application.log
```

Numeric condition:

```bash
awk '$3 > 50000 {print $1, $3}' employees.txt
```

String condition:

```bash
awk '$2 == "devops" {print $1}' employees.txt
```

Not equal:

```bash
awk '$2 != "admin" {print $0}' employees.txt
```

AND condition:

```bash
awk '$2 == "devops" && $3 > 40000 {print $1}' employees.txt
```

OR condition:

```bash
awk '$2 == "devops" || $2 == "admin" {print $1}' employees.txt
```

## BEGIN Block

`BEGIN` runs before `awk` reads the file.

```bash
awk 'BEGIN {print "DevOps Report"} {print $0}' file.txt
```

Commonly used to set separators:

```bash
awk 'BEGIN {FS=":"} {print $1}' /etc/passwd
```

## END Block

`END` runs after all lines have been processed.

```bash
awk 'END {print "Total lines:", NR}' file.txt
```

## Calculations with awk

Calculate total:

```bash
awk '{sum += $3} END {print "Total:", sum}' employees.txt
```

Calculate average:

```bash
awk '{sum += $3} END {print "Average:", sum/NR}' employees.txt
```

Count matching lines:

```bash
awk '/error/ {count++} END {print "Errors:", count}' application.log
```

Find maximum value:

```bash
awk 'NR == 1 || $3 > max {max = $3} END {print max}' employees.txt
```

Find minimum value:

```bash
awk 'NR == 1 || $3 < min {min = $3} END {print min}' employees.txt
```

## Formatting Output with printf

```bash
awk '{printf "User: %-10s Salary: %s\n", $1, $3}' employees.txt
```

Common format symbols:

| Symbol | Meaning |
|---|---|
| `%s` | String |
| `%d` | Integer |
| `%f` | Decimal number |
| `\n` | New line |
| `\t` | Tab |

## DevOps Uses of awk

DevOps engineers use `awk` to:

- Extract CPU and memory information
- Process access logs
- Analyze HTTP status codes
- Extract usernames from `/etc/passwd`
- Process CSV files
- Calculate totals and averages
- Extract columns from command output
- Generate monitoring reports
- Find disk usage values
- Process Docker and Kubernetes output

# Combining grep, sed, and awk

These commands become more powerful when used together with pipes.

## grep with awk

```bash
grep "ERROR" application.log | awk '{print $1, $2, $5}'
```

Meaning:

```text
Finds error lines and extracts selected columns.
```

## grep with sed

```bash
grep "ERROR" application.log | sed 's/ERROR/ISSUE/g'
```

Meaning:

```text
Finds error lines and changes the displayed word ERROR to ISSUE.
```

## sed with awk

```bash
sed '/^#/d' config.txt | awk '{print $1}'
```

Meaning:

```text
Removes comment lines and prints the first column.
```

## All Three Together

```bash
grep "ERROR" application.log | sed 's/ERROR/CRITICAL/g' | awk '{print $1, $2, $0}'
```

Meaning:

```text
grep finds error lines.
sed replaces ERROR with CRITICAL.
awk formats the final output.
```

## When to Use Which Command

| Command | Use When | Simple Meaning |
|---|---|---|
| `grep` | You need to find lines containing a word or pattern | Find text |
| `sed` | You need to replace, delete, or edit text | Change text |
| `awk` | You need to work with columns or calculations | Extract, filter, and calculate |

## DevOps Example Areas

## Log Analysis

```text
grep = find errors
sed  = clean or replace text
awk  = extract date, IP, status code, or message
```

## Configuration Management

```text
grep = check whether a setting exists
sed  = change the setting
awk  = extract configuration values
```

## Monitoring

```text
grep = filter important output
sed  = clean output
awk  = calculate and format values
```

## CI/CD Pipelines

```text
grep = detect success or failure
sed  = update versions and variables
awk  = produce reports
```

# Part 2: Linux Volume Management and LVM

Linux volume management helps manage storage on Linux servers.

In cloud environments like AWS, storage is commonly added using EBS volumes and attached to EC2 instances.

## Important Concepts

| Term | Meaning |
|---|---|
| Disk | Physical or virtual storage device |
| Partition | Divided section of a disk |
| Mount Point | Directory where storage is attached |
| AWS EBS | Elastic Block Store volume used with EC2 |
| PV | Physical Volume |
| VG | Volume Group |
| LV | Logical Volume |
| LVM | Logical Volume Manager |

## Normal Disk vs LVM

## Normal Disk

In normal disk management, a disk or partition is mounted directly.

Example:

```text
Disk → Filesystem → Mount Point
```

## LVM

In LVM, storage is managed in layers.

```text
Physical Volumes → Volume Group → Logical Volumes → Filesystem → Mount Point
```

This makes storage more flexible.

## Why LVM Is Useful

LVM is useful because it allows dynamic storage management.

DevOps engineers can:

- Combine multiple disks
- Create logical volumes
- Extend storage when needed
- Manage storage more flexibly
- Use AWS EBS volumes with Linux servers
- Resize storage without redesigning the whole disk layout

## Useful LVM Commands

## Check Block Devices

```bash
lsblk
```

## Check Disk Usage

```bash
df -h
```

## Install LVM

Ubuntu/Debian:

```bash
sudo apt update
sudo apt install lvm2
```

Amazon Linux/RHEL/CentOS:

```bash
sudo yum install lvm2
```

## Create Physical Volumes

```bash
sudo pvcreate /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1
```

Check physical volumes:

```bash
sudo pvs
sudo pvdisplay
```

## Create Volume Group

```bash
sudo vgcreate tws-vg /dev/nvme1n1 /dev/nvme2n1
```

Check volume groups:

```bash
sudo vgs
sudo vgdisplay
```

## Create Logical Volume

```bash
sudo lvcreate -L 10G -n tws-lv tws-vg
```

Check logical volumes:

```bash
sudo lvs
sudo lvdisplay
```

## Create Mount Directory

```bash
sudo mkdir -p /mnt/tws-lv-mount
```

## Create Filesystem

```bash
sudo mkfs.ext4 /dev/tws-vg/tws-lv
```

## Mount Logical Volume

```bash
sudo mount /dev/tws-vg/tws-lv /mnt/tws-lv-mount
```

Verify:

```bash
lsblk
df -h
```

## Unmount Logical Volume

```bash
sudo umount /mnt/tws-lv-mount
```

## Extend Logical Volume

```bash
sudo lvextend -L +5G /dev/tws-vg/tws-lv
```

For ext4 filesystem, resize after extending:

```bash
sudo resize2fs /dev/tws-vg/tws-lv
```

Verify:

```bash
df -h
```

## Important Storage Safety Notes

- Always check disk names using `lsblk`
- Do not run `mkfs` on the wrong disk
- `mkfs` formats the disk and can delete data
- Always verify the mount point using `df -h`
- Be careful when working on production servers
- Take backup before storage changes
- Confirm the correct AWS EBS volume before formatting or mounting

# Important Notes for DevOps Engineers

- Test `sed` changes before using `sed -i`
- Create a backup before editing production configuration files
- Use quotes around patterns containing spaces
- Use single quotes for most `grep`, `sed`, and `awk` expressions
- Linux commands are case-sensitive
- Test commands on sample files before using production logs
- Use pipes to combine `grep`, `sed`, and `awk`
- Avoid modifying active production files without backup and validation
- Always verify disk names before formatting or mounting storage
- Use LVM carefully because storage mistakes can cause data loss

# Files in This Phase

| File/Folder | Description |
|---|---|
| `README.md` | Complete Phase 5 overview and detailed notes |
| `commands.md` | Commands practiced in this phase |
| `errors-and-fixes.md` | Errors and fixes during practice |
| `resources.md` | Useful resources and practice references |
| `handwritten-notes/` | My handwritten Phase 5 notes |
| `practice-screenshots/` | Terminal screenshots of hands-on practice |

# What I Learned

In this phase, I learned how to:

- Search files and command output using `grep`
- Use important `grep` options
- Use regular expressions with `grep`
- Replace, delete, insert, and modify text using `sed`
- Safely edit files using `sed -i.bak`
- Extract columns using `awk`
- Use important `awk` variables like `$0`, `$1`, `NR`, `NF`, `$NF`, `FS`, and `OFS`
- Filter records using `awk`
- Calculate totals, averages, counts, minimum, and maximum values using `awk`
- Format output using `awk printf`
- Combine `grep`, `sed`, and `awk` using pipes
- Understand Linux volumes and AWS EBS
- Understand PV, VG, LV, and LVM
- Create physical volumes, volume groups, and logical volumes
- Mount logical volumes
- Extend logical volumes using LVM
- Follow safety rules before editing files or changing storage

# Status

Completed
