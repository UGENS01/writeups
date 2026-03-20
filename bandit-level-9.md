# OverTheWire Bandit — Level 9

## Goal
Find the password stored in data.txt among
human readable strings preceded by several
= characters.

## Commands Used
ls
strings data.txt | grep "=="

## Solution
Used ls to list files in the home directory
which revealed data.txt.

Tried grep directly on data.txt first but
it returned "binary file matches" — meaning
grep could not read the binary content properly.

Understood that strings was needed first to
extract human readable text from the binary
file before grep could search through it.

Combined both commands using a pipe:
strings data.txt | grep "=="

Breaking down the command:
- strings data.txt = extracts all human
  readable strings from the binary file
- | = pipe — transfers standard output (1)
  from strings directly into grep
  functioning like a bridge between commands
- grep "==" = searches the extracted strings
  for lines containing == characters

This returned the password preceded by
several = signs.

## What I Learned
- Binary files cannot be searched with grep
  directly — it returns "binary file matches"
- strings extracts human readable text from
  binary files — pulling readable content
  out of otherwise unreadable data
- Piping transfers standard output of one
  command directly into the next command
- Piping could be replaced with input
  redirection < in some cases but piping
  is cleaner when chaining commands
- file command identifies file type
- strings command extracts readable content
- grep then searches that extracted content
- The three commands work together as a
  powerful combination for binary analysis

## Key Commands Reference
strings file          = extract readable text
                        from any file
strings file | grep   = extract then search
binary file matches   = grep cannot read
                        binary data directly
|                     = pipe — bridges output
                        of one command into
                        input of next command
