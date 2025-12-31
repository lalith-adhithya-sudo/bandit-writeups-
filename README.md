OverTheWire Bandit – Personal Learning Notes (Level 0–15)

This document records my hands-on learning while working through the OverTheWire Bandit wargame.
Passwords are intentionally excluded. The focus is on the approach, commands used, and concepts learned.

##Level 0 – Getting In

I connected to the Bandit server using SSH on a non standard port.

Command used:
ssh bandit0@bandit.labs.overthewire.org
 -p 2220

This highlighted that services do not always run on default ports.

##Level 0 → 1 – Reading a File

I listed the files in the directory and read the available text file.

Commands used:
ls
cat readme

This reinforced the habit of checking the environment before doing anything else.

##Level 1 → 2 – When Filenames Fight Back

The file name started with a hyphen, which conflicted with normal command options.
Using a relative path solved the issue.

Command used:
cat ./-

This taught me how the shell interprets filenames before execution.

##Level 2 → 3 – Filenames With Spaces

The file name contained spaces, so it had to be quoted properly.

Command used:
cat "spaces in this filename"

Small syntax details like this can completely break commands if ignored.

##Level 3 → 4 – Hidden in Plain Sight

The password was stored in a hidden file.

Commands used:
ls -a
cat .hidden

This showed that hidden files are not protected — just not shown by default.

##Level 4 → 5 – Identifying the Right File

Inside a directory with many files, only one contained readable text.
I checked each file’s type before opening it.

Commands used:
cd inhere
file ./*
cat ./-file07

This introduced me to analyzing data formats instead of guessing.

##Level 5 → 6 – Filters Matter

The correct file had specific size and permission constraints.
Using filters made the search efficient.

Commands used:
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2

This demonstrated how powerful structured searching can be.

##Level 6 → 7 – Searching the Entire System

The password file was located somewhere in the system and had specific ownership.
Error output was suppressed to keep results readable.

Commands used:
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password

This level showed how noisy real systems can be and how to manage that noise.

##Level 7 → 8 – Finding Meaning in Noise

The password was buried inside a large text file.

Command used:
grep "millionth" data.txt

This showed how quickly targeted searching can extract useful information.

##Level 8 → 9 – Spotting the Odd One Out

Only one line in the file was unique.

Command used:
sort data.txt | uniq -u

This highlighted how simple tools can work together effectively.

##Level 9 → 10 – Reading Binary Data

The file wasn’t plain text. Extracting readable strings revealed the password.

Command used:
strings data.txt | grep "="

This reinforced that binary files can still contain human-readable data.

##Level 10 → 11 – Decoding Base64

The content was encoded using Base64.

Command used:
base64 -d data.txt

This helped clarify the difference between encoding and encryption.

##Level 11 → 12 – ROT13 Cipher

The text was encoded using a simple letter substitution.

Command used:
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

This showed how basic obfuscation techniques can be reversed easily.

##Level 12 → 13 – Layer by Layer

The file was repeatedly compressed using different formats.
I first reversed the hex dump, then identified and extracted each layer step by step.

Commands used:
xxd -r data.txt > data
file data

Extraction involved gzip, bzip2, and tar until the final text file was revealed.

This level taught patience and systematic analysis.

##Level 13 → 14 – SSH With a Private Key

Instead of a password, authentication was done using an SSH private key.

Command used:
ssh -i sshkey.private bandit14@localhost -p 2220

This mirrors real-world secure server access.

##Level 14 → 15 – Talking to a Secure Service

The final level here involved interacting with a local SSL service.

Command used:
openssl s_client -connect localhost:30001

After connecting, providing the previous password returned the next one.

This tied together networking and encrypted communication.


Current Status

Completed: Levels 0–15
In Progress: Levels 16–20
