# Process Management Notes

## View processes

```bash
ps aux
ps aux | grep nginx
```

## Real time monitoring

```bash
top
sudo apt install htop -y
htop
```

## Background and foreground jobs

```bash
sleep 100 &
jobs
fg %1
bg %1
```

## Kill processes

```bash
kill <PID>
killall sleep
```

## Exercise completed

Start a long running process in the background, find its PID, and kill it.

### Commands used

```bash
sleep 300 &
jobs
ps aux | grep sleep
kill 12345
```

### Explanation

- `sleep 300 &` starts a process in the background
- `jobs` shows the active background job
- `ps aux | grep sleep` finds the process and its PID
- `kill 12345` stops the process using its PID

Replace `12345` with the real PID from your terminal.
