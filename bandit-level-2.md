# OverTheWire Bandit — Level 2

## Goal
Read a file called --spaces in this filename-- 
stored in the home directory to find the 
password for Level 3

## Commands Used
ls
cat "./--spaces in this filename--"

## What Went Wrong First
- cat --spaces treated --spaces as a command
  option not a filename
- cat "spaces in this file name" failed because
  the filename was typed incorrectly
- cat spaces\ in\ this\ filename failed because
  the -- dashes at start and end were missing

## Solution
First used ls to see the exact filename which
revealed: --spaces in this filename--

The filename had three tricky elements:
1. Dashes -- at the start
2. Spaces in the middle  
3. Dashes -- at the end

Used quotes and ./ together to handle both
the dashes and the spaces:
cat "./--spaces in this filename--"

This revealed the password for Level 3.

## What I Learned
- Always run ls first to see exact filenames
- Filenames starting with -- need ./ prefix
- Spaces in filenames need quotes around them
- Combining ./ and quotes handles both problems
- Tab autocomplete avoids all these issues
- Backslash at end of command creates > prompt
- Press Ctrl+C to cancel unwanted commands
