# Day 2 - Linux Commands

This file contains all Linux commands I practiced on Day 2 of my Linux for DevOps journey.

---

## 1. Directory Navigation Commands

```bash
pwd
ls
ls -l
ls -a
ls -la
cd foldername
cd ..
cd ~
cd /
```

---

## 2. Create Directories

```bash
mkdir linux-practice
mkdir empty-folder
mkdir test-folder
mkdir backup
mkdir folder1
mkdir folder2
```

Create nested directories:

```bash
mkdir -p devops/linux/commands
```

---

## 3. Create Files

```bash
touch notes.txt
touch delete-me.txt
touch file1.txt
touch file2.txt
touch folder1/file3.txt
touch users.txt
touch output.txt
touch original.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

---

## 4. Write Content into Files

Using `cat`:

```bash
cat > notes.txt
```

After writing text, press:

```bash
CTRL + D
```

Using `echo`:

```bash
echo "Hello Linux"
echo "Linux" > original.txt
echo "zain ali sarah bilal" > names.txt
```

Append text into a file:

```bash
echo "New line" >> notes.txt
```

---

## 5. Read File Content

```bash
cat notes.txt
cat file1.txt
cat users.txt
cat output.txt
cat original.txt
cat hardlink.txt
cat softlink
```

---

## 6. View Starting Lines of a File

```bash
head notes.txt
head file1.txt
head -n 5 notes.txt
head -n 5 nohup.out
```

---

## 7. View Ending Lines of a File

```bash
tail notes.txt
tail file1.txt
tail -n 5 notes.txt
tail -n 5 nohup.out
```

---

## 8. Read Large Files Page by Page

```bash
less notes.txt
more notes.txt
less file1.txt
more file1.txt
```

Inside `less`:

```bash
Space      # next page
b          # previous page
/search    # search text
n          # next search result
q          # quit
```

---

## 9. Remove Files

```bash
rm delete-me.txt
rm notes.txt
rm original.txt
```

Force remove file:

```bash
rm -f file1.txt
```

---

## 10. Remove Directories

Remove empty directory:

```bash
rmdir empty-folder
```

Remove directory with files inside:

```bash
rm -r test-folder
rm -r foldername
```

Force remove directory:

```bash
rm -rf foldername
```

---

## 11. Copy Files and Folders

Copy one file into another file:

```bash
cp file1.txt file2.txt
```

Copy file into a folder:

```bash
cp notes.txt backup/
```

Copy folder recursively:

```bash
cp -r folder1 folder2
```

Copy folder into another folder:

```bash
cp -r project project-backup
```

---

## 12. Move and Rename Files/Folders

Rename file:

```bash
mv old.txt new.txt
```

Move file into folder:

```bash
mv notes.txt backup/
```

Rename folder:

```bash
mv folder2 backups
```

Move folder:

```bash
mv folder1 backups/
```

---

## 13. Word Count Commands

Show lines, words, and bytes:

```bash
wc file1.txt
```

Count only lines:

```bash
wc -l file1.txt
```

Count only words:

```bash
wc -w file1.txt
```

Count only bytes:

```bash
wc -c file1.txt
```

Count characters:

```bash
wc -m file1.txt
```

Use with pipe:

```bash
cat file1.txt | wc -l
cat file1.txt | wc -w
cat file1.txt | wc -c
```

---

## 14. Vi Editor Commands

Open file in `vi`:

```bash
vi file1.txt
```

Inside `vi`:

```bash
i        # insert mode
Esc      # command mode
:w       # save
:q       # quit
:wq      # save and quit
:q!      # quit without saving
```

---

## 15. Hard Link Commands

Create hard link:

```bash
ln original.txt hardlink.txt
```

Check hard link:

```bash
cat hardlink.txt
ls -l
```

Remove original file and test hard link:

```bash
rm original.txt
cat hardlink.txt
```

---

## 16. Soft Link Commands

Create soft link:

```bash
ln -s original.txt softlink
```

Check soft link:

```bash
ls -l
cat softlink
```

Remove original file and test soft link:

```bash
rm original.txt
cat softlink
```

---

## 17. Cut Command

Example file content:

```bash
cat > users.txt
ali:20:karachi
ahmed:22:lahore
sarah:21:islamabad
```

Show first field:

```bash
cut -d ":" -f 1 users.txt
```

Show second field:

```bash
cut -d ":" -f 2 users.txt
```

Show third field:

```bash
cut -d ":" -f 3 users.txt
```

Cut first field from system password file:

```bash
cut -d ":" -f 1 /etc/passwd
```

---

## 18. Tee Command

Show output on screen and save into file:

```bash
echo "Hello devops" | tee output.txt
```

Append output into file:

```bash
echo "New Line" | tee -a output.txt
echo "Third line" | tee -a output.txt
```

Save command output into file:

```bash
ls -l | tee output.txt
```

Append command output into file:

```bash
ls -l | tee -a output.txt
```

Check file:

```bash
cat output.txt
```

---

## 19. Sort Command

Sort lines alphabetically:

```bash
sort names.txt
```

Reverse sort:

```bash
sort -r names.txt
```

Numeric sort:

```bash
sort -n numbers.txt
```

Sort words written in one line:

```bash
tr ' ' '\n' < names.txt | sort
```

Reverse sort words written in one line:

```bash
tr ' ' '\n' < names.txt | sort -r
```

---

## 20. Diff Command

Compare two files:

```bash
diff file1.txt file2.txt
```

Example:

```bash
diff old.txt new.txt
```

---

## 21. SSH Commands

Change permission of private key:

```bash
chmod 400 linux-devops.pem
```

Login to remote Ubuntu server:

```bash
ssh -i linux-devops.pem ubuntu@your-ec2-public-dns
```

Example format:

```bash
ssh -i key-name.pem ubuntu@server-public-ip
```

Important:

```bash
# Never upload .pem files to GitHub
```

---

## 22. Disk Usage Commands

Show disk usage:

```bash
df
```

Show disk usage in human-readable format:

```bash
df -h
```

Show folder size:

```bash
du
```

Show folder size in human-readable format:

```bash
du -h
```

Show current directory size:

```bash
du -h .
```

---

## 23. Process Commands

Show running processes:

```bash
ps
```

Show all running processes:

```bash
ps aux
```

Show processes using a file or directory:

```bash
fuser .
```

---

## 24. Memory Commands

Show memory usage:

```bash
free
```

Show memory usage in human-readable format:

```bash
free -h
```

---

## 25. Nohup Command

Run command in background even after terminal closes:

```bash
nohup command &
```

Example:

```bash
nohup free -h
```

Better DevOps-style example:

```bash
nohup ping -c 20 google.com > ping.log 2>&1 &
```

Check output:

```bash
cat nohup.out
cat ping.log
```

---

## 26. Vmstat Commands

Show system performance:

```bash
vmstat
```

Show active and inactive memory:

```bash
vmstat -a
```

Show vmstat help:

```bash
vmstat -h
```

---

## 27. Helpful Manual Commands

```bash
man ls
man cp
man mv
man rm
man wc
man cut
man sort
man diff
man ssh
man df
man du
man free
man vmstat
```

---

## 28. Commands I Should Be Careful With

```bash
rm file.txt
rm -r foldername
rm -rf foldername
chmod 400 key.pem
ssh -i key.pem ubuntu@server
```

These commands should be used carefully because they can delete data, change permissions, or connect to remote servers.

---

## 29. Security Reminder

Never upload these files to GitHub:

```bash
*.pem
*.key
.env
```

Add them inside `.gitignore`:

```bash
*.pem
*.key
.env
```

---

## Day 2 Completed

I practiced Linux file operations, text processing, links, SSH login, and basic system monitoring commands.
