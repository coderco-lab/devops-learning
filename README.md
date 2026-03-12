# DevOps Linux Fundamentals
This repository captures my learning while completing the Linux module of a DevOps training program. The main goal of this module is to become comfortable working in the Linux command line, since most modern production infrastructure runs on Linux systems.
The exercises and notes here cover fundamental areas such as navigating the system, managing files, handling permissions, controlling processes, and using text-processing utilities. These core abilities serve as the foundation for later DevOps technologies like Docker, Kubernetes, CI/CD pipelines, and cloud platforms.
# Module Objectives
By completing this module, the following skills were developed:

• Navigating the Linux file system using the terminal
• Creating, copying, moving, and deleting files and directories
• Understanding file permissions and ownership
• Monitoring and managing system processes
• Using command-line tools such as `grep`, `awk`, `sed`, and `find`
• Completing Levels 1–20 of the Bandit challenge

# Linux Environment
The Linux practice environment was set up using one of the following options:

• Local Linux installation
• Virtual machine
• Cloud instance using Amazon EC2 on AWS
• Browser-based Linux lab

Basic verification commands used after setup:

```
uname -a
whoami
pwd
```

# Core Skills Practiced

## File System Navigation
Common commands used while learning the Linux directory structure:

```
cd /var/log
ls -lah
pwd
```

## File Operations
Basic commands for creating and managing files and directories:

```
touch test.txt
mkdir -p projects/demo
cp test.txt projects/demo/
mv projects/demo/test.txt projects/demo/backup.txt
rm projects/demo/backup.txt
```

## Viewing Files
Commands used to read and inspect files directly from the terminal:

```
cat /etc/passwd
less /var/log/syslog
head -n 20 /etc/services
tail -f /var/log/auth.log
```

## Permissions and Ownership
A simple bash script was created and file permissions were adjusted:

```
echo '#!/bin/bash
echo "Hello DevOps"' > hello.sh
chmod +x hello.sh
./hello.sh
sudo chown root:root hello.sh
ls -l hello.sh
```

Example permission output:

```
-rwxr-xr-x 1 root root 32 Nov 29 10:00 hello.sh
```

Permission meaning:

• Owner: read, write, execute
• Group: read, execute
• Others: read, execute

## Process Management
Commands used to inspect and manage running processes:

```
ps aux
ps aux | grep nginx
top
htop
```

Example of running a background job:

```
sleep 100 &
jobs
kill <PID>
```

## Text Processing
Linux tools used for searching and processing text data:

```
grep "error" /var/log/syslog
grep -r "TODO" ~/projects/
grep -i "failed" /var/log/auth.log | wc -l
```

Examples using `awk` and `sed`:

```
ps aux | awk '{print $1, $11}'
cat /etc/passwd | awk -F: '{print $1, $6}'
sed 's/old/new/g' file.txt
sed -n '10,20p' file.txt
```

Example command pipeline:

```
cat /var/log/syslog | grep "error" | awk '{print $1, $2, $3}' | sort | uniq
```

# Linux Bandit Challenge
Levels 1–20 of the Bandit wargame were completed through the OverTheWire challenge platform.

The Bandit challenges help build Linux proficiency by solving practical tasks such as locating hidden files, decoding encoded data, handling file permissions, and working with compressed archives.

Solutions and notes for these challenges are included in this repository.

# Why Linux Matters in DevOps
Linux forms the foundation of most modern cloud and server infrastructure. Strong command-line skills make it easier to manage servers, build containers, write automation scripts, and maintain deployment pipelines.

Developing Linux fundamentals early creates a strong base for learning the rest of the DevOps ecosystem.

# Next Steps
Planned topics to focus on after completing this module:

• Docker containerization
• CI/CD pipelines
• Infrastructure automation
• Cloud infrastructure on AWS 🚀
