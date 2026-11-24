# Bandit Level 2 → Level 3

## Objective
Find and read the password for the next Bandit level.

## Login Information
- Current user: `bandit2`
- Working directory: `/home/bandit2`
- Target file: `--spaces in this filename--`

## Commands Used

### 1. Identify the current user
```bash
whoami
```
Output:
```text
bandit2
```

### 2. Check the working directory
```bash
pwd
```
Output:
```text
/home/bandit2
```

### 3. List files
```bash
ls
```
Output:
```text
--spaces in this filename--
```

### 4. Display detailed file information
```bash
ls -al
```

This showed the file's permissions, owner, group, and size.

### 5. Attempt to read the file
```bash
cat '--spaces in this filename--'
```

This failed because the filename begins with `--`, which was interpreted as an option.

### 6. Successfully read the file
```bash
cat ./'--spaces in this filename--'
```

The `./` prefix specifies the current directory, allowing the filename to be interpreted correctly.

Another valid method:
```bash
cat -- '--spaces in this filename--'
```

## What I Learned

- How to inspect files using `ls` and `ls -al`.
- How filenames containing spaces are handled using quotes.
- Why filenames beginning with hyphens can be mistaken for command options.
- How `./` specifies a relative path from the current directory.
- How `--` tells commands to stop processing options.

## Security Note
The next-level password is intentionally not included in this public documentation.

## Status
Completed — successfully retrieved the next-level password.