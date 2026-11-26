
# Bandit Level 12 → Level 13

## Objective

Retrieve the password from data.txt, which
contains a hexadecimal dump of a file that
has been repeatedly compressed and archived.

## SSH Connection

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

## Step 1: Initial Enumeration

```bash
ls
cat data.txt
```

The file contained a hexadecimal dump.

The initial bytes were:

```text
00000000: 1f8b 0808 ...
```

The hexadecimal signature 1f8b indicates
Gzip compressed data.

## Step 2: Create a Temporary Directory

```bash
mktemp -d
```

Output:

```text
/tmp/tmp.opLC0nLNGY
```

Navigate into the temporary directory:

```bash
cd /tmp/tmp.opLC0nLNGY
```

Copy the original file:

```bash
cp /home/bandit12/data.txt .
ls
```

Using a temporary directory provides a
writable workspace without modifying
the original file.

## Step 3: Reverse the Hexadecimal Dump

```bash
xxd -r data.txt data.bin
file data.bin
```

Output:

```text
data.bin: gzip compressed data
```

The -r option reverses a hexadecimal dump
into its original binary representation.

## Step 4: First Gzip Layer

```bash
mv data.bin data.gz
gzip -d data.gz
ls
file data
```

Output:

```text
data: bzip2 compressed data, block size = 900k
```

The Gzip command removed the .gz extension
and produced a file named data.

### Troubleshooting

I attempted to access the previous filename:

```bash
cat data.bin
mv data.bin data.bz2
```

Both commands failed because data.bin
no longer existed.

## Step 5: First Bzip2 Layer

```bash
mv data data.bz2
```

Initially, I used an incorrect command:

```bash
bz2 -d data.bz2
```

Output:

```text
Command 'bz2' not found
```

Correct command:

```bash
bzip2 -d data.bz2
file data
```

Output:

```text
data: gzip compressed data
```

## Step 6: Second Gzip Layer

```bash
mv data data.gz
gzip -d data.gz
file data
```

Output:

```text
data: POSIX tar archive (GNU)
```

## Step 7: First TAR Archive

List archive contents:

```bash
tar -tf data
```

Output:

```text
data5.bin
```

Extract the archive:

```bash
tar -xf data
ls
file data5.bin
```

Output:

```text
data5.bin: POSIX tar archive (GNU)
```

Unlike Gzip and Bzip2 decompression,
TAR extraction preserves the original
archive.

## Step 8: Second TAR Archive

```bash
tar -tf data5.bin
tar -xf data5.bin
ls
file *
```

Output:

```text
data:      POSIX tar archive (GNU)
data5.bin: POSIX tar archive (GNU)
data6.bin: bzip2 compressed data, block size = 900k
data.txt:  ASCII text
```

### Wildcard Troubleshooting

I initially executed:

```bash
file .*
```

Output:

```text
.*: cannot open `.*' (No such file or directory)
```

The pattern .* matches hidden filenames.
The correct command for the visible files
in this directory was:

```bash
file *
```

## Step 9: Second Bzip2 Layer

```bash
bzip2 -d data6.bin
```

Output:

```text
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
```

The decompression was successful.

Because the input filename did not have
a recognized Bzip2 extension, the command
used the .out extension for its output.

I attempted to rename the original file:

```bash
mv data6.bin data6.bz2
```

This failed because the original compressed
file had already been removed.

Identify the decompressed file:

```bash
file data6.bin.out
```

Output:

```text
data6.bin.out: POSIX tar archive (GNU)
```

## Step 10: Third TAR Archive

```bash
tar -tf data6.bin.out
```

Output:

```text
data8.bin
```

Initially, I attempted to identify data8.bin
before extracting it:

```bash
file data8.bin
```

Output:

```text
data8.bin: cannot open `data8.bin' (No such file or directory)
```

Listing an archive does not extract its files.

Correct procedure:

```bash
tar -xf data6.bin.out
ls
file data8.bin
```

Output:

```text
data8.bin: gzip compressed data
```

## Step 11: Final Gzip Layer

```bash
mv data8.bin data8.gz
gzip -d data8.gz
ls
file data8
```

Output:

```text
data8: ASCII text
```

## Step 12: Retrieve the Password

```bash
cat data8
```

Output:

```text
The password is [PASSWORD REDACTED]
```

The password was successfully recovered.

## Complete Extraction Sequence

| Stage | File | Format |
|---|---|---|
| Original | data.txt | Hexadecimal dump |
| Layer 1 | data.bin | Gzip |
| Layer 2 | data | Bzip2 |
| Layer 3 | data | Gzip |
| Layer 4 | data | TAR |
| Layer 5 | data5.bin | TAR |
| Layer 6 | data6.bin | Bzip2 |
| Layer 7 | data6.bin.out | TAR |
| Layer 8 | data8.bin | Gzip |
| Final | data8 | ASCII text |

## Commands Used

| Command | Purpose |
|---|---|
| ls | List files |
| ls -al | Detailed listing |
| mktemp -d | Create temporary directory |
| cd | Change directory |
| cp | Copy files |
| mv | Rename or move files |
| xxd -r | Reverse hexadecimal dump |
| file | Identify file format |
| gzip -d | Decompress Gzip |
| bzip2 -d | Decompress Bzip2 |
| tar -tf | List archive contents |
| tar -xf | Extract archive contents |
| cat | Display readable text |

## File Signatures

| Format | Common signature |
|---|---|
| Gzip | 1F 8B |
| Bzip2 | 42 5A 68 (BZh) |
| TAR (ustar format) | ustar at offset 257 |

File signatures help identify formats
regardless of filename extensions.

## Security Concepts

- Hexadecimal representation of binary data.
- File signature and magic byte analysis.
- File identification independent of extensions.
- Nested compression and archive extraction.
- Temporary directory management.
- Linux wildcard expansion.
- Binary versus ASCII data.
- Compression versus encryption.

Compression reduces data size or changes
its representation. It does not provide
confidentiality.

## Lessons Learned

- Always identify unknown files using file.
- Avoid displaying compressed binary files
  directly using cat.
- Verify filenames after decompression.
- TAR listing and extraction are different.
- TAR extraction preserves the original archive.
- File extensions do not determine file types.
- Bzip2 can decompress files without a .bz2
  extension.
- Repeatedly identify and extract each layer
  until readable text is recovered.

## Result

- Status: Completed
- Compression layers removed: 5
- TAR archives extracted: 3
- Total layers processed: 8
- Password: Successfully retrieved
- Next Level: Bandit Level 13

The actual password and complete hexadecimal
dump are intentionally omitted for security.

## Reference

https://overthewire.org/wargames/bandit/bandit12.html

---

Part of my hands-on cybersecurity learning journey.
