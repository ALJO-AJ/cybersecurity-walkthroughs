
# Bandit Level 9 → Level 10

## Objective

Find the password stored in `data.txt` among
human-readable strings preceded by several
`=` characters.

## SSH Connection

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
ls
```

Output:

```text
data.txt
```

## Step 2: Incorrect Command

```bash
string data.txt
```

This returned a command-not-found error.

The correct command is `strings`, not `string`.

## Step 3: Extract Printable Strings

```bash
strings data.txt
```

The command extracted human-readable character
sequences from the file.

Among the output, the following relevant
strings were identified:

```text
========== the
========== password
========== is
========== [PASSWORD REDACTED]
```

## Step 4: Inspecting Raw File Contents

```bash
cat data.txt
```

The output contained unreadable characters
because the file contained binary data.

This demonstrated why strings is more suitable
for extracting readable information from
binary files.

## Step 5: Optimized Solution

```bash
strings data.txt | grep '===='
```

This is an improved solution that combines
strings with grep to filter unnecessary output.

The password was already identified using
the strings command during the actual session.

## Commands Used

| Command | Description |
|---|---|
| `ls` | Lists files and directories |
| `cat` | Displays raw file contents |
| `strings` | Extracts printable character sequences |
| `grep` | Filters matching lines |
| `\|` | Passes output between commands |

## Additional Useful Commands

```bash
file data.txt
strings -n 10 data.txt
strings data.txt | grep '^='
reset
```

## Lessons Learned

- Understanding binary and text data.
- Extracting readable strings from binary files.
- Understanding the limitations of cat.
- Combining strings and grep.
- Filtering unnecessary output.
- Troubleshooting command syntax errors.

## Result

- Status: Password retrieved
- Next Level: Bandit Level 10

The actual password is intentionally omitted
for responsible documentation.

## Reference

https://overthewire.org/wargames/bandit/bandit9.html

---

Part of my hands-on cybersecurity learning journey.
