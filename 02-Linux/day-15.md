# Advanced Linux Commands

## 1. Analyze Resource Usage (CPU & Memory)
To find processes consuming the most CPU or memory:
```bash
top
```
or a more user-friendly version:
```bash
htop
```
To sort by memory usage:
```bash
ps aux --sort=-%mem | head -10
```
To sort by CPU usage:
```bash
ps aux --sort=-%cpu | head -10
```

## 2. Monitor System Performance & Set Up Data Logging
To monitor CPU and memory usage over time:
```bash
vmstat 1 10
```
To log performance data:
```bash
sar -u 5 10 >> cpu_usage.log
```
For detailed monitoring over time, install and use:
```bash
nmon
```
or set up `sysstat` and use:
```bash
iostat -x 5 >> disk_usage.log
```

## 3. Check Network Connections & Listening Services
To list open network connections:
```bash
netstat -tulnp
```
or using `ss` (faster alternative):
```bash
ss -tulnp
```
To see only listening services:
```bash
lsof -i -P -n | grep LISTEN
```

## 4. Visualize Real-time Network Bandwidth Usage
To monitor real-time bandwidth usage:
```bash
nload
```
or per process usage:
```bash
iftop -i eth0
```
For network traffic by process:
```bash
nethogs
```

## 5. Monitor Network Traffic Trends Over Time
To capture network traffic:
```bash
tcpdump -i eth0
```
To analyze bandwidth usage over time:
```bash
vnstat -i eth0
```

## 6. Change Ownership of a Directory and Its Contents
To change the ownership:
```bash
chown -R newuser:newgroup /path/to/directory
```

## 7. Modify Script File Permissions (Owner Execute Only)
To allow only the owner to execute:
```bash
chmod 700 script.sh
```

## 8. Create an Isolated Environment (chroot)
To change the root directory:
```bash
mkdir -p /newroot/{bin,lib,lib64}
cp /bin/bash /newroot/bin/
chroot /newroot /bin/bash
```
For full environments, consider:
```bash
systemd-nspawn -D /newroot
```

## 9. Schedule a Task to Run Daily & Log Output
To run a script daily:
```bash
crontab -e
```
Add:
```
0 2 * * * /path/to/script.sh >> /var/log/script.log 2>&1
```
For `systemd` timers:
```bash
systemctl enable myscript.timer
```

## 10. Run a Long Task in Background & Logout Safely
Using `nohup`:
```bash
nohup long-running-command & disown
```
Using `screen`:
```bash
screen -S mysession
```
Run command, then press `Ctrl + A, D` to detach.

## 11. Pass Command Output to Another Command
Using pipes (`|`):
```bash
ls -l | grep ".txt"
```
Using `xargs`:
```bash
find . -name "*.log" | xargs rm
```

## 12. Test Connectivity to a Remote Host & Measure Latency
Using `ping`:
```bash
ping -c 5 example.com
```
For detailed output:
```bash
mtr example.com
```

## 13. Query DNS Records for a Domain
Using `nslookup`:
```bash
nslookup example.com
```
Using `dig`:
```bash
dig example.com
```

## 14. Retrieve Detailed DNS Information
To get all DNS records:
```bash
dig example.com ANY
```
For detailed troubleshooting:
```bash
whois example.com
```

## 15. Check & Repair Filesystem Corruption
To check a disk:
```bash
fsck -n /dev/sdX
```
To repair:
```bash
fsck -y /dev/sdX
```
If it's the root filesystem:
```bash
touch /forcefsck
reboot
