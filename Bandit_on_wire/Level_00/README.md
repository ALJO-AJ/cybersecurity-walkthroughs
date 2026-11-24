# Bandit Level 0 → Level 1

## Challenge Objective

The objective of this level is to connect to the Bandit server using SSH and retrieve the password required to access Level 1.

## 1. SSH Connection

Command:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

**Credentials:**
- Username: `bandit0`
- Host: `bandit.labs.overthewire.org`
- Port: `2220`
- Initial password: `bandit0`

## 2. Exploring the System

After successfully connecting, I checked my current username.

Command:

```bash
whoami
```

Output:

```text
bandit0
```

This confirmed that I was logged in as the `bandit0` user.

## 3. Listing Files

Command:

```bash
ls
```

Output:

```text
readme
```

I discovered a file named `readme` in the current directory.

## 4. Checking the Current Directory

Command:

```bash
pwd
```

Output:

```text
/home/bandit0
```

This showed that I was working inside the home directory of the `bandit0` user.

## 5. Reading the File

Command:

```bash
cat readme
```

The command displayed the contents of the file.

The file contained a welcome message and the password needed for the next level.

## 6. Concepts Learned

| Command | Purpose |
|---|---|
| `whoami` | Identify the current user |
| `ls` | List directory contents |
| `pwd` | Display the current working directory |
| `cat` | Read file contents |

## 7. Result

Successfully retrieved the password for Bandit Level 1.

**Password handling:** The actual password is intentionally not published in this documentation.

## 8. What I Learned

- How to connect to a remote Linux machine using SSH.
- How to identify the currently logged-in user.
- How to navigate and inspect directories.
- How to read files using the `cat` command.
- How basic Linux commands can help solve security challenges.

## 9. References

- https://overthewire.org/wargames/bandit/
- https://linux.die.net/man/1/cat
- https://linux.die.net/man/1/ls

---

**Status:** Level 0 completed successfully.