# OverTheWire Bandit — Level 3

## Goal
Find the password hidden inside a file inside 
a folder called inhere. The file is hidden.

## Commands Used
ls
cat inhere
cd inhere
ls
find
cat "./...Hiding-From-You"

## What Went Wrong First
- cat inhere failed because inhere is a 
  directory not a file. cat only reads files.
- ls inside the inhere folder showed nothing
  because the file is hidden. Hidden files in
  Linux start with a dot and are invisible 
  to normal ls.

## Solution
Used find command inside the inhere directory
which revealed a hidden file called:
...Hiding-From-You

Then read it using:
cat "./...Hiding-From-You"

This revealed the password for Level 4.

## What I Learned
- cd foldername moves you into a directory
- cat cannot read directories, only files
- Hidden files in Linux start with a dot .
- Normal ls does not show hidden files
- ls -la shows ALL files including hidden ones
- find command reveals hidden files in the
  current directory
- Hidden files are commonly used in Linux to
  store configuration and sensitive data
- Always try find if ls shows nothing

## Key Commands Reference
ls          = list visible files only
ls -la      = list ALL files including hidden
cd folder   = move into a folder
find        = show all files including hidden
cat ./file  = read a file in current directory
