# Phase 5 Errors and Fixes

This file contains common errors and fixes related to Phase 5: Pro Linux Commands and LVM.

The errors are related to `grep`, `sed`, `awk`, regular expressions, pipes, file editing, Linux volume management, AWS EBS, and LVM commands.

---

# grep Errors and Fixes

## 1. grep pattern not found

### Example

```bash
grep "error" application.log
```

No output appears.

### Reason

The pattern may not exist in the file, or the case may be different.

### Fix

Try ignore case:

```bash
grep -i "error" application.log
```

Check the file content:

```bash
cat application.log
```

---

## 2. grep matches too many lines

### Reason

The search pattern is too broad.

### Fix

Use whole-word matching:

```bash
grep -w "user" file.txt
```

Use more specific pattern:

```bash
grep "Database connection error" application.log
```

---

## 3. grep does not search subdirectories

### Wrong

```bash
grep "database" /etc/
```

### Fix

Use recursive option:

```bash
grep -r "database" /etc/
```

---

## 4. grep OR condition does not work

### Wrong

```bash
grep "error|warning" application.log
```

### Reason

Basic grep does not treat `|` as OR unless extended regex is enabled.

### Fix

```bash
grep -E "error|warning" application.log
```

or:

```bash
egrep "error|warning" application.log
```

---

## 5. grep fixed string interpreted as regex

### Problem

Dots and other characters may be treated as regex symbols.

### Example

```bash
grep "192.168.1.10" access.log
```

### Safer Fix

```bash
grep -F "192.168.1.10" access.log
```

---

# sed Errors and Fixes

## 6. sed command does not modify file

### Example

```bash
sed 's/old/new/g' file.txt
```

### Reason

By default, `sed` only prints the changed output on the terminal.

### Fix

Use `-i` to modify the file:

```bash
sed -i 's/old/new/g' file.txt
```

Safer fix with backup:

```bash
sed -i.bak 's/old/new/g' file.txt
```

---

## 7. sed modifies wrong file content

### Reason

The command was not tested before using `-i`.

### Fix

Test first:

```bash
sed 's/old/new/g' config.conf
```

Then use backup:

```bash
sed -i.bak 's/old/new/g' config.conf
```

---

## 8. sed prints duplicate lines with p command

### Example

```bash
sed '/ERROR/p' application.log
```

### Reason

`sed` prints every line by default and also prints matching lines again.

### Fix

Use `-n`:

```bash
sed -n '/ERROR/p' application.log
```

---

## 9. sed path replacement becomes confusing because of slashes

### Example

```bash
sed 's//var/www/old//var/www/new/g' file.txt
```

### Reason

The `/` delimiter conflicts with path slashes.

### Fix

Use another delimiter:

```bash
sed 's|/var/www/old|/var/www/new|g' file.txt
```

---

## 10. sed extended regex does not work

### Example

```bash
sed 's/error|warning/issue/g' file.txt
```

### Reason

Extended regex is not enabled.

### Fix

```bash
sed -E 's/error|warning/issue/g' file.txt
```

---

## 11. sed permission denied

### Error

```bash
Permission denied
```

### Reason

The file may require root permission.

### Fix

```bash
sudo sed -i.bak 's/old/new/g' /etc/config.conf
```

### DevOps Warning

Be careful when editing system configuration files. Always create a backup.

---

# awk Errors and Fixes

## 12. awk prints wrong column

### Reason

The file may use a separator other than spaces or tabs.

### Fix for colon-separated data

```bash
awk -F: '{print $1}' /etc/passwd
```

### Fix for comma-separated data

```bash
awk -F, '{print $1, $3}' employees.csv
```

---

## 13. awk condition does not match string

### Wrong

```bash
awk '$2 == devops {print $1}' employees.txt
```

### Reason

String values must be inside quotes.

### Fix

```bash
awk '$2 == "devops" {print $1}' employees.txt
```

---

## 14. awk numeric comparison gives unexpected result

### Reason

The wrong column may be selected, or the column may contain non-numeric values.

### Fix

Check columns first:

```bash
awk '{print $1, $2, $3}' employees.txt
```

Then run the condition:

```bash
awk '$3 > 50000 {print $1, $3}' employees.txt
```

---

## 15. awk average calculation is wrong

### Problem

Using `sum/NR` may be wrong if header rows exist.

### Fix

Skip header if needed:

```bash
awk 'NR > 1 {sum += $3; count++} END {print sum/count}' employees.txt
```

---

## 16. awk field separator issue

### Problem

`awk` separates by spaces by default.

### Fix

Use `-F`:

```bash
awk -F, '{print $1, $3}' employees.csv
```

---

# Pipe Errors and Fixes

## 17. Pipe command gives no output

### Example

```bash
grep "ERROR" application.log | awk '{print $5}'
```

No output appears.

### Possible Reasons

- `grep` found no matching lines
- The selected column does not exist
- The file is empty
- Pattern case is different

### Fix

Check step by step:

```bash
grep "ERROR" application.log
```

Then:

```bash
grep "ERROR" application.log | awk '{print $0}'
```

---

## 18. grep, sed, and awk order confusion

### Rule

Use this order when needed:

```text
grep = find lines
sed  = edit or clean text
awk  = extract columns or format output
```

### Example

```bash
grep "ERROR" application.log | sed 's/ERROR/CRITICAL/g' | awk '{print $1, $2, $0}'
```

---

# LVM and Storage Errors and Fixes

## 19. lvm command not found

### Error

```bash
lvm: command not found
```

or:

```bash
pvcreate: command not found
```

### Reason

LVM tools are not installed.

### Fix for Ubuntu/Debian

```bash
sudo apt update
sudo apt install lvm2
```

### Fix for Amazon Linux/RHEL/CentOS

```bash
sudo yum install lvm2
```

---

## 20. pvcreate device not found

### Error

```bash
Device /dev/nvme1n1 not found
```

### Reason

The device name may be different on your server.

### Fix

Check block devices:

```bash
lsblk
```

Use the correct device name from the output.

---

## 21. pvcreate permission denied

### Error

```bash
Permission denied
```

### Reason

Storage commands require root permissions.

### Fix

```bash
sudo pvcreate /dev/nvme1n1
```

or become root:

```bash
sudo su
```

---

## 22. Device is already used

### Error

```bash
Device is already in use
```

### Reason

The disk may already have a filesystem, partition, or LVM metadata.

### Fix

Check carefully:

```bash
lsblk
sudo pvs
sudo blkid
```

### Warning

Do not wipe disks unless you are sure they do not contain important data.

---

## 23. vgcreate fails because physical volume is missing

### Error

```bash
Physical volume not found
```

### Reason

`pvcreate` was not run successfully.

### Fix

Create PV first:

```bash
sudo pvcreate /dev/nvme1n1
```

Then create VG:

```bash
sudo vgcreate tws-vg /dev/nvme1n1
```

---

## 24. lvcreate fails because volume group does not exist

### Error

```bash
Volume group not found
```

### Fix

Check volume groups:

```bash
sudo vgs
```

Create VG if missing:

```bash
sudo vgcreate tws-vg /dev/nvme1n1
```

Then create LV:

```bash
sudo lvcreate -L 10G -n tws-lv tws-vg
```

---

## 25. mkfs command can delete data

### Warning

```bash
sudo mkfs.ext4 /dev/tws-vg/tws-lv
```

This formats the logical volume.

### Safety Check

Before running `mkfs`, verify:

```bash
lsblk
df -h
```

### DevOps Note

Never run `mkfs` on a production disk without confirmation and backup.

---

## 26. mount point does not exist

### Error

```bash
mount: mount point does not exist
```

### Fix

Create mount directory first:

```bash
sudo mkdir -p /mnt/tws-lv-mount
```

Then mount:

```bash
sudo mount /dev/tws-vg/tws-lv /mnt/tws-lv-mount
```

---

## 27. wrong fs type or bad option during mount

### Reason

The logical volume may not have a filesystem.

### Fix

Create filesystem:

```bash
sudo mkfs.ext4 /dev/tws-vg/tws-lv
```

Then mount again:

```bash
sudo mount /dev/tws-vg/tws-lv /mnt/tws-lv-mount
```

---

## 28. df -h does not show mounted volume

### Possible Reasons

- Volume was not mounted
- Wrong mount point was used
- Mount command failed

### Fix

Check:

```bash
lsblk
df -h
mount | grep tws
```

---

## 29. lvextend completed but df -h size did not change

### Reason

The logical volume may be extended, but the filesystem was not resized.

### Fix for ext4

```bash
sudo resize2fs /dev/tws-vg/tws-lv
```

Then verify:

```bash
df -h
```

---

## 30. cannot unmount because target is busy

### Error

```bash
target is busy
```

### Reason

A process or terminal is using the mount directory.

### Fix

Move out of the mount directory:

```bash
cd ~
```

Then unmount:

```bash
sudo umount /mnt/tws-lv-mount
```

---

# Summary

In this phase, I learned that pro Linux commands and storage commands require careful syntax.

Important lessons:

- `grep` is used to search text
- `sed` is used to edit text
- `awk` is used to process columns and calculate values
- Pipes combine commands together
- Always test `sed` before using `-i`
- Always backup important configuration files
- Always verify disk names before using LVM commands
- `mkfs` can delete data
- `lsblk` and `df -h` are important before and after mounting storage
- LVM commands require careful planning and root permissions
