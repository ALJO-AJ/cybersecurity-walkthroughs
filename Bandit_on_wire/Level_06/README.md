
# Bandit Level 6 → Level 7

## Objective

Find the password for the next level stored somewhere
on the server with the following properties:

- Owned by user `bandit7`
- Owned by group `bandit6`
- Exactly 33 bytes in size

## SSH Connection

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
whoami
pwd
ls
ls -al
```

The current user was `bandit6`, and the working
directory was `/home/bandit6`.

No relevant password file was found in the home directory.

## Step 2: Initial Search

```bash
find / -size 33c -group bandit5 -user bandit7
```

This command used the incorrect group name and
generated multiple permission-denied errors.

The required group was `bandit6`, not `bandit5`.

## Step 3: Search by File Size

```bash
find / -size 33c
```

This returned many unrelated files because the search
only considered file size.

## Step 4: Narrowing the Search

```bash
find / -size 33c -user bandit7 -type f
```

This narrowed the search to regular files owned by
bandit7 with a size of exactly 33 bytes.

However, permission-denied messages were still displayed.

## Step 5: Error Redirection

### Incorrect attempt

```bash
find / -size 33c -user bandit7 -type f | 2>/dev/null
```

The pipe operator was unnecessary because error
redirection must be applied directly to the command.

### Corrected command

```bash
find / -size 33c -user bandit7 -type f 2>/dev/null
```

Output:

```text
/var/lib/dpkg/info/bandit7.password
/etc/bandit_pass/bandit7
```

Attempting to read the second file resulted in
a permission-denied error.

## Step 6: Final Search and Verification

```bash
find / -size 33c -user bandit7 -group bandit6 -type f 2>/dev/null
```

Output:

```text
/var/lib/dpkg/info/bandit7.password
```

This command satisfies all the challenge requirements.

## Step 7: Retrieve the Password

```bash
cat /var/lib/dpkg/info/bandit7.password
```

The password for Bandit Level 7 was successfully retrieved.

The actual password is intentionally omitted.

## Command Breakdown

| Command / Option | Description |
|---|---|
| `whoami` | Displays the current username |
| `pwd` | Displays the current working directory |
| `ls -al` | Lists all files with detailed information |
| `find /` | Searches from the root directory |
| `-size 33c` | Matches files exactly 33 bytes in size |
| `-user bandit7` | Filters by user ownership |
| `-group bandit6` | Filters by group ownership |
| `-type f` | Matches regular files |
| `2>/dev/null` | Suppresses standard error messages |
| `cat` | Displays file contents |

## New Concept: Linux Standard Streams

| File Descriptor | Stream | Description |
|---|---|---|
| 0 | stdin | Standard input |
| 1 | stdout | Standard output |
| 2 | stderr | Standard error |

The `/dev/null` device discards all data written to it.

Redirecting stderr to `/dev/null` hides error messages
without changing file permissions or bypassing access controls.

## Lessons Learned

- Searching the entire Linux filesystem.
- Filtering files using user and group ownership.
- Searching for files by exact byte size.
- Combining multiple search conditions.
- Understanding Linux file permissions.
- Understanding standard streams and error redirection.
- Identifying and correcting command syntax mistakes.

## Result

- Status: Completed
- Password: Successfully retrieved
- Next Level: Bandit Level 7

## Reference

https://overthewire.org/wargames/bandit/bandit6.html

---

Part of my hands-on cybersecurity learning journey.
