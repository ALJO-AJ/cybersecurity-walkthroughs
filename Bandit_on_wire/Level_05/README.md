# Bandit Level 5 → Level 6

## Objective
Find a human-readable file with exactly 1,033 bytes that is not executable.

## Login Information
- Username: `bandit5`
- Working directory: `/home/bandit5/inhere`
- Target file: `maybehere07/.file2`

## Commands Used

### 1. Check current user
```bash
whoami
```
Output: `bandit5`

### 2. Check current directory
```bash
pwd
```
Output: `/home/bandit5/inhere`

### 3. List directories
```bash
ls
```
The directory contains multiple folders named `maybehere00` through `maybehere19`.

### 4. Search for the required file
First attempt:
```bash
find . -type f -size 1033c ! executable
```
This failed because the hyphen before `executable` was missing.

Correct command:
```bash
find . -type f -size 1033c ! -executable
```

Result:
```text
./maybehere07/.file2
```

### 5. Read the file
```bash
cat ./maybehere07/.file2
```

Successfully retrieved the next-level password.

## Command Explanation

| Option | Meaning |
|---|---|
| `find .` | Search from the current directory |
| `-type f` | Search for regular files |
| `-size 1033c` | Match files exactly 1,033 bytes |
| `!` | Negate the following condition |
| `-executable` | Match executable files |

Therefore, `! -executable` means the file must not be executable.

## What I Learned
- Searching recursively with `find`.
- Filtering files by exact size.
- Finding regular files using `-type f`.
- Excluding executable files.
- Understanding the importance of correct command syntax.

## Security Note
The retrieved password is intentionally excluded from this public documentation.

## Status
Completed — successfully found the required file and retrieved the next-level password.
