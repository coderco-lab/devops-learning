# Permissions and Ownership Notes

## Create a script

```bash
echo '#!/bin/bash
echo "Hello DevOps"' > hello.sh
```

## Make it executable

```bash
chmod +x hello.sh
```

## Run it

```bash
./hello.sh
```

## Change ownership

```bash
sudo chown root:root hello.sh
```

## Check permissions

```bash
ls -l hello.sh
```

Example output:

```bash
-rwxr-xr-x 1 root root 32 Nov 29 10:00 hello.sh
```

## Permission breakdown

- `rwx` for owner means read, write, execute
- `r-x` for group means read and execute
- `r-x` for others means read and execute

## Challenge command

Create a file where only you can read and write, while others can only read:

```bash
touch private-notes.txt
chmod 644 private-notes.txt
```

## Extra useful permission examples

Only you can read and write:

```bash
chmod 600 secret.txt
```

Everyone can read, write, and execute:

```bash
chmod 777 test.sh
```

Owner full access, group read only, others no access:

```bash
chmod 740 report.txt
```
