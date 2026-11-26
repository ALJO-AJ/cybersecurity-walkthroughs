
# Bandit Level 11 → Level 12

## Objective

Retrieve the password stored in data.txt,
where all uppercase and lowercase letters
have been rotated by 13 positions (ROT13).

## SSH Connection

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
pwd
ls
```

Output:

```text
/home/bandit11
data.txt
```

## Step 2: Inspect File Contents

```bash
cat data.txt
```

Output:

```text
Gur cnffjbeq vf [REDACTED]
```

The file contained ROT13-transformed text.

## Step 3: Incorrect Command

```bash
base13 -d data.txt
```

Output:

```text
Command 'base13' not found
```

Initially, I attempted to use base13 based
on my previous experience with Base64.

However, ROT13 is a character substitution
cipher, not a Base64-style encoding method.

## Step 4: Apply ROT13 Transformation

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Output:

```text
The password is [PASSWORD REDACTED]
```

The tr command translates each uppercase
and lowercase letter by 13 positions.

Numbers and special characters remain
unchanged.

## Command Breakdown

| Component | Description |
|---|---|
| `cat data.txt` | Reads file contents |
| `\|` | Passes output to the next command |
| `tr` | Translates characters |
| `A-Za-z` | Original alphabet |
| `N-ZA-Mn-za-m` | ROT13 alphabet |

## Alternative Solution

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

This uses input redirection instead of cat.

## Commands Used

| Command | Description |
|---|---|
| `pwd` | Displays current directory |
| `ls` | Lists files and directories |
| `cat` | Displays file contents |
| `tr` | Translates or deletes characters |

## Security Concepts

ROT13 is a variation of the Caesar cipher.

- Rotates letters by 13 positions.
- Preserves uppercase and lowercase.
- Does not change numbers or punctuation.
- Applying ROT13 twice restores the original text.
- Does not require a secret key.
- Does not provide meaningful confidentiality.

## Lessons Learned

- Understanding ROT13 and Caesar ciphers.
- Character substitution using tr.
- Understanding encoding versus substitution.
- Troubleshooting command-not-found errors.
- Combining Linux commands using pipes.
- Recognizing insecure data protection methods.

## Result

- Status: Completed
- Password: Successfully retrieved
- Next Level: Bandit Level 12

The actual password and its ROT13
representation are intentionally omitted.

## Reference

https://overthewire.org/wargames/bandit/bandit11.html

---

Part of my hands-on cybersecurity learning journey.
