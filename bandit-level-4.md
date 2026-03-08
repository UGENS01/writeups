# OverTheWire Bandit — Level 4

## Goal
Find the only human-readable file among 10 files
inside the inhere directory. Only one file contains
the password — the rest contain binary garbage.

## Commands Used
cd inhere
ls
find
cat ./-file00
cat ./-file01
file ./-file0*
cat ./-file0[number that showed ASCII text]

## What Went Wrong First
- Tried cat ./-file00 — showed random symbols
  and garbled characters. This is binary data,
  not human readable text.
- Tried cat ./-file01 — same result. Binary garbage.
- Opening binary files blindly is inefficient and
  can crash your terminal in real situations.

## Solution
Used the file command with a wildcard * to check
all 10 files simultaneously:
file ./-file0*

This showed the file type of every file at once.
Nine files showed "data" meaning binary content.
One file showed "ASCII text" meaning human readable.

Read only that file:
cat ./-file0[X]

This revealed the password for Level 5.

## What I Learned
- Binary files contain unreadable data and show
  as garbled symbols when opened with cat
- The file command identifies what type of data
  is inside a file without opening it
- ASCII text means human readable — always the
  password file in these challenges
- Wildcards like * match multiple files at once
  saving enormous time
- file ./-file0* checks all 10 files in one command
  instead of 10 separate commands
- Never open unknown files blindly — always check
  the file type first with the file command
- In real pentesting, file command helps identify
  interesting files among thousands quickly

## Key Commands Reference
file filename     = identify what type of data 
                    is inside a file
file ./*          = check file type of every 
                    file in current directory
file ./-file0*    = check all files starting 
                    with -file0
*                 = wildcard meaning match anything
ASCII text        = human readable text file
data              = binary non-readable file
