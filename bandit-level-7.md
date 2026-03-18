# OverTheWire Bandit — Level 7

## Goal
Find the password stored in a file called 
data.txt next to the word "millionth"

## Commands Used
ls
grep "millionth" data.txt

## Solution
Used ls to confirm data.txt existed in the
home directory.

Used grep to search inside data.txt for the
word "millionth":
grep "millionth" data.txt

grep instantly returned the line containing
the word millionth alongside the password.

## What I Learned
- grep searches INSIDE files for specific words
- grep "word" filename returns only lines
  containing that word
- data.txt contained millions of lines but
  grep found the right one instantly
- grep is extremely fast regardless of file size
- This is exactly how grep is used in real
  pentesting — searching large files for
  specific keywords like "password" or "secret"

## Why This Level Was Fast
Previous levels taught the right tools at
the right time. grep was already understood
before attempting this level — making the
solution immediate and obvious.

## Real World Application
On a real penetration test after gaining
access to a Linux system:
grep -r "password" /var/
grep -r "secret" /etc/
grep -r "key" /home/
These commands search entire directories
for sensitive keywords instantly.

## Key Commands Reference
grep "word" file     = find lines containing
                       word in file
grep -r "word" .     = search all files in
                       current directory
grep -i "word" file  = case insensitive search
grep -n "word" file  = show line numbers
