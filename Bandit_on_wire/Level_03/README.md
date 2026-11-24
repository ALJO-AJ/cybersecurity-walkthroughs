# Bandit Level 3 → Level 4

## Objective
Find a hidden file inside the `inhere` directory and read its contents to obtain the next level's password.

## Login Information
- Current user: `bandit3`
- Working directory: `/home/bandit3`
- Target directory: `inhere`
- Target file: `...Hiding-From-You`

## Commands Used

### 1. Identify the current user
```bash
whoami
```
Output:
```text
bandit3
```

### 2. Check the working directory
```bash
pwd
```
Output:
```text
/home/bandit3
```

### 3. List files
```bash
ls
```
Output:
```text
inhere
```

### 4. Display all files, including hidden files
```bash
ls -al
```

This displays hidden entries as well as ordinary files.

### 5. Enter the target directory
```bash
cd inhere/
```

### 6. Check ordinary files
```bash
ls
```

No files were displayed because the target filename begins with dots.

### 7. Find the hidden file
```bash
ls -al
```

Discovered:
```text
...Hiding-From-You
```

### 8. Read the hidden file
```bash
cat ./...Hiding-From-You
```

Successfully retrieved the next-level password.

## What I Learned

- Linux hidden-file naming conventions.
- Difference between `ls` and `ls -al`.
- How to navigate directories using `cd`.
- How to inspect hidden files.
- How to use relative paths with `./`.

## Security Note
The next-level password is not included in this public documentation.

## Status
Completed — successfully located and read the hidden file.