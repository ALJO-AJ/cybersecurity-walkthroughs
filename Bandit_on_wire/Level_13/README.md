
# Bandit Level 13 → Level 14

## Objective

Understand SSH private key authentication
and Linux file access permissions.

## Topics Covered

- SSH authentication
- Public and private keys
- Identity files
- Linux file permissions
- Absolute and relative paths
- Localhost and loopback addresses
- SSH error troubleshooting

## Initial Enumeration

I inspected the available files and
identified an OpenSSH private key.

Commands explored:

- ls
- ls -al
- file
- man ssh

## SSH Authentication

SSH supports authentication using a
private key instead of a password.

The -i option specifies the identity
file used for authentication.

General syntax:

```bash
ssh -i <private-key> <user>@<host> -p <port>
```

The private key must remain confidential.

## Troubleshooting Localhost Connections

My initial SSH connections failed because
the game server restricts localhost SSH
connections between levels.

I learned that localhost and 127.0.0.1
refer to the loopback interface.

The server's error messages and supplied
hint file helped identify the restriction.

## Private Key Permissions

My initial client-side authentication
failed because the private key had
permissions of 0664.

SSH rejected the key because other users
could access it.

Recommended private key permissions:

```bash
chmod 600 <private-key>
```

Permission comparison:

| Mode | Owner | Group | Others |
|---|---|---|---|
| 664 | rw- | rw- | r-- |
| 600 | rw- | --- | --- |
| 400 | r-- | --- | --- |

## Linux Path Management

I encountered errors when attempting
to navigate directly into a regular file.

The cd command changes directories,
while cat reads file contents.

| Symbol | Meaning |
|---|---|
| / | Root directory |
| ~ | Home directory |
| . | Current directory |
| .. | Parent directory |

## Commands Explored

| Command | Purpose |
|---|---|
| ls | List directory contents |
| ls -al | Detailed file information |
| file | Identify file type |
| cat | Read file contents |
| cd | Change directory |
| man ssh | Read SSH documentation |
| ssh -i | Specify SSH identity file |
| chmod | Modify file permissions |

## Security Concepts

- Asymmetric cryptography
- Public key authentication
- Private key confidentiality
- Principle of least privilege
- Linux access control
- Server-side connection restrictions

## Lessons Learned

- Read error messages carefully.
- Protect private keys from other users.
- Verify file permissions before authentication.
- Understand absolute and relative paths.
- Distinguish regular files from directories.
- Understand the purpose of loopback addresses.
- Identify the network service before connecting.

## Result

Status: Completed

SSH private key authentication was successful,
and the next level credential was recovered.

Passwords, private keys and challenge-specific
solutions are intentionally omitted.

## Reference

https://overthewire.org/wargames/bandit/bandit13.html

---

Part of my hands-on cybersecurity learning journey.
