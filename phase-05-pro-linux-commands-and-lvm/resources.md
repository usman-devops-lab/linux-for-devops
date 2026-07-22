# Phase 5 Resources

This file contains useful references, manual pages, package installation commands, and practice commands for Phase 5: Pro Linux Commands and LVM.

## Course Reference

Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi

# Manual Pages

Use the `man` command to read official Linux documentation.

## Pro Linux Commands

```bash
man grep
man sed
man awk
```

## Storage and LVM Commands

```bash
man lsblk
man df
man mount
man umount
man mkfs
man pvcreate
man pvs
man pvdisplay
man vgcreate
man vgs
man vgdisplay
man lvcreate
man lvs
man lvdisplay
man lvextend
man resize2fs
```

# Help Commands

```bash
grep --help
sed --help
awk --help
lsblk --help
df --help
mount --help
umount --help
mkfs.ext4 --help
pvcreate --help
vgcreate --help
lvcreate --help
lvextend --help
```

# Useful Package Installation

## Ubuntu/Debian

```bash
sudo apt update
sudo apt install gawk sed grep lvm2
```

## Amazon Linux/RHEL/CentOS

```bash
sudo yum install gawk sed grep lvm2
```

# Practice Files

## Create Sample Log File

```bash
cat > application.log <<EOF
INFO Application started
ERROR Database connection failed
WARNING Disk usage high
INFO User login successful
ERROR Payment service failed
DEBUG Cache refreshed
EOF
```

## Create Sample Text File

```bash
cat > file.txt <<EOF
old value
new value
old path
good
goood
server
saver
ERROR
error
EOF
```

## Create Sample Employee File

```bash
cat > employees.txt <<EOF
ali devops 50000
sara developer 60000
ahmed admin 45000
usman devops 70000
EOF
```

## Create Sample CSV File

```bash
cat > employees.csv <<EOF
name,role,salary
ali,devops,50000
sara,developer,60000
ahmed,admin,45000
EOF
```

## Create Sample Config File

```bash
cat > config.conf <<EOF
# old server config
server_name=localhost
port=8080

# debug mode
debug=true
path=/var/www/old
EOF
```

# Recommended grep Practice

```bash
grep "ERROR" application.log
grep -i "error" application.log
grep -n "ERROR" application.log
grep -v "INFO" application.log
grep -c "ERROR" application.log
grep -w "server" file.txt
grep -E "ERROR|WARNING" application.log
grep --color=auto "ERROR" application.log
ps aux | grep ssh
```

# Recommended sed Practice

```bash
sed 's/old/new/' file.txt
sed 's/old/new/g' file.txt
sed 's/error/issue/gI' application.log
sed -n '2p' file.txt
sed -n '2,4p' file.txt
sed '2d' file.txt
sed '/DEBUG/d' application.log
sed '/^#/d' config.conf
sed '/^#/d; /^$/d' config.conf
sed 's|/var/www/old|/var/www/new|g' config.conf
sed -E 's/ERROR|WARNING/ISSUE/g' application.log
```

# Recommended awk Practice

```bash
awk '{print $0}' employees.txt
awk '{print $1}' employees.txt
awk '{print $1, $3}' employees.txt
awk '{print NR, $0}' employees.txt
awk '{print NF}' employees.txt
awk '{print $NF}' employees.txt
awk -F, '{print $1, $3}' employees.csv
awk '$3 > 50000 {print $1, $3}' employees.txt
awk '$2 == "devops" {print $1}' employees.txt
awk '$2 != "admin" {print $0}' employees.txt
awk '{sum += $3} END {print "Total:", sum}' employees.txt
awk '{sum += $3} END {print "Average:", sum/NR}' employees.txt
awk 'NR == 1 || $3 > max {max=$3} END {print max}' employees.txt
awk '{printf "User: %-10s Salary: %s\n", $1, $3}' employees.txt
```

# Recommended Combined Practice

```bash
grep "ERROR" application.log | awk '{print $1, $2}'
grep "ERROR" application.log | sed 's/ERROR/CRITICAL/g'
sed '/^#/d' config.conf | awk '{print $1}'
grep "ERROR" application.log | sed 's/ERROR/CRITICAL/g' | awk '{print $1, $2, $0}'
```

# LVM Practice Commands

## Check Storage

```bash
lsblk
df -h
```

## Install LVM

```bash
sudo apt update
sudo apt install lvm2
```

## Create PV

```bash
sudo pvcreate /dev/nvme1n1
sudo pvs
```

## Create VG

```bash
sudo vgcreate tws-vg /dev/nvme1n1
sudo vgs
```

## Create LV

```bash
sudo lvcreate -L 10G -n tws-lv tws-vg
sudo lvs
```

## Create Filesystem and Mount

```bash
sudo mkdir -p /mnt/tws-lv-mount
sudo mkfs.ext4 /dev/tws-vg/tws-lv
sudo mount /dev/tws-vg/tws-lv /mnt/tws-lv-mount
df -h
```

## Extend LV

```bash
sudo lvextend -L +5G /dev/tws-vg/tws-lv
sudo resize2fs /dev/tws-vg/tws-lv
df -h
```

# Quick Revision

```text
grep = find text
sed  = change text
awk  = process columns
PV   = physical volume
VG   = volume group
LV   = logical volume
LVM  = logical volume manager
EBS  = AWS block storage volume
```

# Important Safety Rules

- Test `sed` output before using `sed -i`
- Use `sed -i.bak` for backup
- Use single quotes around most `grep`, `sed`, and `awk` expressions
- Linux commands are case-sensitive
- Use sample files before production logs
- Verify disk names using `lsblk`
- Do not run `mkfs` on the wrong disk
- Take backup before storage changes
- Be careful when working on EC2 and EBS volumes
