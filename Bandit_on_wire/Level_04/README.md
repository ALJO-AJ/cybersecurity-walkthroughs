# Bandit Level 4 → Level 5

## Objective
Find the only human-readable file among several files in the `inhere` directory.

## Login Information
- Current user: `bandit4`
- Working directory: `/home/bandit4/inhere`
- Target file: `-file07`

## Commands Used

### 1. Identify the current user
```bash
whoami
```

### 2. Check the working directory
```bash
pwd
```

### 3. List files
```bash
ls
```

### 4. Display detailed file information
```bash
ls -l
```

This showed ten files with similar sizes and permissions.

### 5. Identify file types
```bash
file ./*
```

This examined all files in the current directory and displayed their types.

The target file was identified as:
```text
./-file07: ASCII text
```

### 6. Read the human-readable file
```bash
cat ./-file07
```

Successfully retrieved the next-level password.

## Mistakes and Troubleshooting

Initially, I tried:
```bash
file -type -file*
```

This failed because `-type` is not a valid option for the `file` command, and filenames beginning with hyphens can be interpreted as options.

The correct command was:
```bash
file ./*
```

## What I Learned

- How to identify file types using `file`.
- How shell wildcards (`*`) work.
- Why `./` is useful for filenames beginning with hyphens.
- How to distinguish human-readable text from binary or other data files.
- How to troubleshoot invalid command options.

## Security Note
The next-level password is not included in this public documentation.

## Status
Completed — successfully identified and read the human-readable file.