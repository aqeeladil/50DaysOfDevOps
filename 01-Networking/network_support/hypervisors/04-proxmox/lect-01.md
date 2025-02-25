# Proxmox Virtual Environment (VE) Setup and Usage Guide

This guide provides step-by-step instructions for setting up and using Proxmox VE, a powerful open-source virtualization platform. It covers installation, configuration, creating virtual machines (VMs) and containers, backups, clustering, and high availability.

---

## **What You Need**
- A physical server or desktop (not a VM).
- A 64-bit CPU with virtualization support (Intel VT-x/AMD-V).
- At least 4GB of RAM (8GB or more recommended).
- A fast storage drive (SSD preferred).
- A network connection.

---

## **Step 1: Setting Up Proxmox**

### **1. Download Proxmox VE ISO**
- Visit the official Proxmox website: [https://www.proxmox.com](https://www.proxmox.com).
- Download the latest Proxmox VE ISO file.

### **2. Create a Bootable USB**
- Use a tool like **Rufus** (Windows) or **Etcher** (Linux/Mac) to create a bootable USB drive with the Proxmox ISO.

### **3. Boot from the USB**
- Insert the USB into your server or desktop.
- Boot into the BIOS/UEFI and set the USB as the primary boot device.
- Save changes and reboot.

### **4. Install Proxmox**
- Select "Install Proxmox VE" from the boot menu.
- Accept the EULA.
- Choose the target disk for installation (preferably an SSD).
- Set your country, time zone, and keyboard layout.
- Set a strong password for the root account.
- Configure the network:
  - Enter a hostname (e.g., `pve1`).
  - Set an IP address, gateway, and DNS (e.g., `192.168.1.100` for the IP, `192.168.1.1` for the gateway, and `8.8.8.8` for DNS).
- Confirm the installation and wait for it to complete.

### **5. Access the Proxmox Web Interface**
- Once installed, reboot the server.
- Open a web browser on another computer and go to `https://<IP>:8006` (e.g., `https://192.168.1.100:8006`).
- Log in with the username `root` and the password you set during installation.

---

## **Step 2: Exploring the Proxmox Web Interface**

### **Dashboard Overview**
- The dashboard shows an overview of your Proxmox server, including CPU, memory, and storage usage.
- On the left sidebar, you’ll see your server node (e.g., `pve1`).

### **Storage Configuration**
- Go to **Datacenter > Storage**.
- Add storage by clicking **Add** and selecting a type (e.g., **Directory** for local storage or **NFS** for shared storage).
- For example, to add local storage:
  - Select **Directory**.
  - Set an ID (e.g., `local`).
  - Choose the directory path (e.g., `/var/lib/vz`).

### **Network Configuration**
- Go to **Datacenter > Network**.
- You can add additional network interfaces or bridges here.
- For example, to create a new bridge for VMs:
  - Click **Create > Linux Bridge**.
  - Set a name (e.g., `vmbr1`).
  - Assign an IP address and subnet (e.g., `192.168.2.1/24`).

---

## **Step 3: Creating a Virtual Machine**

### **1. Download an ISO**
- Go to **Datacenter > Storage > local > Content**.
- Click **Upload** and select an ISO file (e.g., Ubuntu Server ISO).

### **2. Create the VM**
- Click **Create VM** in the top-right corner.
- Set a VM ID and name (e.g., `100` and `Ubuntu-Server`).
- Choose the ISO file you uploaded.
- Set the OS type (e.g., Linux).
- Allocate resources:
  - 2 CPU cores.
  - 4GB RAM.
  - 20GB disk space.
- Configure the network to use the bridge you created (e.g., `vmbr0`).
- Finish the setup and start the VM.

### **3. Install the OS**
- Open the VM’s console.
- Follow the OS installation steps (e.g., partitioning, user setup).

---

## **Step 4: Creating a Container**

### **1. Download a Container Template**
- Go to **Datacenter > Storage > local > Content**.
- Click **Templates** and download a template (e.g., Ubuntu 22.04).

### **2. Create the Container**
- Click **Create CT**.
- Set a container ID and hostname (e.g., `101` and `ubuntu-container`).
- Choose the template you downloaded.
- Allocate resources:
  - 1 CPU core.
  - 1GB RAM.
  - 10GB disk space.
- Configure the network to use the bridge (e.g., `vmbr0`).
- Finish the setup and start the container.

### **3. Access the Container**
- Open the container’s console.
- Log in with the root credentials you set during creation.

---

## **Step 5: Backups and Snapshots**

### **Backups**
- Go to **Datacenter > Backup**.
- Click **Add** to create a backup job.
- Select the VMs or containers to back up.
- Choose a storage location (e.g., `local`).
- Set a schedule (e.g., daily at 2 AM).

### **Snapshots**
- Select a VM or container.
- Go to **Snapshots**.
- Click **Take Snapshot**.
- Name the snapshot (e.g., `Before-Upgrade`).
- Snapshots allow you to revert to a previous state if something goes wrong.

---

## **Step 6: Clustering (Advanced)**

### **1. Set Up Additional Nodes**
- Repeat the installation steps on two more servers (e.g., `pve2` and `pve3`).

### **2. Create the Cluster**
- On `pve1`, go to **Datacenter > Cluster**.
- Click **Create Cluster** and name it (e.g., `my-cluster`).
- Copy the join information.

### **3. Join the Cluster**
- On `pve2` and `pve3`, go to **Datacenter > Cluster**.
- Click **Join Cluster** and paste the join information from `pve1`.

### **4. Verify the Cluster**
- Go to **Datacenter > Cluster** on any node.
- You should see all three nodes listed.

---

## **Step 7: High Availability (HA)**

### **1. Enable HA**
- Go to **Datacenter > HA**.
- Add a VM or container to the HA group.
- Set the priority for each node.

### **2. Test HA**
- Shut down one node (e.g., `pve1`).
- The VM or container should automatically migrate to another node (e.g., `pve2`).

---

## **Conclusion**

By following this guide, you’ll have a fully functional Proxmox server capable of running VMs, containers, and even a clustered setup with high availability. For further assistance, refer to the [Proxmox Documentation](https://pve.proxmox.com/wiki/Main_Page) or community forums.

---
