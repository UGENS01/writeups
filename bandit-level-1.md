# OverTheWire Bandit — Level 1

## Goal
Read a file called - (a single dash) stored
in the home directory to find the password
for Level 2.

## Commands Used
ls
cat -
cat ./-

## What Went Wrong First
Tried cat - directly but it failed because
Linux interpreted the dash as a command
option not a filename. Linux reads anything
starting with - as an instruction to the
command rather than a file to read.

## Solution
Used ./ before the filename to tell Linux
to look in the current directory for a file
called - rather than interpreting it as
a command option:
cat ./-

This revealed the password for Level 2.

## What I Learned
- Files can be named with special characters
  like a single dash -
- Linux interprets - as a command option
  not a filename when used directly
- ./ means "look in current directory for"
  and forces Linux to treat what follows
  as a filename not an instruction
- ./ bypasses Linux interpretation rules
  and goes directly to the exact file named
- This is different from hidden files which
  start with a dot and need ls -la to reveal

## Key Commands Reference
cat -        = reads from keyboard not a file
cat ./-      = reads file called - in current
               directory
./           = look in current directory for
               this exact filename
