# Proxmox VE: Getting Started Guide

This guide provides a step-by-step walkthrough for setting up **Proxmox VE** (Virtual Environment), a powerful open-source platform for virtualization and container management. Whether you're a beginner or an experienced user, this guide will help you install, configure, and manage Proxmox on your server.

---

## What is Proxmox?
Proxmox VE is a robust platform that combines two virtualization technologies:
- **KVM** for virtual machines (VMs).
- **LXC** for lightweight containers.

It’s ideal for home labs, small businesses, or large-scale deployments.

---

## Hardware Requirements
To run Proxmox VE, ensure your server meets the following minimum requirements:
- **CPU**: 64-bit processor with virtualization support (Intel VT-x/AMD-V).
- **RAM**: 4GB (8GB or more recommended).
- **Storage**: 20GB disk space (SSD recommended for better performance).
- **Network**: Ethernet connection.

---

## Installation Steps

### Step 1: Prepare Bootable Media
1. Download the Proxmox VE ISO from the [official website](https://www.proxmox.com/en/downloads).
2. Use a tool like **Rufus** (Windows) or **Balena Etcher** (cross-platform) to flash the ISO to a USB drive.
3. Insert the USB drive into your server and boot from it.

### Step 2: Install Proxmox VE
1. **Boot into the Installer**:
   - Select **Install Proxmox VE** from the boot menu.
2. **Accept the License Agreement**:
   - Click **I agree**.
3. **Select the Target Disk**:
   - Choose the disk for installation (use **ZFS RAID 1** for redundancy if you have multiple disks).
4. **Configure Location and Time Zone**:
   - Set your country, time zone, and keyboard layout.
5. **Set Up Root Password and Email**:
   - Enter a strong password for the `root` user and provide a valid email address.
6. **Configure Network Settings**:
   - Assign a static IP address, gateway, and DNS server.
7. **Review and Confirm**:
   - Double-check all settings and click **Install**.
8. **Reboot the Server**:
   - After installation, remove the USB drive and reboot.

---

## Accessing the Web Interface
1. Open a web browser and go to the Proxmox URL (e.g., `https://192.168.1.100:8006`).
2. Log in with:
   - Username: `root`
   - Password: The one you set during installation.
3. Explore the **Dashboard** to view your server’s resources (CPU, RAM, storage, etc.).

---

## Updating Proxmox
1. **Enable No-Subscription Repository**:
   - Go to **Datacenter** > **Updates** > **Repositories**.
   - Click **Add** and select the **No-Subscription** repository.
2. **Refresh and Install Updates**:
   - Go to **Updates** and click **Refresh**.
   - Click **Upgrade** to install available updates.
3. **Reboot the Server**:
   - Reboot the server from the web interface after updates.

---

## Creating a Virtual Machine (VM)
1. **Download an ISO**:
   - Go to **local (pve)** > **ISO Images**.
   - Click **Download from URL** and paste the link to an ISO (e.g., Debian or Ubuntu).
2. **Create a VM**:
   - Click **Create VM** in the top-right corner.
   - Configure the following:
     - **General**: VM ID, name.
     - **OS**: Select the downloaded ISO.
     - **System**: Leave defaults (BIOS or UEFI).
     - **Disks**: Set disk size (e.g., `32GB`).
     - **CPU**: Assign cores (e.g., `2`).
     - **Memory**: Set RAM (e.g., `2048MB`).
     - **Network**: Leave defaults (bridge mode).
   - Click **Finish**.
3. **Install the OS**:
   - Start the VM and click **Console** to access it.
   - Follow the OS installation steps (e.g., partitioning, user setup).

---

## Managing Your Proxmox Server
- **Backups**:
  - Schedule backups for your VMs under **Datacenter** > **Backup**.
- **Networking**:
  - Configure VLANs, bridges, or bonded networks under **Datacenter** > **Network**.
- **Storage**:
  - Add additional storage (e.g., NFS, Ceph) under **Datacenter** > **Storage**.

---

## Why Use Proxmox?
- **Cost-Effective**: Free and open-source.
- **Flexible**: Supports both VMs and containers.
- **Scalable**: Suitable for small to large deployments.
- **Community Support**: Active forums and extensive documentation.

---

## Next Steps
- Explore advanced features like **containers**, **clustering**, and **high availability**.
- Check out the [Proxmox documentation](https://pve.proxmox.com/wiki/Main_Page) for more details.

---

