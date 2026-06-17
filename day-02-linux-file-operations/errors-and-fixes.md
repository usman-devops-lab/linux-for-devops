# Day 2 - Errors and Fixes

This file contains the mistakes I faced during Day 2 Linux practice and how I fixed them.

Learning errors is an important part of becoming comfortable with Linux and DevOps.

---

## 1. `sort` Command Did Not Sort Names Correctly

### Issue

I created a file with names in one line:

```bash
echo "zain ali sarah bilal" > names.txt
```

Then I ran:

```bash
sort names.txt
```

But the output did not change.

### Reason

The `sort` command sorts lines, not individual words.

Because all names were written in one line, Linux treated the full line as one item.

### Fix

Convert spaces into new lines first, then sort:

```bash
tr ' ' '\n' < names.txt | sort
```

### Reverse Sort

```bash
tr ' ' '\n' < names.txt | sort -r
```

### Learning

`sort` works line by line.
If words are in one line, I need to convert them into separate lines first.

---

## 2. Used `cat` Instead of `cut`

### Wrong Command

```bash
cat -d ":" -f 1 users.txt
```

### Error

```text
cat: invalid option -- 'd'
```

### Reason

The `cat` command is only used to display file content.
It does not support `-d` and `-f` options.

The `-d` and `-f` options are used with the `cut` command.

### Correct Command

```bash
cut -d ":" -f 1 users.txt
```

### Example File

```text
ali:20:karachi
ahmed:22:lahore
sarah:21:islamabad
```

### Extract Names

```bash
cut -d ":" -f 1 users.txt
```

### Extract Ages

```bash
cut -d ":" -f 2 users.txt
```

### Extract Cities

```bash
cut -d ":" -f 3 users.txt
```

### Learning

Use `cat` to display files.
Use `cut` to extract fields or columns from structured text.

---

## 3. `cp` Failed Because Backup Folder Did Not Exist

### Wrong Command

```bash
cp notes.txt backup/
```

### Error

```text
cp: cannot create regular file 'backup/': Not a directory
```

### Reason

The `backup` directory did not exist before copying the file.

### Fix

First create the directory:

```bash
mkdir backup
```

Then copy the file:

```bash
cp notes.txt backup/
```

### Learning

Before copying a file into a folder, make sure the destination folder already exists.

---

## 4. `cp` Failed Because Source File Did Not Exist

### Wrong Command

```bash
cp notes.txt backup/
```

### Error

```text
cp: cannot stat 'notes.txt': No such file or directory
```

### Reason

The file `notes.txt` was not available in the current directory at that time.

### Fix

Check files first:

```bash
ls
```

Create the file if needed:

```bash
touch notes.txt
```

Then copy it:

```bash
cp notes.txt backup/
```

### Learning

Before copying or moving files, check the current directory using `ls`.

---

## 5. Typing Mistake in `echo` Command

### Wrong Command

```bash
exho "Hello Linux"
```

### Error

```text
Command 'exho' not found
```

### Reason

I typed `exho` instead of `echo`.

### Correct Command

```bash
echo "Hello Linux"
```

### Learning

Linux commands are exact.
A small spelling mistake can cause a command not found error.

---

## 6. Typing Mistake in `cat` Command

### Wrong Command

```bash
car file1.txt | wc -c
```

### Error

```text
Command 'car' not found
```

### Reason

I typed `car` instead of `cat`.

### Correct Command

```bash
cat file1.txt | wc -c
```

### Learning

Always check command spelling carefully, especially when using pipes.

---

## 7. Understanding `wc` Output

### Command

```bash
wc file1.txt
```

### Example Output

```text
4 10 58 file1.txt
```

### Meaning

```text
4  = lines
10 = words
58 = bytes
```

### Useful Options

```bash
wc -l file1.txt
wc -w file1.txt
wc -c file1.txt
```

### Learning

`wc` without options shows lines, words, and bytes together.

---

## 8. `rm -r` Should Be Used Carefully

### Command

```bash
rm -r test-folder/
```

### Reason for Caution

This command deletes a folder and everything inside it.

### Safer Approach

Check folder content first:

```bash
ls test-folder/
```

Then delete:

```bash
rm -r test-folder/
```

### Learning

In DevOps, delete commands must be used carefully because they can remove important files.

---

## 9. Hard Link and Soft Link Difference

### Hard Link

```bash
ln original.txt hardlink.txt
```

A hard link still works even if the original file is deleted.

### Soft Link

```bash
ln -s original.txt softlink
```

A soft link breaks if the original file is deleted.

### Learning

Hard links point to the same file data.
Soft links point to the file path.

---

## 10. SSH Private Key Permission

### Command

```bash
chmod 400 linux-devops.pem
```

### Reason

SSH private keys should not be publicly readable.

After setting correct permissions, SSH login can be done using:

```bash
ssh -i linux-devops.pem ubuntu@your-ec2-public-dns
```

### Learning

Private keys must be protected before connecting to a remote server.

---

## Security Reminder

Never upload private keys or secret files to GitHub.

Do not upload:

```text
linux-devops.pem
.env
*.key
```

Add these lines to `.gitignore`:

```gitignore
*.pem
*.key
.env
```

---

## Final Learning

Today I learned that errors are part of Linux practice.
Each error helped me understand commands more clearly and improved my confidence in using the terminal.
