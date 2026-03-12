# Bandit Levels 0 to 20

This file is written so you can drop it straight into your repo as a separate guide.

## Bandit Access

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Password for `bandit0`:

```text
bandit0
```

---

## Level 0 to Level 1

Goal: Read the `readme` file in the home directory.

```bash
ls
cat readme
```

Save the output password and use it to log into `bandit1`.

---

## Level 1 to Level 2

Goal: Read a file called `-`.

```bash
cat ./-
```

Why this works:
- `-` is treated specially by many commands
- `./-` tells Linux it is a file in the current directory

---

## Level 2 to Level 3

Goal: Read a file with spaces in the name.

```bash
cat "--spaces in this filename--"
```

Alternative:

```bash
cat -- --spaces\ in\ this\ filename--
```

---

## Level 3 to Level 4

Goal: Find the hidden file inside `inhere`.

```bash
cd inhere
ls -la
cat .hidden
```

---

## Level 4 to Level 5

Goal: Find the only human readable file inside `inhere`.

```bash
cd inhere
file ./*
cat ./-file07
```

Note: The exact file name shown by `file ./*` is the one to open.

---

## Level 5 to Level 6

Goal: Find the file under `inhere` which is:
- human readable
- 1033 bytes
- not executable

```bash
find inhere -type f -size 1033c ! -executable -exec file {} \; 
cat inhere/maybe_here07/.file2
```

Tip: Your exact path should match the result from `find`.

---

## Level 6 to Level 7

Goal: Find the file on the server which is:
- owned by user `bandit7`
- owned by group `bandit6`
- 33 bytes in size

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

---

## Level 7 to Level 8

Goal: Find the password in `data.txt` next to the word `millionth`.

```bash
grep "millionth" data.txt
```

---

## Level 8 to Level 9

Goal: Find the only line in `data.txt` which appears once.

```bash
sort data.txt | uniq -u
```

---

## Level 9 to Level 10

Goal: Find the password in `data.txt` among human readable strings, preceded by several `=` characters.

```bash
strings data.txt | grep "="
```

A tighter version:

```bash
strings data.txt | grep "^=*"
```

---

## Level 10 to Level 11

Goal: Decode the base64 content in `data.txt`.

```bash
base64 -d data.txt
```

---

## Level 11 to Level 12

Goal: Decode a ROT13 string in `data.txt`.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

---

## Level 12 to Level 13

Goal: `data.txt` is a hexdump of a repeatedly compressed file.

Work in `/tmp`.

```bash
mktemp -d
cd /tmp/tmp.xxxxxxxx
cp ~/data.txt .
xxd -r data.txt > data.bin
file data.bin
mv data.bin data.gz
gunzip data.gz
file data
mv data data.bz2
bunzip2 data.bz2
file data
mv data data.gz
gunzip data.gz
file data
mv data data.tar
tar -xf data.tar
file data5.bin
mv data5.bin data.tar
tar -xf data.tar
file data6.bin
mv data6.bin data.bz2
bunzip2 data.bz2
file data
mv data data.tar
tar -xf data.tar
file data8.bin
mv data8.bin data.gz
gunzip data.gz
cat data
```

Tip: Use `file <filename>` after each step to see what format comes next.

---

## Level 13 to Level 14

Goal: Use the private SSH key in the home directory to log into `bandit14`.

```bash
ls -la
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@localhost -p 2220
```

Once logged into `bandit14`:

```bash
cat /etc/bandit_pass/bandit14
```

---

## Level 14 to Level 15

Goal: Send the current password to port `30000` on localhost.

```bash
echo "CURRENT_PASSWORD" | nc localhost 30000
```

Replace `CURRENT_PASSWORD` with the password for `bandit14`.

---

## Level 15 to Level 16

Goal: Send the current password to port `30001` on localhost using SSL/TLS.

```bash
echo "CURRENT_PASSWORD" | openssl s_client -connect localhost:30001 -quiet
```

Replace `CURRENT_PASSWORD` with the password for `bandit15`.

---

## Level 16 to Level 17

Goal: Find the correct listening port between `31000` and `32000`, then submit the current password over SSL/TLS.

First scan the range:

```bash
nmap localhost -p 31000-32000
```

Then test the SSL enabled ports. One of them returns a private SSH key.

Example:

```bash
echo "CURRENT_PASSWORD" | openssl s_client -connect localhost:31790 -quiet
```

Save the private key to a file:

```bash
nano bandit17.key
chmod 600 bandit17.key
ssh -i bandit17.key bandit17@localhost -p 2220
```

---

## Level 17 to Level 18

Goal: Compare `passwords.old` and `passwords.new` and find the changed line.

```bash
diff passwords.old passwords.new
```

The line shown with `>` in `passwords.new` is the next password.

Cleaner extraction:

```bash
diff passwords.old passwords.new | grep ">" | awk '{print $2}'
```

---

## Level 18 to Level 19

Goal: The `.bashrc` logs you out when you SSH in.

Run a command directly without starting an interactive shell.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

---

## Level 19 to Level 20

Goal: Use the setuid binary in the home directory.

Inspect it first:

```bash
ls -l
./bandit20-do
```

Then use it to read the password file as `bandit20`:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

---

## Suggested Repo Structure

```text
devops-learning-linux/
├── README.md
├── notes.md
├── file-system-notes.md
├── permissions-notes.md
├── process-management-notes.md
├── text-processing-notes.md
├── hello.sh
└── bandit-solutions.md
```

---

## Notes

- Save each password as you go
- Some exact file names or ports may differ in your own session flow if you make mistakes and retry
- For Level 12, the repeated decompression path is best handled by checking `file` after every step
- For Level 16, the SSL port with the key is commonly found during the scan phase, but always trust your own `nmap` result first
