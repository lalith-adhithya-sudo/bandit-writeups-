##Level 0 – Getting In

The first step was connecting to the Bandit server using SSH on a non-standard port.

Command used:
ssh bandit0@bandit.labs.overthewire.org
 -p 2220

This immediately highlighted that real systems often run services on custom ports.

##Level 0 → 1 – Reading a File

After logging in, I explored the directory and read the available text file.

Commands used:
ls
cat readme

This reinforced the habit of checking the environment before taking action.

##Level 1 → 2 – When Filenames Fight Back

The filename started with a hyphen, which conflicted with normal command options.
Using a relative path solved the issue.

Command used:
cat ./-

This taught me how the shell interprets arguments and filenames.

##Level 2 → 3 – Filenames With Spaces

The file name contained spaces, so it had to be handled carefully.

Command used:
cat "spaces in this filename"

This showed how small syntax details can completely break commands.

##Level 3 → 4 – Hidden in Plain Sight

The required file was hidden and not visible with a normal directory listing.

Commands used:
ls -a
cat .hidden

This showed that hidden files are not secure, just hidden by default.

##Level 4 → 5 – Identifying the Right File

Inside a directory with many files, only one contained readable text.
Instead of guessing, I checked the file type of each one.

Commands used:
cd inhere
file ./*
cat ./-file07

This introduced the importance of understanding file formats.

##Level 5 → 6 – Filters Matter

The correct file had specific size and permission constraints.
Using search filters made the process efficient and precise.

Commands used:
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2

This demonstrated the power of structured searching.

##Level 6 → 7 – Searching the Entire System

The file was located somewhere in the system and had specific ownership requirements.
Error messages were suppressed to keep output readable.

Commands used:
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password

This level showed how noisy real systems can be.

##Level 7 → 8 – Finding Meaning in Noise

The password was buried inside a large text file.

Command used:
grep "millionth" data.txt

This showed how powerful targeted searching can be.

##Level 8 → 9 – Spotting the Odd One Out

Most lines in the file were duplicated, with only one unique line.

Command used:
sort data.txt | uniq -u

This showed how simple tools work together effectively.

##Level 9 → 10 – Reading Binary Data

The file wasn’t plain text. Extracting readable strings revealed useful information.

Command used:
strings data.txt | grep "="

This reinforced that binary files can still contain readable data.

##Level 10 → 11 – Decoding Base64

The content was encoded using Base64.

Command used:
base64 -d data.txt

This helped clarify the difference between encoding and encryption.

##Level 11 → 12 – ROT13 Cipher

The data used a simple letter substitution cipher.

Command used:
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

This showed how basic obfuscation techniques can be reversed easily.

##Level 12 → 13 – Layer by Layer

The file was repeatedly compressed using different formats.
I first reverted the hex dump, then identified and extracted each layer step by step.

Commands used:
xxd -r data.txt > data
file data

Extraction involved gzip, bzip2, and tar until the final text file was revealed.

This level required patience and systematic analysis.

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

The above given details are my understanding about the tasks i did in bandit. 
will continue to work upon it.

Below is my Current Status:-

Completed: Levels 0–15
In Progress: Levels 16–20
