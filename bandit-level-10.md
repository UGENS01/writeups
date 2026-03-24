# OverTheWire Bandit — Level 10

## Goal
Find the password stored in data.txt which
contains data encoded in Base64.

## Commands Used
ls
cat data.txt
base64 data.txt
base64 -d data.txt

## What Went Wrong First
Ran base64 data.txt without the -d flag.
This encoded the already encoded data again
producing even more random looking output.
base64 without -d encodes — not decodes.

## Solution
Used base64 with the -d flag to decode
the contents of data.txt:
base64 -d data.txt

This converted the Base64 encoded text back
into human readable text revealing the password.

## What Base64 Is
Base64 is a way of converting binary data
into readable text using only 64 safe characters:
- Letters A-Z and a-z
- Numbers 0-9
- Plus + and slash /

It is an encoding not an encryption — meaning
it provides zero security. Anyone can decode
it instantly. It exists purely to make binary
data safe to transmit through text based systems.

## How to Recognize Base64
- Looks like random letters and numbers
- Almost always ends with = or ==
- Uses only letters, numbers, + and /
- No special characters or spaces

## What I Learned
- base64 without -d encodes data
- base64 -d decodes data back to readable text
- Base64 is encoding not encryption
- It provides zero security — anyone can decode it
- Base64 ends with = or == almost always
- Recognizing Base64 on sight is an essential
  cybersecurity skill

## Real World Importance
Base64 appears constantly in cybersecurity:
- Malware hides malicious code in Base64
  to avoid detection by antivirus software
- JWT (JSON Web Tokens) use Base64 encoding
- Email attachments are Base64 encoded
- Many CTF challenges hide flags in Base64
- Web application tokens often use Base64

## Key Commands Reference
base64 filename      = encode file to Base64
base64 -d filename   = decode Base64 back
                       to readable text
-d                   = decode flag
