
# Bandit Level 8 → Level 9

## Objective

Find the password stored in `data.txt` that occurs
exactly once in the file.

## SSH Connection

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
pwd
ls
```

Current working directory:

```text
/home/bandit8
```

The directory contained a file named `data.txt`.

## Step 2: Initial Attempt

```bash
cat data.txt | grep -c 1
```

Output:

```text
400
```

This approach was incorrect because `grep -c 1`
counts lines containing the character `1`, rather
than identifying lines that occur exactly once.

## Step 3: Sorting and Removing Duplicates

```bash
sort data.txt | uniq
```

The `sort` command arranges identical lines together.

The `uniq` command removes adjacent duplicate copies.

However, this does not identify which line originally
occurred only once.

## Step 4: Counting Line Occurrences

```bash
sort data.txt | uniq -c
```

The `-c` option displays the occurrence count
of each group of identical lines.

Example of the observed pattern:

```text
10 [REPEATED LINE]
10 [REPEATED LINE]
 1 [PASSWORD REDACTED]
10 [REPEATED LINE]
```

Only one line had an occurrence count of 1.

## Step 5: Final Solution

```bash
sort data.txt | uniq -u
```

The `-u` option displays only non-repeated lines
after sorting.

Output:

```text
[PASSWORD REDACTED]
```

The password for Bandit Level 9 was successfully
retrieved.

## Step 6: Close the SSH Connection

```bash
exit
```

## Commands Used

| Command | Description |
|---|---|
| `pwd` | Displays the current working directory |
| `ls` | Lists files and directories |
| `cat` | Displays file contents |
| `grep -c` | Counts matching lines |
| `sort` | Sorts lines of text |
| `uniq` | Removes adjacent duplicate copies |
| `uniq -c` | Counts adjacent identical lines |
| `uniq -u` | Displays non-repeated lines |
| `\|` | Passes output between commands |
| `exit` | Closes the shell session |

## Lessons Learned

- Understanding the difference between text matching
  and counting repeated lines.
- Sorting and processing text files.
- Identifying duplicate and non-repeated lines.
- Understanding the importance of sorting before uniq.
- Combining Linux commands using pipes.
- Troubleshooting incorrect search logic.
- Extracting relevant information from large files.

## Result

- Status: Completed
- Password: Successfully retrieved
- Next Level: Bandit Level 9

The actual password is intentionally omitted
for responsible documentation.

## Reference

https://overthewire.org/wargames/bandit/bandit8.html

---

Part of my hands-on cybersecurity learning journey.
