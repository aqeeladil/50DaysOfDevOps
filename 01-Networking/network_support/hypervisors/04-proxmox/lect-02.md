# Proxmox VE Installation Guide

This guide provides step-by-step instructions for installing and setting up Proxmox Virtual Environment (VE) on a server or computer. Proxmox VE is an open-source platform for running virtual machines (VMs) and containers.

---

## 1. Download the Proxmox ISO
1. Visit the [Proxmox website](https://www.proxmox.com).
2. Navigate to the **Downloads** section and select **Proxmox Virtual Environment (VE)**.
3. Download the latest ISO file (e.g., Proxmox VE 8.x).

---

## 2. Create a Bootable USB Drive
1. Use a USB drive with at least **4GB** of space.
2. Download a USB imaging tool:
   - **Rufus** (Windows)
   - **Balena Etcher** (Windows/Mac/Linux)
   - **USB Imager** (cross-platform)
3. Write the Proxmox ISO to the USB drive:
   - Open the USB imaging tool.
   - Select the Proxmox ISO file.
   - Choose the USB drive as the target.
   - Click **Write** or **Flash** to create the bootable USB drive.

**Note**: This process will erase all data on the USB drive, so back up any important files first.

---

## 3. Boot the Server from the USB Drive
1. Insert the bootable USB drive into the server or computer.
2. Restart the server and access the boot menu (usually by pressing `F12`, `F11`, `Esc`, or `Del` during startup).
3. Select the USB drive as the boot device.

---

## 4. Install Proxmox
1. **Start the installer**:  
   Select **Install Proxmox VE** from the boot menu and press `Enter`.
2. **Accept the license agreement**:  
   Read and agree to the license terms.
3. **Select the installation disk**:  
   - Choose the hard drive where Proxmox will be installed.
   - Select the file system (default is `ext4`; `ZFS` is recommended for advanced users with sufficient RAM).
4. **Set the time zone**:  
   Select your region and time zone.
5. **Set a password**:  
   - Enter a strong password for the `root` user.
   - Add an email address (optional but useful for notifications).
6. **Configure networking**:  
   - Assign an IP address (e.g., `192.168.1.100`).
   - Set the gateway (e.g., `192.168.1.1`).
   - Set the DNS server (e.g., `8.8.8.8` for Google’s public DNS).
   - Choose a hostname (e.g., `pve1`).
7. **Review and confirm**:  
   Double-check all settings, then click **Install**.
8. **Wait for installation to complete**:  
   The installer will copy files and set up Proxmox. This may take a few minutes.

---

## 5. Access the Proxmox Web Interface
1. **Reboot the server**:  
   After installation, the server will reboot. Remove the USB drive.
2. **Find the IP address**:  
   The server will display its IP address on the screen (e.g., `https://192.168.1.100:8006`).
3. **Open a web browser**:  
   On another computer, enter the IP address with the port `:8006` (e.g., `https://192.168.1.100:8006`).
4. **Log in**:  
   - Username: `root`  
   - Password: The one you set during installation.
5. **Accept the SSL warning**:  
   Proxmox uses a self-signed certificate, so your browser may show a security warning. Proceed by accepting the risk.

---

## 6. Explore the Proxmox Web Interface
Once logged in, you can:
- **Create virtual machines (VMs)**:  
  Click **Create VM** to set up a new virtual machine.
- **Create containers**:  
  Use lightweight containers (like LXC) for running applications.
- **Manage storage**:  
  Add disks or network storage for VMs and backups.
- **Set up networking**:  
  Configure virtual networks, bridges, and firewalls.
- **Backup and restore**:  
  Schedule backups for your VMs and containers.

---

## 7. Example: Creating a Virtual Machine
1. **Click "Create VM"**:  
   In the top-right corner of the Proxmox interface, click **Create VM**.
2. **Set VM details**:  
   - Name: `MyFirstVM`  
   - OS Type: Linux (or Windows if you’re installing Windows).
3. **Assign resources**:  
   - CPU: 2 cores  
   - RAM: 2048 MB (2GB)  
   - Disk: 20GB (adjust based on your needs).
4. **Attach an ISO**:  
   Upload an ISO file (e.g., Ubuntu or Windows installer) to Proxmox and attach it to the VM.
5. **Start the VM**:  
   Click **Start** to boot the VM and install the operating system.

---

## Why Use Proxmox?
- **Run multiple operating systems**: Create VMs to run Linux, Windows, or other OSes on the same server.
- **Efficient resource usage**: Use one powerful server to host many VMs.
- **Flexibility**: Easily back up, clone, or move VMs between servers.

---

## Tips
- **Hardware requirements**: Proxmox works best on servers with sufficient RAM and fast storage.
- **Networking**: Ensure the IP address you assign doesn’t conflict with other devices on your network.
- **Backup**: Always back up your data before installing a new operating system.

---

For more information, visit the [Proxmox Documentation](https://pve.proxmox.com/wiki/Main_Page).
