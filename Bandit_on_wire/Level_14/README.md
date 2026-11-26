
# Bandit Level 14 → Level 15

## Objective

Understand TCP communication and interact
with a network service using Netcat.

## Topics Covered

- TCP connections
- Network ports
- Netcat
- Client-server communication
- Loopback addresses
- Application-layer protocols
- Source and destination ports
- Linux command syntax

## Step 1: Initial Enumeration

I inspected the home directory and
located the required credential file.

During enumeration, I encountered
errors while attempting to navigate
into a regular file using cd.

## File and Directory Management

The cd command is used to change
directories, while cat reads files.

| Command | Purpose |
|---|---|
| cd | Change directory |
| cat | Read file contents |
| ls | List directory contents |
| pwd | Display current directory |

## Step 2: Initial Connection Attempt

I initially attempted to communicate
with the target service using SSH.

The connection was closed by the server.

### Reason

SSH uses its own application-layer
protocol and expects an SSH server.

A TCP service does not necessarily
support SSH.

Changing the destination port does
not change the application protocol.

## Step 3: Exploring Netcat

Netcat is a networking utility used
to send and receive data through
TCP and UDP connections.

General syntax:

```bash
nc <hostname> <port>
```

## Step 4: Troubleshooting Netcat Syntax

Initially, I attempted to specify the
destination port using the -p option.

Netcat displayed its usage information.

After examining the usage information,
I understood that -p specifies the
source port in this Netcat version.

The destination port is supplied as
a positional argument.

## Source vs Destination Port

- Source port identifies the client-side
  endpoint of a network connection.
- Destination port identifies the
  service the client connects to.
- The operating system normally assigns
  an available source port automatically.

## Port Syntax Comparison

| Command | Port specification |
|---|---|
| SSH | ssh user@host -p PORT |
| SCP | scp -P PORT |
| Netcat | nc host PORT |
| Netcat source port | nc -p SOURCE host DESTINATION |

## Step 5: Successful Communication

After correcting the command syntax,
I established a TCP connection with
the intended service.

I submitted the required credential,
which the server validated successfully.

The next level credential was returned.

## SSH vs Netcat

| Feature | SSH | Netcat |
|---|---|---|
| Encryption | Yes | No by default |
| Remote shell | Supported | Not by default |
| Authentication | Supported | Not built in |
| Raw TCP communication | Not by default | Supported |
| UDP communication | Not normally | Supported |

## Commands Explored

| Command | Purpose |
|---|---|
| ls | List files |
| cd | Navigate directories |
| cat | Read file contents |
| ssh | Secure remote connection |
| nc | TCP and UDP communication |

## Security Concepts

### Plain-text Communication

Ordinary Netcat TCP connections do not
provide encryption by default.

Sensitive information transmitted over
unencrypted networks may be intercepted.

### Loopback Address

Localhost refers to the current machine.

The IPv4 loopback address is 127.0.0.1.

### Application-Layer Protocols

Different network services expect
different communication protocols.

A successful TCP connection alone
does not guarantee that the client
uses the correct application protocol.

## Lessons Learned

- Identify the service before connecting.
- SSH cannot communicate with every TCP service.
- Command options differ between utilities.
- Source and destination ports are different.
- Read usage information and error messages.
- Netcat is useful for network troubleshooting.
- Understand the difference between encrypted
  and unencrypted communication.

## Result

- Status: Completed
- TCP connection: Successful
- Credential validation: Successful
- Next level credential: Retrieved

Passwords and challenge-specific solutions
are intentionally omitted.

## Reference

https://overthewire.org/wargames/bandit/bandit14.html

---

Part of my hands-on cybersecurity learning journey.
