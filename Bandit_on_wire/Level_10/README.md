
# Bandit Level 10 → Level 11

## Objective

Find the password stored in `data.txt`, which
contains Base64-encoded data.

## SSH Connection

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
ls
```

Output:

```text
data.txt
```

## Step 2: Inspect File Contents

```bash
cat data.txt
```

The file contained Base64-encoded text.

The encoded content is omitted because it
contains the password in a reversible format.

## Step 3: Decode Base64 Data

```bash
base64 -d data.txt
```

Output:

```text
The password is [PASSWORD REDACTED]
```

The `-d` option decodes Base64-encoded data
into its original representation.

## Step 4: Incorrect Option Syntax

```bash
base64 -decode data.txt
```

Output:

```text
error: unexpected argument '-e' found
```

This error occurred because a long option
was incorrectly specified using a single hyphen.

## Step 5: Correct Long Option

```bash
base64 --decode data.txt
```

Output:

```text
The password is [PASSWORD REDACTED]
```

Both `-d` and `--decode` successfully
decoded the file.

## Alternative Solution

```bash
cat data.txt | base64 -d
```

## Commands Used

| Command | Description |
|---|---|
| `ls` | Lists files and directories |
| `cat` | Displays file contents |
| `base64` | Encodes data using Base64 |
| `base64 -d` | Decodes Base64 data |
| `base64 --decode` | Long option for decoding |

## Encoding vs Encryption

Base64 is an encoding mechanism, not encryption.

- Encoding changes data representation.
- Encryption protects data confidentiality.
- Base64 decoding does not require a secret key.
- Base64 should not be used to protect passwords.

## Lessons Learned

- Understanding Base64 encoding and decoding.
- Identifying encoded data.
- Understanding short and long command options.
- Troubleshooting invalid command arguments.
- Understanding encoding versus encryption.
- Extracting information from encoded files.

## Result

- Status: Completed
- Password: Successfully retrieved
- Next Level: Bandit Level 11

The password and its encoded representation
are intentionally omitted.

## Reference

https://overthewire.org/wargames/bandit/bandit10.html

---

Part of my hands-on cybersecurity learning journey.
