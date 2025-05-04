# Bandit Writeup

## Level 0 
- **Password:** bandit0
- **What is Expected:** It is provided.
- **What I did:** It’s given.

## Level 0-1
- **Password:** ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
- **What is Expected:** Read a file called `readme`.
- **What I did:** 
  ```bash
  cat readme

## Level 2-3
- **Password:** MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
- **What is Expected:** File called spaces in this filename.
- **What I did:** 
  ```bash
  Used the Tab key to autocomplete the file name:
  cat "spaces in this filename"

## Level 3-4
- **Password:** 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
- **What is Expected:** Hidden file inside the inhere directory.
- **What I did:** 
  ```bash
    cat inhere/.hidden

## Level 4-5
- **Password:** 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
- **What is Expected:** Human-readable file inside inhere directory.
- **What I did:** 
  ```bash
    file ./-*

## Level 5-6
- **Password:** HWaSNphtq9AVKe0dmk45nxy20cvUa6EG
- **What is Expected:**
        Human-readable file
        1033 bytes in size
        Not executable
- **What I did:** 
  ```bash
    find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII

        -type f: Find files only.

        -size 1033c: Exactly 1033 bytes (c means bytes).

        ! -executable: Not executable files.

        file '{}' \;: Identify the file type.

        grep ASCII: Find human-readable (ASCII) files.

## Level 6-7
- **Password:** morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
- **What is Expected:**
        Owned by user bandit7
        Owned by group bandit6
        33 bytes in size
- **What I did:** 
  ```bash
    find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null

        2>/dev/null hides permission denied errors.

## Level 7-8
- **Password:** dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
- **What is Expected:** File data.txt, find next to word "millionth".
- **What I did:** 
  ```bash
    grep "millionth" data.txt

## Level 8-9
- **Password:** 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
- **What is Expected:** Password stored in data.txt — appears only once.
- **What I did:** 
  ```bash
    sort data.txt | uniq -u

## Level 9-10
- **Password:** FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
- **What is Expected:** Human-readable strings inside data.txt.
- **What I did:** 
  ```bash
    strings data.txt | grep "=="

## Level 10-11
- **Password:** dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
- **What is Expected:** File data.txt contains base64 encoded data.
- **What I did:** 
  ```bash
    cat data.txt
    base64 -d data.txt

    Base64 is a binary-to-text encoding.

    Recognized by padding characters = at the end.

## Level 11-12
- **Password:** 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
- **What is Expected:** The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
- **What I did:** 
  ```bash
    Cat data.txt | tr ‘A-Za-z’ ‘N-ZA-Mn-za-m’
Tr ‘A-Za-z’ ‘N-ZA-Mn-za-m’ command performs character transformation. 
A-Za-z specifies the range citing both upper and lower case.
N-ZA-Mn-za-m This is the mapping for the ROT13 transformation. It shifts each letter by 13 positions.

## Level 12-13
- **Password:** FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
- **What is Expected:** The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level, it may be useful to create a directory under /tmp in which you can work using mkdir.
- **What I did:** 
  ```bash
  I had to decompress many times from data file. The use of file command to Identify the type of data stored in the file. 
  The compressed commands include tar xf, gunzip and bunzip2. 

## Level 13-14
- **Password:** 
- **What is Expected:** The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on
- **What I did:** 
  ```bash
  I started with ls, Listed the sshkey.private file that helps in connecting to bandit14. chmod 700 sshkey.private to make the file an executable, got a permission denied and resulted in using the ssh key as follows : ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

## Level 14-15
- **Password:** 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
- **What is Expected:** The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
- **What I did:** 
  ```bash
  I cat /etc/bandit_pass/bandit14 to view the password to use in logging to the localhost 30000
  then I connected to localhost 30000 using nc localhost 30000 

## Level 15-16
- **Password:** kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
- **What is Expected:** The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption
- **What I did:** 
  ```bash
  openssl s_client -connect localhost:30001
Since the task highlighted that the passwd can be retrieved using the SSL encryption, I connected to the localhost server with OpenSSL client ad sent passwd from this level:
openssl s_client -connect localhost:30001
using password in level 14 to retrieve the password for the next level