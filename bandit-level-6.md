# OverTheWire Bandit — Level 6

## Goal
Find the password stored somewhere on the 
entire server — not just the home directory.
The file has three specific properties:
- Owned by user bandit7
- Owned by group bandit6
- Exactly 33 bytes in size

## Commands Used
find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password

## What Went Wrong First
- Tried grep word with no filename — it waited
  for keyboard input. Cancelled with Ctrl+C.
- Tried cat ./bash_logout — failed because the
  file is hidden and needs a dot before the name
- Tried cat ./.bash_logout — worked but showed
  a system logout script, not the password
- Ran find without 2>/dev/null first — hundreds
  of Permission denied errors flooded the screen
  making it impossible to read the output
- Tried cat ./var/lib/dpkg/info/bandit7.password
  — failed because ./ cannot be combined with
  an absolute path starting with /

## Solution
Searched the entire system using find with
three specific conditions simultaneously:

find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null

Breaking down the command:
- find /         = search entire system from root
- -type f        = files only not folders
- -size 33c      = exactly 33 bytes (c = bytes)
- -user bandit7  = owned by user bandit7
- -group bandit6 = owned by group bandit6
- 2>/dev/null    = hide all Permission denied
                   errors silently

find returned exactly one result:
/var/lib/dpkg/info/bandit7.password

Read it using the full absolute path:
cat /var/lib/dpkg/info/bandit7.password

This revealed the password for Level 7.

## What I Learned
- find / searches the ENTIRE system not just
  current directory
- -user and -group flags filter by file ownership
- Two types of output channels exist in Linux:
  1 = standard output (normal results)
  2 = standard error (error messages)
- 2>/dev/null redirects error messages to the
  void — deleting them silently
- /dev/null is a special Linux black hole that
  destroys everything sent to it
- 2>/dev/null does NOT grant permission to
  locked files — it only hides the error messages
- Absolute paths start with / and go from root
- Relative paths start with ./ and go from
  current directory
- Never combine ./ with an absolute path
- grep was not needed here because find's own
  flags were precise enough to return only
  one result

## Key Commands Reference
find / -user username     = find files owned 
                            by specific user
find / -group groupname   = find files owned
                            by specific group
2>/dev/null               = hide error messages
/dev/null                 = Linux void/black hole
cat /full/path/to/file    = read file using
                            absolute path
cat ./relative/file       = read file using
                            relative path

## Absolute vs Relative Paths
/var/lib/file    = absolute — starts from root
./var/lib/file   = relative — starts from here
Never mix both together
