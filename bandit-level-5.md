# OverTheWire Bandit — Level 5

## Goal
Find the password hidden somewhere inside 20 folders
in the inhere directory. The correct file has three
specific properties:
- Human readable
- Exactly 1033 bytes in size
- Not executable

## Commands Used
ls
cd inhere
ls
cd maybehere0*   (failed)
cd maybehere00
ls
cd ..
find . -type f -size 1033c ! -executable
cat "./maybehere07/.file2"

## What Went Wrong First
- Tried cd maybehere0* to enter all folders at once
  but got error "too many arguments"
- cd can only move into one folder at a time
- Went into maybehere00 manually and found 6 files
  but did not know which one was correct
- Going through all 20 folders manually would take
  forever — a smarter approach was needed

## Solution
Went back to inhere folder using cd ..
Then used find with specific properties to search
all 20 folders simultaneously:

find . -type f -size 1033c ! -executable

Breaking down the command:
- find .       = search from current directory
- -type f      = look for files not folders
- -size 1033c  = exactly 1033 bytes in size
                 (c means bytes)
- ! -executable = NOT an executable/green file

find instantly returned one result:
./maybehere07/.file2

Note: the dot before file2 means it is a hidden
file — it starts with a dot making it invisible
to normal ls.

Read the file using:
cat "./maybehere07/.file2"

This revealed the password for Level 6.

## What I Learned
- cd only works on one folder at a time
- cd * fails because * expands to multiple folders
- find is extremely powerful for searching with
  specific file properties simultaneously
- -type f finds files, -type d finds folders
- -size 1033c means exactly 1033 bytes
- c after a number in find means bytes
- k = kilobytes, M = megabytes, G = gigabytes
- ! -executable means NOT executable
- Green files in terminal = executable files
- A dot before a filename = hidden file
- find searches all subfolders automatically
- The . in find . means start from here

## Key Commands Reference
find . -type f              = find all files here
find . -type d              = find all folders here  
find . -size 1033c          = find files 1033 bytes
find . ! -executable        = find non-executable
find . -type f -size 1033c ! -executable = combine
                              all conditions at once
