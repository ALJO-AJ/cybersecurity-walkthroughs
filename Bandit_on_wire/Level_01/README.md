# Bandit Level 1 → Level 2

## Challenge Objective

The objective of this level is to retrieve the next password from a file named `-` located in the home directory.

## 1. Connection

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

## 2. Identifying the Current User

Command:

```bash
whoami
```

Output:

```text
bandit1
```

## 3. Checking the Working Directory

Command:

```bash
pwd
```

Output:

```text
/home/bandit1
```

## 4. Listing Files

Command:

```bash
ls
```

Output:

```text
-
```

I discovered a file with the unusual filename `-`.

## 5. Investigating the File

I inspected its permissions and ownership:

```bash
ls -l
```

Output:

```text
-rw-r----- 1 bandit2 bandit1 33 Oct 25 13:37 -
```

The file belongs to `bandit2` and its group is `bandit1`.

## 6. Initial Attempts

I tried:

```bash
cd -
```

This failed because `cd -` is used to switch to the previous working directory.

I also tried:

```bash
cat "-"
```

This did not read the file because `cat` treats a standalone `-` as standard input.

## 7. Successful Solution

Command:

```bash
cat ./-
```

Explanation:

- `cat` reads file contents.
- `.` represents the current directory.
- `/` separates the directory from the filename.
- `-` is the actual filename.

Using `./-` explicitly identifies the file path and avoids the special meaning of a standalone `-`.

## 8. Concepts Learned

| Command / Concept | Purpose |
|---|---|
| `whoami` | Identify current user |
| `pwd` | Display working directory |
| `ls` | List directory contents |
| `ls -l` | Display detailed file information |
| `cd -` | Switch to previous directory |
| `cat` | Display file contents |
| `./` | Refer to the current directory |
| `--` | End option processing in supported commands |

## 9. Result

Successfully retrieved the password for Bandit Level 2.

The actual password is intentionally excluded from this public documentation.

## 10. What I Learned

- Linux allows filenames that look like command-line options.
- Some commands assign special meanings to standalone `-`.
- Quoting a filename does not always prevent special argument handling.
- Using `./filename` is a useful way to specify unusual filenames.
- Understanding command-line argument parsing helps solve Linux challenges.

## References

- https://overthewire.org/wargames/bandit/
- https://man7.org/linux/man-pages/man1/cat.1.html

---

**Status:** Level 1 completed successfully.