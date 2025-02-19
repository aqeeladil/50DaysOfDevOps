# Advanced Linux Commands

## 16. Creating a Filesystem on a Disk Partition
To create a new filesystem on a disk partition:
1. Identify the target partition using `lsblk` or `fdisk -l`.
2. Unmount the partition if it's mounted:  
   ```bash
   umount /dev/sdX
   ```
3. Format the partition with a suitable filesystem (e.g., ext4):  
   ```bash
   mkfs.ext4 /dev/sdX
   ```
4. Create a mount point:  
   ```bash
   mkdir /mnt/newdisk
   ```
5. Mount the partition:  
   ```bash
   mount /dev/sdX /mnt/newdisk
   ```
6. Persist the mount across reboots by adding an entry to `/etc/fstab`:
   ```bash
   echo "/dev/sdX /mnt/newdisk ext4 defaults 0 2" >> /etc/fstab
   ```

---

## 17. Identifying Running Processes
To list processes and their resource usage:
- Use `ps`:
  ```bash
  ps aux
  ```
- Use `top` or `htop` for real-time monitoring:
  ```bash
  top
  ```
- Get resource-intensive processes:
  ```bash
  ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head
  ```
- Get details for a specific process:
  ```bash
  ps -p <PID> -o pid,ppid,cmd,%mem,%cpu
  ```

---

## 18. Checking Free and Used Memory
Use:
- `free -h` (human-readable memory usage)
- `vmstat -s` (detailed memory statistics)
- `top` or `htop` to see memory usage per process.

Implications:
- High memory usage with frequent swapping (`si/so` in `vmstat`) can degrade performance.
- Consider tuning cache settings or adding more RAM if memory pressure is high.

---

## 19. Accessing a Command’s Manual
Use:
```bash
man <command>
```
For quick help:
```bash
<command> --help
```
For alternative documentation:
```bash
info <command>
```

---

## 20. Investigating Unexpected Process Behavior
To list processes:
```bash
ps aux | grep <process_name>
```
To get detailed info:
```bash
top -p <PID>
strace -p <PID> # Trace system calls
lsof -p <PID>   # Check open files
```
For logs:
```bash
journalctl -u <service_name>
```

---

## 21. Gracefully Terminating a Process
1. **Find the process:**
   ```bash
   ps aux | grep <process_name>
   ```
2. **Send a SIGTERM signal (graceful shutdown):**
   ```bash
   kill <PID>
   ```
3. **If unresponsive, send SIGKILL (force terminate):**
   ```bash
   kill -9 <PID>
   ```
4. **For services, use systemctl:**
   ```bash
   systemctl stop <service>
   ```

---

## 22. Modifying Kernel Parameters at Runtime
To temporarily modify a kernel parameter:
```bash
sysctl -w <parameter>=<value>
```
Example:
```bash
sysctl -w vm.swappiness=10
```
To make it permanent, edit `/etc/sysctl.conf`:
```bash
echo "vm.swappiness=10" >> /etc/sysctl.conf
sysctl -p
```

---

## 23. Managing System Services
- **Start a service:**  
  ```bash
  systemctl start <service>
  ```
- **Stop a service:**  
  ```bash
  systemctl stop <service>
  ```
- **Restart a service:**  
  ```bash
  systemctl restart <service>
  ```
- **Check status:**  
  ```bash
  systemctl status <service>
  ```
- **Enable on boot:**  
  ```bash
  systemctl enable <service>
  ```

---

## 24. Secure File Transfer
To transfer files securely:
```bash
scp file.txt user@remote:/path/
```
For directories:
```bash
scp -r directory user@remote:/path/
```
For increased security, use `rsync` with SSH:
```bash
rsync -avz -e ssh /local/path user@remote:/remote/path
```

---

## 25. Copying Files While Preserving Attributes
Use `scp` with `-p`:
```bash
scp -p file.txt user@remote:/path/
```
Use `rsync` to preserve permissions:
```bash
rsync -avz /source/path user@remote:/destination/path
```
Use `cp` for local copies:
```bash
cp -a source/ destination/
```

---

## 26. Editing Configuration Files in Place
To edit and replace text in a file:
```bash
sed -i 's/old_value/new_value/g' config_file
```
For multiple occurrences:
```bash
grep -rl 'old_value' /etc/configs/ | xargs sed -i 's/old_value/new_value/g'
```

---

## 27. Extracting Patterns from a Large Text File
- Using `grep`:
  ```bash
  grep 'pattern' largefile.txt
  ```
- Using `awk`:
  ```bash
  awk '{print $2, $5}' largefile.txt
  ```
- Using `cut`:
  ```bash
  cut -d ' ' -f 2,5 largefile.txt
  ```

---

## 28. Finding a Process's Associated Terminal
To determine the terminal:
```bash
ps -o pid,tty,cmd -p <PID>
```
To see which users are using which terminals:
```bash
who
```
If the process is running in a detached terminal (e.g., background jobs), use:
```bash
tty
```
Or check `/proc/<PID>/fd` for terminal devices.
