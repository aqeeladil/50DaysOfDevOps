# Run Level and Systemd Commands

## SysVinit Commands:

### View the Current Run Level
```bash
runlevel
```
or  
```bash
who -r
```

### Switch to Single-User Mode
```bash
init 1
```
or  
```bash
telinit 1
```

---

## systemd Commands:

### List All Available systemd Targets
```bash
systemctl list-units --type=target --all
```
or  
```bash
systemctl list-targets
```

### Change the Default Target to `multi-user.target`
```bash
systemctl set-default multi-user.target
```

### Temporarily Switch to `graphical.target` from the Command Line
```bash
systemctl isolate graphical.target
```

### Check Active Services in `multi-user.target`
```bash
systemctl list-units --type=service --state=active
```
or  
```bash
systemctl list-units --type=service --state=running
```

### Halt the System from the Command Line
```bash
systemctl halt
```

### Reboot the System Using systemd
```bash
systemctl reboot
```

### Enable a Specific Target as the Default Boot Target
```bash
systemctl set-default <target>
```
Example:  
```bash
systemctl set-default multi-user.target
```

### Create a Custom Target in systemd
1. Navigate to the systemd configuration directory:
   ```bash
   cd /etc/systemd/system/
   ```
2. Create a new target file (e.g., `custom.target`):
   ```bash
   sudo nano custom.target
   ```
3. Add the following contents:
   ```ini
   [Unit]
   Description=My Custom Target
   Requires=multi-user.target
   AllowIsolate=yes
   ```
4. Save and exit the file.
5. Reload systemd:
   ```bash
   systemctl daemon-reload
   ```
6. Enable the new target (if needed):
   ```bash
   systemctl enable custom.target
   ```


