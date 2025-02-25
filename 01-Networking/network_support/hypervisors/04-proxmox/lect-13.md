# Proxmox VM & Container Management (CLI)

## **1. Connect to Your Proxmox Server**
Before running commands, log in to your Proxmox server via SSH.

### **1.1 Open SSH Connection**
#### **Linux/macOS:**
```bash
ssh root@<your-proxmox-ip>
```
Example:
```bash
ssh root@192.168.1.100
```

#### **Windows (PowerShell or PuTTY):**
```powershell
ssh root@192.168.1.100
```

---

## **2. List Virtual Machines (VMs)**
```bash
qm list
```
### **Example Output:**
```plaintext
 VMID NAME            STATUS     MEM(MB) BOOTDISK(GB) PID
 100  Ubuntu-Server   stopped    2048     20.00        -
 101  Windows10       running    4096     50.00        2593
 102  Debian          running    1024     10.00        3125
```

---

## **3. Start, Stop, Restart a VM**
### **3.1 Start a VM**
```bash
qm start 100
```

### **3.2 Stop a VM**
Graceful shutdown:
```bash
qm shutdown 101
```
Force stop:
```bash
qm stop 101
```

### **3.3 Restart a VM**
```bash
qm reboot 102
```

### **3.4 Force Reset a VM (if frozen)**
```bash
qm reset 102
```

---

## **4. View & Modify VM Settings**
### **4.1 View VM Configuration**
```bash
qm config 100
```

### **4.2 Change RAM Allocation**
```bash
qm set 100 --memory 4096
```

### **4.3 Enable Auto-Start**
```bash
qm set 100 --onboot 1
```
Disable Auto-Start:
```bash
qm set 100 --onboot 0
```

---

## **5. List and Manage Containers**
### **5.1 List All Containers**
```bash
pct list
```

### **5.2 Start, Stop, Restart a Container**
```bash
pct start 105  # Start Container 105
pct shutdown 104  # Gracefully stop Container 104
pct stop 104  # Force stop Container 104
pct reboot 104  # Restart Container 104
```

### **5.3 Enter a Running Container**
```bash
pct enter 104
```
Exit the container:
```bash
Ctrl + D
```

### **5.4 View & Modify Container Configuration**
```bash
pct config 104
```
Change RAM:
```bash
pct set 104 -memory 1024
```
Enable Auto-Start:
```bash
pct set 104 -onboot 1
```

---

## **6. Summary of Key Commands**

| **Action** | **VM Command** | **Container Command** |
|------------|---------------|------------------|
| List all | `qm list` | `pct list` |
| Start | `qm start <VMID>` | `pct start <ContainerID>` |
| Stop (Graceful) | `qm shutdown <VMID>` | `pct shutdown <ContainerID>` |
| Stop (Force) | `qm stop <VMID>` | `pct stop <ContainerID>` |
| Restart | `qm reboot <VMID>` | `pct reboot <ContainerID>` |
| View Config | `qm config <VMID>` | `pct config <ContainerID>` |
| Change RAM | `qm set <VMID> --memory <MB>` | `pct set <ContainerID> -memory <MB>` |
| Auto-Start | `qm set <VMID> --onboot 1` | `pct set <ContainerID> -onboot 1` |
| Enter Shell | N/A | `pct enter <ContainerID>` |

---

## **7. Conclusion**
This guide provides a CLI-based approach to managing Proxmox VMs and Containers efficiently. Use these commands for automation, scripting, and remote management.


