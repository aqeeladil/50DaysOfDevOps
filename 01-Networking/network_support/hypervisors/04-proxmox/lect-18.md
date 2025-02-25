# Proxmox Backup Server (PBS) Setup and Usage Guide

This guide provides step-by-step instructions for setting up and using **Proxmox Backup Server (PBS)**. It covers installation, configuration, integration with Proxmox VE, and using the backup client for file-level backups.

---

## **Table of Contents**
1. [Installing Proxmox Backup Server](#1-installing-proxmox-backup-server)
2. [Configuring Proxmox Backup Server](#2-configuring-proxmox-backup-server)
3. [Integrating PBS with Proxmox VE](#3-integrating-pbs-with-proxmox-ve)
4. [Using the Proxmox Backup Client](#4-using-the-proxmox-backup-client)
5. [Advanced Features](#5-advanced-features)

---

## **1. Installing Proxmox Backup Server**

### **Step 1: Download the PBS ISO**
- Visit the [Proxmox Backup Server download page](https://www.proxmox.com/en/downloads) and download the latest ISO image.

### **Step 2: Create a Bootable USB Drive**
- Use a tool like **Rufus** (Windows) or **Etcher** (cross-platform) to write the ISO to a USB drive.

### **Step 3: Boot from the USB Drive**
- Insert the USB drive into the server and boot from it.
- Select **Install Proxmox Backup Server** from the boot menu.

### **Step 4: Follow the Installation Wizard**
1. **License Agreement**: Accept the license terms.
2. **Target Disk**: Select the disk for installation (e.g., `/dev/sda`).
   - Choose the file system (e.g., `ext4`).
3. **Time Zone**: Set your country and time zone.
4. **Administration Password**: Set a strong password for the `root` user.
5. **Network Configuration**:
   - Set the hostname (e.g., `pbs.example.com`).
   - Configure the IP address, gateway, and DNS server.
6. **Installation Summary**: Review the settings and click **Install**.

### **Step 5: Access the PBS Web Interface**
- After installation, reboot the server.
- Access the PBS web interface using the IP address and port `8007` (e.g., `https://192.168.1.100:8007`).
- Log in with the `root` username and the password you set during installation.

---

## **2. Configuring Proxmox Backup Server**

### **Step 1: Set Up Storage**
1. Go to **Storage > Disks**.
2. Initialize any additional disks for backup storage (e.g., `/dev/sdb`).
3. Create a **directory** for backups:
   - Go to **Storage > Directory**.
   - Select the disk, choose the file system (e.g., `ext4`), and name the directory (e.g., `backup1`).

### **Step 2: Configure Network Settings**
- Go to **Configuration > Network**.
- Verify the IP address, gateway, and DNS settings.
- Add additional network interfaces if needed.

### **Step 3: Add Users and Permissions**
- Go to **Access Control > Users**.
- Add a new user (e.g., `admin`).
- Assign permissions to the user (e.g., `Administrator` role).

### **Step 4: Enable Two-Factor Authentication (Optional)**
- Go to **Access Control > TOTP**.
- Scan the QR code with an authenticator app (e.g., Google Authenticator).
- Enter the code to enable 2FA.

---

## **3. Integrating PBS with Proxmox VE**

### **Step 1: Add PBS to Proxmox VE**
1. In Proxmox VE, go to **Datacenter > Storage > Add > Proxmox Backup Server**.
2. Fill in the details:
   - **ID**: Name the storage (e.g., `pbs`).
   - **Server**: IP address of the PBS server.
   - **Username**: `root@pam`.
   - **Password**: Root password of PBS.
   - **Datastore**: Name of the datastore (e.g., `backup1`).
3. Click **Add**.

### **Step 2: Create a Backup**
1. Select a VM or container in Proxmox VE.
2. Click **Backup**.
3. Choose the PBS storage as the target.
4. Select the backup mode (e.g., `Stop` mode for consistency).
5. Click **Backup**.

### **Step 3: Restore a Backup**
1. Go to **Backups** in Proxmox VE.
2. Select the backup and click **Restore**.
3. Choose the target storage and VM ID.
4. Click **Restore**.

---

## **4. Using the Proxmox Backup Client**

### **Step 1: Install the Backup Client**
1. On a Debian/Ubuntu system, add the PBS repository:
   ```bash
   echo "deb http://download.proxmox.com/debian/pbs-client bullseye main" > /etc/apt/sources.list.d/pbs-client.list