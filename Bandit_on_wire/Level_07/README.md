
# Bandit Level 7 → Level 8

## Objective

Find the password stored in `data.txt` next to
the word `millionth`.

## SSH Connection

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
pwd
ls
```

Current directory:

```text
/home/bandit7
```

The directory contained a file named `data.txt`.

## Step 2: Search for the Password

```bash
cat data.txt | grep millionth
```

The `cat` command reads the file contents.

The pipe operator (`|`) passes the output of
`cat` as input to `grep`.

The `grep` command filters the lines containing
the word `millionth`.

## Output

```text
millionth    [PASSWORD REDACTED]
```

## Alternative Solution

```bash
grep millionth data.txt
```

This method is more efficient because grep can
read the file directly without using cat.

## Commands Used

| Command | Description |
|---|---|
| `pwd` | Displays the current directory |
| `ls` | Lists files and directories |
| `cat` | Displays file contents |
| `grep` | Searches for matching text |
| `\|` | Connects command output to another command |

## Lessons Learned

- Searching for specific text inside files.
- Understanding the Linux pipe operator.
- Combining multiple Linux commands.
- Filtering large amounts of text.
- Improving command efficiency.
- Extracting relevant information from files.

## Result

- Status: Completed
- Password: Successfully retrieved
- Next Level: Bandit Level 8

The actual password is intentionally omitted
for responsible documentation.

## Reference

https://overthewire.org/wargames/bandit/bandit7.html

---

Part of my hands-on cybersecurity learning journey.
