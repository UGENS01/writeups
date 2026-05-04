OverTheWire: Bandit — Level 12 → Level 13
🎯 Objective
The password for the next level is stored in data.txt, which is a hexdump of a file that has been repeatedly compressed. The goal is to reverse the hexdump and peel back every layer of compression until the password is recovered.

📚 Concepts Covered
ConceptExplanationHexdumpA text representation of binary data in hexadecimal (base-16) format. Used for inspecting binary files in a human-readable form.xxdA command-line tool that creates hexdumps or converts hexdumps back to binary.fileA command that identifies the type of a file based on its internal structure (magic bytes), not its extension.gzip / gunzipGNU zip compression format. Commonly used for single-file compression.bzip2 / bunzip2A block-sorting compression algorithm — typically compresses better than gzip but is slower.tarTape Archive — bundles multiple files into one. Often combined with gzip or bzip2 for .tar.gz or .tar.bz2 archives./tmp directoryA world-writable temporary directory in Linux where any user can create and edit files.chmodChange mode — modifies file permissions.

🛠️ Tools Used

ssh (Secure Shell) — remote login
xxd — hexdump and reverse hexdump
file — file type detection
cp, mv — file operations
gunzip, bunzip2, tar — decompression tools
mkdir — create directories
cat — display file contents


🔐 Login
bashssh bandit12@bandit.labs.overthewire.org -p 2220
Password: (password obtained from Level 11)

📝 Walkthrough
Step 1 — Examine the file
bashls
cat data.txt
The output is a hexdump — rows of hex values with ASCII interpretation on the right. This is binary data printed as text.
00000000: 1f8b 0808 dfcd eb66 0203 6461 7461 322e  .......f..data2.
00000010: 6269 6e00 013e 02c1 fd42 5a68 3931 4159  bin..>...BZh91AY
...

Step 2 — Create a working directory
Your home directory is read-only. All work must be done in /tmp:
bashmkdir /tmp/nullwork
cp ~/data.txt /tmp/nullwork/
cd /tmp/nullwork

Why /tmp? It is world-writable — every user on the system has write access here. Think of it like a public whiteboard you can draw on.


Step 3 — Reverse the hexdump
bashxxd -r data.txt > data.bin

xxd by default creates a hexdump.
The -r flag reverses the process — it reads hex text and outputs the original binary.
The result (data.bin) is now raw binary data, not human-readable text.


Step 4 — Identify and decompress in a loop
This is the core of the challenge. Run file first, then decompress based on what it reports. Repeat until the output is ASCII text.
bashfile data.bin
The general loop:
If file reports: gzip compressed data
bashmv data.bin data.bin.gz
gunzip data.bin.gz
# A new file appears — identify it again with `file`
If file reports: bzip2 compressed data
bashmv data.bin data.bin.bz2
bunzip2 data.bin.bz2
If file reports: POSIX tar archive
bashtar -xf data.bin
# tar extracts the inner file(s) — check what was extracted with `ls`

Tip: After each decompression, rename the output and run file again immediately. The file type changes every layer.


Step 5 — Read the password
After approximately 8 rounds of decompression, file will report:
data8: ASCII text
bashcat data8
The password for bandit13 is printed to the terminal.

💡 Key Takeaways

Extensions don't define file type in Linux — file reads the internal magic bytes, which is far more reliable.
Hexdumps are not encryption — they are just a different representation of data. xxd -r fully reverses them.
Working in /tmp is a common CTF (Capture The Flag) technique when your home directory is restricted.
Compression layers can be stacked arbitrarily — automated detection (file in a loop) is cleaner than guessing.


🔁 Automation (Bonus)
Once you understand the logic, a loop can handle all layers automatically:
bash#!/bin/bash
# Run from /tmp/nullwork after xxd -r step

f="data.bin"
while true; do
    type=$(file -b "$f")
    echo "Detected: $type"

    case "$type" in
        *gzip*)   mv "$f" "$f.gz"  && gunzip "$f.gz"  && f="${f%.gz}" ;;
        *bzip2*)  mv "$f" "$f.bz2" && bunzip2 "$f.bz2" && f="${f%.bz2}" ;;
        *tar*)    tar -xf "$f" && f=$(tar -tf "$f" | head -1) ;;
        *ASCII*)  echo "Password:"; cat "$f"; break ;;
        *)        echo "Unknown type: $type"; break ;;
    esac
done

This is not required to solve the level — it is included to illustrate how the logic can be expressed programmatically.


✅ Summary
StepActionCommand1Create workspacemkdir /tmp/nullwork && cp ~/data.txt /tmp/nullwork/2Reverse hexdumpxxd -r data.txt > data.bin3Detect file typefile data.bin4Decompress (repeat)gunzip / bunzip2 / tar -xf5Read passwordcat <final_file>

Written by NullScalpel — dual-tracking medicine and cybersecurity, one level at a time.
