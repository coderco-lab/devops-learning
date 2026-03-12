# Text Processing Notes

## grep examples

```bash
grep "error" /var/log/syslog
grep -r "TODO" ~/projects/
grep -i "failed" /var/log/auth.log | wc -l
```

## awk examples

```bash
ps aux | awk '{print $1, $11}'
cat /etc/passwd | awk -F: '{print $1, $6}'
```

## sed examples

```bash
sed 's/old/new/g' file.txt
sed -n '10,20p' file.txt
```

## Piping example

```bash
cat /var/log/syslog | grep "error" | awk '{print $1, $2, $3}' | sort | uniq
```

## Challenge completed

Parse `/etc/passwd` to list all users with `/bin/bash` as their shell.

```bash
awk -F: '$7=="/bin/bash" {print $1}' /etc/passwd
```

## What this command does

- `-F:` tells awk to use `:` as the field separator
- `$7=="/bin/bash"` checks the shell field
- `{print $1}` prints the username field

## Extra useful commands

Find lines containing root:

```bash
grep "root" /etc/passwd
```

Print lines 1 to 5 from a file:

```bash
sed -n '1,5p' /etc/passwd
```

List usernames and shells:

```bash
awk -F: '{print $1, $7}' /etc/passwd
```
