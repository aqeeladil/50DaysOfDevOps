# Linux Kernel Guide

## 1. Kernel Parameters Adjustment
### Viewing and Modifying Kernel Parameters
Kernel parameters are stored in `/proc/sys/` and can be modified temporarily using `sysctl` or permanently in `/etc/sysctl.conf`.

### Example: Change Maximum Open Files per Process
```bash
# View current value
cat /proc/sys/fs/file-max

# Temporarily change the value
sysctl -w fs.file-max=100000

# Permanently modify the parameter
echo "fs.file-max = 100000" | sudo tee -a /etc/sysctl.conf
sysctl -p
```

---

## 2. Monitoring Kernel Logs
### Purpose of `/var/log/kern.log`
Contains kernel-related log messages, including hardware events and driver issues.

### Using `dmesg` to View Kernel Messages
```bash
# Display all kernel messages
dmesg

# Filter messages for a specific device
dmesg | grep eth0

# View only recent messages
dmesg | tail -50
```

---

## 3. Resource Monitoring with `top` and `htop`
### `top` vs `htop`
| Feature  | `top` | `htop` |
|----------|-------|--------|
| UI | Text-based | Interactive, color-coded |
| Sorting | Manual commands | Supports mouse scrolling |
| Process control | Limited | Can directly kill processes |

### Identify High CPU/Memory Usage
```bash
# Run top
top  
# Press 'Shift + P' for CPU, 'Shift + M' for memory

# Run htop
htop
# Use arrow keys or mouse to navigate
```

---

## 4. Analyzing System Performance
### Monitoring Tools
```bash
# Memory, CPU, I/O usage
vmstat 2 5

# Disk I/O usage
iostat -dx 2

# CPU usage per core
mpstat -P ALL 2
```

---

## 5. Kernel Tuning for Performance
### Swappiness Parameter
```bash
# Check current value
cat /proc/sys/vm/swappiness

# Change value temporarily
sysctl -w vm.swappiness=10

# Permanent change
echo "vm.swappiness = 10" | sudo tee -a /etc/sysctl.conf
sysctl -p
```

---

## 6. Using `sysctl` for Runtime Configuration
### Disable IP Forwarding
```bash
# Check current status
sysctl net.ipv4.ip_forward

# Disable it temporarily
sysctl -w net.ipv4.ip_forward=0

# Make it permanent
echo "net.ipv4.ip_forward = 0" | sudo tee -a /etc/sysctl.conf
sysctl -p
```

---

## 7. Kernel Oops and Panic Analysis
### Definitions
- **Kernel Oops**: A non-fatal error that allows system continuation.
- **Kernel Panic**: A critical error that crashes the system.

### Troubleshooting
```bash
# Check logs
journalctl -k -b -1
cat /var/log/kern.log | grep -i "panic"

# Enable crash dumps
sudo apt install kdump-tools

# Debug with gdb
gdb vmlinux /var/crash/core
```

---

## 8. Kernel Module Management
### Commands
```bash
# List loaded modules
lsmod

# Load a module
modprobe <module_name>

# Unload a module
modprobe -r <module_name>

# Prevent loading at boot
echo "blacklist <module_name>" | sudo tee -a /etc/modprobe.d/blacklist.conf
```

---

## 9. Using `perf` for Performance Analysis
### Example: Analyzing CPU Usage
```bash
# Install perf
sudo apt install linux-tools-common linux-tools-$(uname -r)

# Record CPU events
perf record -g -a -F 99 -- sleep 10

# View report
perf report
```

---

## 10. Kernel Upgrades and Patching
### Considerations
- Ensure **backup** and **recovery plan**.
- Use **LTS kernels** in production.

### Upgrade Process
```bash
# Check current kernel version
uname -r

# List available kernels
apt-cache search linux-image

# Install new kernel
sudo apt install linux-image-<version>

# Reboot system
sudo reboot

# Verify the new kernel is running
uname -r
```

---
