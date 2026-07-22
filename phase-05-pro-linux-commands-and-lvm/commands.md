# Phase 5 Commands Practice

This file contains the commands I practiced in Phase 5.

# grep Commands

## Basic Search

```bash
grep "error" application.log
```

## Ignore Case

```bash
grep -i "error" application.log
```

## Show Line Numbers

```bash
grep -n "error" application.log
```

## Invert Match

```bash
grep -v "success" application.log
```

## Count Matching Lines

```bash
grep -c "error" application.log
```

## Match Complete Word

```bash
grep -w "user" file.txt
```

## Recursive Search

```bash
grep -r "database" /etc/
```

## Show Only Filenames Containing Match

```bash
grep -l "error" *.log
```

## Show Filenames Without Match

```bash
grep -L "error" *.log
```

## Show Lines After Match

```bash
grep -A 3 "error" application.log
```

## Show Lines Before Match

```bash
grep -B 3 "error" application.log
```

## Show Lines Before and After Match

```bash
grep -C 2 "error" application.log
```

## Extended Regular Expression

```bash
grep -E "error|warning" application.log
```

## Fixed Text Search

```bash
grep -F "192.168.1.10" access.log
```

## Highlight Match

```bash
grep --color=auto "error" application.log
```

## Search Command Output

```bash
ps aux | grep nginx
systemctl list-units | grep running
docker ps | grep nginx
```

---

# grep Regular Expression Practice

```bash
grep "^ERROR" application.log
grep "failed$" application.log
grep "s.rv.r" file.txt
grep "go*d" file.txt
grep "[Ee]rror" application.log
grep "[^0-9]" file.txt
grep "[0-9]" file.txt
grep -E "error|failed|warning" application.log
```

---

# sed Commands

## Basic Replace

```bash
sed 's/old/new/' file.txt
```

## Replace All Occurrences

```bash
sed 's/old/new/g' file.txt
```

## Ignore Case

```bash
sed 's/error/issue/gI' application.log
```

## Modify Original File

```bash
sed -i 's/old/new/g' file.txt
```

## Modify Original File With Backup

```bash
sed -i.bak 's/old/new/g' file.txt
```

## Print Specific Line

```bash
sed -n '5p' file.txt
```

## Print Range of Lines

```bash
sed -n '5,10p' file.txt
```

## Delete Specific Line

```bash
sed '5d' file.txt
```

## Delete Range of Lines

```bash
sed '5,10d' file.txt
```

## Delete Lines Containing Pattern

```bash
sed '/debug/d' application.log
```

## Modify File While Deleting Pattern Lines

```bash
sed -i '/debug/d' application.log
```

## Insert Text Before a Line

```bash
sed '3i\new line added' file.txt
```

## Append Text After a Line

```bash
sed '3a\new line added' file.txt
```

## Change Entire Line

```bash
sed '3c\This is the replacement line' file.txt
```

## Use Pattern as Address

```bash
sed -n '/ERROR/p' application.log
```

## Replace Text on Specific Line

```bash
sed '5s/old/new/' file.txt
```

## Replace Text from Line 5 to 10

```bash
sed '5,10s/old/new/g' file.txt
```

## Delete Blank Lines

```bash
sed '/^$/d' file.txt
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

```bash
sed '/^#/d' config.conf
```

## Remove Comments and Blank Lines

```bash
sed '/^#/d; /^$/d' config.conf
```

## Use Another Delimiter

```bash
sed 's|/var/www/old|/var/www/new|g' file.txt
```

## Extended Regex

```bash
sed -E 's/error|warning/issue/g' file.txt
```

## Capturing Groups

```bash
sed -E 's/(user)=([^ ]+)/\1=hidden/' file.txt
```

---

# awk Commands

## Print Complete Line

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

## Colon-Separated Data

```bash
awk -F: '{print $1}' /etc/passwd
```

## Comma-Separated Data

```bash
awk -F, '{print $1, $3}' employees.csv
```

## Pipe-Separated Data

```bash
awk -F'|' '{print $1, $2}' file.txt
```

## Pattern Filtering

```bash
awk '/error/ {print $0}' application.log
```

## Ignore Case

```bash
awk 'tolower($0) ~ /error/ {print}' application.log
```

## Numeric Condition

```bash
awk '$3 > 50000 {print $1, $3}' employees.txt
```

## String Condition

```bash
awk '$2 == "devops" {print $1}' employees.txt
```

## Not Equal

```bash
awk '$2 != "admin" {print $0}' employees.txt
```

## AND Condition

```bash
awk '$2 == "devops" && $3 > 40000 {print $1}' employees.txt
```

## OR Condition

```bash
awk '$2 == "devops" || $2 == "admin" {print $1}' employees.txt
```

## BEGIN Block

```bash
awk 'BEGIN {print "DevOps Report"} {print $0}' file.txt
```

## Set Field Separator in BEGIN

```bash
awk 'BEGIN {FS=":"} {print $1}' /etc/passwd
```

## END Block

```bash
awk 'END {print "Total lines:", NR}' file.txt
```

## Calculate Total

```bash
awk '{sum += $3} END {print "Total:", sum}' employees.txt
```

## Calculate Average

```bash
awk '{sum += $3} END {print "Average:", sum/NR}' employees.txt
```

## Count Matching Lines

```bash
awk '/error/ {count++} END {print "Errors:", count}' application.log
```

## Find Maximum Value

```bash
awk 'NR == 1 || $3 > max {max = $3} END {print max}' employees.txt
```

## Find Minimum Value

```bash
awk 'NR == 1 || $3 < min {min = $3} END {print min}' employees.txt
```

## Formatting Output

```bash
awk '{printf "User: %-10s Salary: %s\n", $1, $3}' employees.txt
```

---

# Combining grep, sed, and awk

## grep with awk

```bash
grep "ERROR" application.log | awk '{print $1, $2, $5}'
```

## grep with sed

```bash
grep "ERROR" application.log | sed 's/ERROR/ISSUE/g'
```

## sed with awk

```bash
sed '/^#/d' config.txt | awk '{print $1}'
```

## All Three Together

```bash
grep "ERROR" application.log | sed 's/ERROR/CRITICAL/g' | awk '{print $1, $2, $0}'
```

---

# Linux Volume Management and LVM Commands

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

## Become Root User

```bash
sudo su
```

## Create Physical Volumes

```bash
sudo pvcreate /dev/nvme1n1 /dev/nvme2n1 /dev/nvme3n1
```

## Display Physical Volumes

```bash
sudo pvs
sudo pvdisplay
```

## Create Volume Group

```bash
sudo vgcreate tws-vg /dev/nvme1n1 /dev/nvme2n1
```

## Display Volume Groups

```bash
sudo vgs
sudo vgdisplay
```

## Create Logical Volume

```bash
sudo lvcreate -L 10G -n tws-lv tws-vg
```

## Display Logical Volumes

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

## Verify Mount

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

## Resize ext4 Filesystem

```bash
sudo resize2fs /dev/tws-vg/tws-lv
```

## Verify After Extension

```bash
df -h
```
