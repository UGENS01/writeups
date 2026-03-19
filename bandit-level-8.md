# OverTheWire Bandit — Level 8

## Goal
Find the password stored in data.txt that
is the only line of text that occurs once.
All other lines appear multiple times.

## Commands Used
ls
sort data.txt | uniq -u

## Solution
Used ls to confirm data.txt existed.

Used sort combined with uniq to find the
only unique line:
sort data.txt | uniq -u

Breaking down the command:
- sort data.txt  = sorts all lines 
                   alphabetically putting
                   duplicates next to each other
- |              = pipe — passes sorted output
                   to uniq
- uniq -u        = shows ONLY lines that
                   appear exactly once

This instantly returned the password.

## Why sort was needed before uniq
uniq only detects duplicates that are directly
next to each other. Without sorting first the
duplicates would be scattered throughout the
file and uniq would miss them.

sort brings all identical lines together first
then uniq can correctly identify which line
appears only once.

## What I Learned
- uniq filters duplicate lines from text
- uniq -u shows ONLY unique lines
- uniq -d shows ONLY duplicate lines
- uniq -c counts occurrences of each line
- uniq only works on adjacent duplicates
- sort must come before uniq in most cases
- The pipe | chains commands together
- sort | uniq is one of the most used
  command combinations in Linux
- < is input redirection — feeds a file
  as input to a command

## Real World Application
In real penetration testing this combination
is used constantly:

sort /var/log/auth.log | uniq -c | sort -rn
Reveals which IPs attempted the most logins
— used to detect brute force attacks

sort passwords.txt | uniq -u
Finds passwords that appear only once in
a leaked password database

## Key Commands Reference
sort file          = sort lines alphabetically
uniq file          = remove adjacent duplicates
uniq -u file       = show only unique lines
uniq -d file       = show only duplicate lines
uniq -c file       = count line occurrences
sort file | uniq   = full duplicate removal
sort file | uniq -u = find truly unique lines
