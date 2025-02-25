# Proxmox Web Interface Guide

This guide provides a detailed walkthrough of the Proxmox web interface, including how to access it, navigate its features, and create virtual machines (VMs) and containers.

---

## Accessing the Proxmox Web Interface
1. Open a web browser (e.g., Chrome, Firefox).
2. Enter the IP address of your Proxmox server followed by `:8006` (e.g., `https://192.168.1.100:8006`).
3. Log in with your username (usually `root`) and password.

---

## Interface Overview
The Proxmox interface is divided into sections:

### Left Side: Tree Menu
- **Datacenter**: The top-level view. If you have multiple Proxmox servers (nodes), they’ll appear here.
- **Nodes (Servers)**: Under the Datacenter, you’ll see your individual servers. Click on a server to manage it.
- **Storage**: Shows all storage devices (hard drives, SSDs, etc.) connected to your server.
- **VMs and Containers**: Once you create virtual machines or containers, they’ll appear here.

### Top Tabs
- **Summary**: Overview of your server’s resources (CPU, RAM, storage).
- **Notes**: Add notes about your server (useful for teams).
- **Shell**: Open a terminal to run commands directly on the server.
- **Networking**: Configure network settings (e.g., bridges, IP addresses).
- **Certificates**: Manage SSL certificates for secure connections.
- **DNS**: Set up DNS settings for your server.
- **Time**: Check and set the correct time zone.
- **Syslog**: View system logs for troubleshooting.

---

## Detailed Walkthrough of Key Features

### Server Summary
1. Click on your server in the left tree menu (e.g., `pve1`).
2. Go to the **Summary** tab.
   - **CPU Usage**: Shows how much of your CPU is being used.
   - **Memory Usage**: Shows how much RAM is being used.
   - **Storage Usage**: Shows how much disk space is used.
   - **System Information**: Displays your server’s hardware (e.g., CPU model, kernel version).
   - **Repository Status**: Shows whether the enterprise repository is enabled (requires a subscription).

### Updates
1. Click on your server in the left tree menu.
2. Go to the **Updates** tab.
   - Click **Refresh** to check for updates.
   - If updates are available, click **Upgrade** to install them.
   - If you don’t have a subscription, you’ll see an error for the enterprise repository. You can ignore this or switch to the **no-subscription repository**.

### Storage
1. Click on your server in the left tree menu.
2. Go to the **Storage** tab.
   - You’ll see a list of storage devices (e.g., local, LVM-Thin, ZFS).
   - **LVM-Thin**: This is where virtual machine disks are stored. Even if your main storage looks full, LVM-Thin might still have space for VMs.
   - You can add new storage devices (e.g., hard drives, SSDs) here.

### Virtual Machines (VMs) and Containers
1. Click on your server in the left tree menu.
2. Click the **Create VM** or **Create CT** button at the top right.
   - **VM**: A full virtual machine with its own operating system (e.g., Windows, Linux).
   - **Container**: A lightweight virtual environment that shares the host’s operating system.
3. Follow the wizard to set up your VM or container:
   - **VM**: Choose the OS, allocate CPU/RAM, and create a virtual disk.
   - **Container**: Choose a template (e.g., Ubuntu, Debian) and configure resources.

### Networking
1. Click on your server in the left tree menu.
2. Go to the **Network** tab.
   - **Bridges**: Create network bridges to connect VMs/containers to your network.
   - **IP Addresses**: Assign static or dynamic IPs to your VMs/containers.
   - **DNS**: Configure DNS settings for your server.

### Firewall
1. Click on your server in the left tree menu.
2. Go to the **Firewall** tab.
   - Create rules to allow or block traffic to/from your server.
   - For example, you can block all traffic except SSH (port 22) for security.

---

## Creating Your First Virtual Machine (VM)
1. Click on your server in the left tree menu.
2. Click the **Create VM** button at the top right.
3. Follow the wizard:
   - **General**: Name your VM (e.g., `Ubuntu-Server`).
   - **OS**: Select the ISO file for the operating system (e.g., Ubuntu 22.04).
   - **System**: Choose the BIOS type (default is fine).
   - **Disks**: Allocate disk space (e.g., 20GB).
   - **CPU**: Allocate CPU cores (e.g., 2 cores).
   - **Memory**: Allocate RAM (e.g., 2048MB).
   - **Network**: Choose a network bridge (default is fine).
4. Click **Finish** to create the VM.
5. Start the VM by clicking **Start** in the VM’s summary page.
6. Connect to the VM’s console to install the operating system.

---

## Creating Your First Container
1. Click on your server in the left tree menu.
2. Click the **Create CT** button at the top right.
3. Follow the wizard:
   - **General**: Name your container (e.g., `Web-Server`).
   - **Template**: Choose a template (e.g., Ubuntu 22.04).
   - **Root Disk**: Allocate disk space (e.g., 10GB).
   - **CPU**: Allocate CPU cores (e.g., 1 core).
   - **Memory**: Allocate RAM (e.g., 1024MB).
   - **Network**: Choose a network bridge (default is fine).
4. Click **Finish** to create the container.
5. Start the container by clicking **Start** in the container’s summary page.
6. Connect to the container’s console to configure it.

---

## Clustering (Advanced Feature)
If you have multiple Proxmox servers, you can create a cluster:
1. Go to the **Datacenter** view.
2. Click **Cluster** > **Create Cluster**.
3. Follow the wizard to set up the cluster.
4. Once the cluster is created, you can manage all your servers from one interface.

---

## Tips for Using Proxmox
- **Backups**: Regularly back up your VMs and containers.
- **Updates**: Keep your Proxmox server updated for security and performance.
- **Resource Allocation**: Don’t overallocate resources (e.g., don’t assign more CPU/RAM than your server has).
- **Networking**: Use bridges to connect VMs/containers to your network.

---

## Next Steps
- **Create Your First VM**: Follow the steps above to set up a virtual machine.
- **Create Your First Container**: Follow the steps above to set up a container.
- **Explore**: Play around with the interface to get comfortable with it.

---

For more information, visit the [Proxmox Documentation](https://pve.proxmox.com/wiki/Main_Page).