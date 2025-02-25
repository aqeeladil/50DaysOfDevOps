# Creating a Virtual Machine Template in Proxmox

## Overview
This guide provides step-by-step instructions to create a **VM template** in **Proxmox**, allowing for quick deployment of multiple VMs with minimal setup.

## Prerequisites
- **Proxmox VE installed** (latest version recommended)
- **ISO image of a Linux OS** (Ubuntu, Debian, or CentOS)
- **Basic knowledge of Proxmox & Linux commands**

---

## Step 1: Create a Base Virtual Machine (VM)

### 1️⃣ Create a New VM in Proxmox
1. **Login to Proxmox Web UI** (`https://your-proxmox-ip:8006`)
2. Click on **Create VM** (top-right corner).
3. Fill in the details:
   - **Node**: Select your Proxmox server  
   - **VM ID**: Auto-generated (or set manually)  
   - **Name**: Choose something meaningful (e.g., `ubuntu-template`)  
   - Click **Next**
4. **Select OS**  
   - Choose **Linux** and select the **ISO image**  
   - Click **Next**  
5. **System Settings**  
   - Default settings work fine; click **Next**  
6. **Disk Setup**  
   - **Storage**: Select `local-lvm`  
   - **Disk Size**: Set `20GB`  
   - Click **Next**  
7. **CPU & Memory**  
   - **CPU Cores**: `2` (minimum)  
   - **RAM**: `2048MB` (minimum)  
   - Click **Next**  
8. **Network Configuration**  
   - Select `vmbr0` (bridge mode)  
   - Click **Next**  
9. **Confirm and Finish**  
   - Click **Finish**  

---

## Step 2: Install and Configure the VM

1. **Start the VM** → Click on **Console**  
2. Follow the installation wizard **(Ubuntu/Debian example)**:
   - Choose language, time zone, and disk partitioning.
   - Create a **user account** (`username: admin` / `password: strongpassword`).
   - Select **OpenSSH Server** (important for remote access).
   - Finish the installation and reboot the VM.
3. **Update and Clean the VM**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   sudo apt autoremove -y
   ```

---

## Step 3: Prepare the VM for Templating

### 1️⃣ Remove SSH Host Keys
```bash
sudo rm -f /etc/ssh/ssh_host_*
```

### 2️⃣ Reset Machine ID
```bash
sudo truncate -s 0 /etc/machine-id
sudo rm -f /var/lib/dbus/machine-id
ln -s /etc/machine-id /var/lib/dbus/machine-id
```

### 3️⃣ Install Cloud-Init
```bash
sudo apt install cloud-init -y
```

### 4️⃣ Clean the System
```bash
sudo apt clean
sudo journalctl --vacuum-time=1s
```

Shutdown the VM before converting it to a template:
```bash
sudo poweroff
```

---

## Step 4: Convert VM to Template

1. In **Proxmox Web UI**, go to **Datacenter → Node → VM (`ubuntu-template`)**  
2. Right-click on the VM → Select **Convert to Template**  
3. Confirm the action → The VM is now a **template** 🎉  

---

## Step 5: Configure Cloud-Init in Proxmox

1. Select the **Template VM (`ubuntu-template`)**  
2. Go to **Hardware → Add → Cloud-Init Drive**  
3. Choose **Storage** (`local-lvm`) → Click **Add**  
4. Go to **Cloud-Init** tab → Set:
   - **User**: `admin`
   - **Password**: `your-secure-password`
   - **SSH Key** (optional)
5. Click **Regenerate Image**

---

## Step 6: Clone the Template to Create New VMs

### Create a New VM from Template
1. Right-click on **`ubuntu-template`** → Select **Clone**  
2. Set:
   - **Name**: `web-server-1`  
   - **Clone Mode**: `Full Clone`  
   - **Target Storage**: `local-lvm`  
   - Click **Clone**  

💡 **Repeat this step to create more VMs (`web-server-2`, etc.)**  

---

## Step 7: Start and Verify New VMs

1. **Start the cloned VM (`web-server-1`)**  
2. Open the console and log in  
3. Verify **Cloud-Init applied changes**:  
   ```bash
   hostnamectl
   ```
   → Should show `web-server-1`

4. Check **network settings**:  
   ```bash
   ip a
   ```
   → Should have a unique IP  

5. Check **machine ID**:  
   ```bash
   cat /etc/machine-id
   ```

6. **Access via SSH** (if configured):  
   ```bash
   ssh admin@<vm-ip>
   ```

---

## 🎯 Final Result
✅ Successfully created a **VM Template**  
✅ Cloned multiple **VMs quickly**  
✅ Cloud-Init automated configurations  
✅ Each VM has **unique SSH keys, machine ID, and hostname**  

---

## 🚀 Benefits of Using VM Templates
✔ **Saves Time** – Deploy VMs in seconds  
✔ **Ensures Consistency** – Every VM has the same base setup  
✔ **Reduces Manual Effort** – Automates tedious tasks  
✔ **Scalable** – Perfect for DevOps & cloud environments  

---
