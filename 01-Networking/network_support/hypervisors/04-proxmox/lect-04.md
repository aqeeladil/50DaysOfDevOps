# **Proxmox: Virtual Machines (VMs) vs. Containers (LXC)**

## **📌 What is Proxmox?**
[Proxmox Virtual Environment (Proxmox VE)](https://www.proxmox.com/) is an **open-source** virtualization platform that allows you to run and manage:
1. **Virtual Machines (VMs)** using **KVM (Kernel-based Virtual Machine)**
2. **LXC Containers** for lightweight OS-level virtualization

---

## **📌 Virtual Machines (VMs) vs. Containers (LXC) in Proxmox**
| Feature            | **Virtual Machines (VMs)** | **LXC Containers** |
|--------------------|--------------------------|---------------------|
| **Virtualization Type** | Full Virtualization (Hardware Emulation) | OS-Level Virtualization (Lightweight) |
| **Resource Usage** | High (Requires full OS) | Low (Shares host OS kernel) |
| **Performance** | Slightly lower due to overhead | Higher (Near-native performance) |
| **Isolation** | Strong isolation (each VM runs its own OS) | Weaker isolation (shares host kernel) |
| **Live Migration** | ✅ Supported | ❌ Not supported |
| **Ideal for** | Running multiple OS environments | Running lightweight Linux-based workloads |
| **Boot Time** | Slow (needs OS boot) | Fast (instant start) |

---

## **📌 Hands-on Demonstration in Proxmox**

### **1️⃣ Install and Access Proxmox VE**
Before creating a VM or container, ensure you have **Proxmox installed** and accessible via the **Proxmox Web UI**.

- Open a browser and go to:
  ```
  https://<your_proxmox_server_IP>:8006
  ```
- Login with your **root** username and password.

---

## **📌 2️⃣ Creating a Virtual Machine (VM) in Proxmox**
A VM runs **a full OS** (e.g., Ubuntu, Windows) and provides full isolation.

### **Step-by-Step Guide to Create a VM**
1. **Open Proxmox Web UI**
   - Navigate to **Datacenter → Select Node** (e.g., `pve1`).  
   - Click **Create VM**.

2. **Configure the VM**
   - **General Tab:** Give the VM a **name** (e.g., `Ubuntu-Server`).
   - **OS Tab:** Select the **ISO Image** and choose **Guest OS Type** (Linux or Windows).
   - **Hard Disk Tab:** Choose storage (e.g., `local-lvm`), set disk size (e.g., **20GB**).
   - **CPU Tab:** Assign **CPU Cores** (e.g., **2 cores**).
   - **Memory Tab:** Assign **RAM** (e.g., **4GB**).
   - **Network Tab:** Select **Bridge Mode (`vmbr0`)**.

3. **Finish and Start VM**
   - Click **Finish**.
   - Go to **VM List** and **Start the VM**.
   - Open **Console** and install the OS.

🎉 **Done!** You now have a functional virtual machine in Proxmox.

---

## **📌 3️⃣ Creating an LXC Container in Proxmox**
LXC containers are **lightweight** and share the host’s kernel.

### **Step-by-Step Guide to Create an LXC Container**
1. **Download an LXC Template**
   - Go to **Datacenter → Storage → CT Templates**.
   - Click **Templates** and **Download** an OS template (e.g., `ubuntu-22.04-standard`).

2. **Create an LXC Container**
   - Click **Create CT**.
   - **General Tab:** Assign a **Container ID** and set a **Hostname**.
   - **Template Tab:** Choose the **LXC Template**.
   - **Root Disk Tab:** Set disk size (e.g., **10GB**).
   - **CPU & Memory:** Assign **1 CPU Core** and **512MB RAM**.
   - **Network Tab:** Choose **Bridge (`vmbr0`)**.

3. **Finish and Start Container**
   - Click **Finish** and start the container.
   - Open **Console** and log in using **root**.

🎉 **Done!** Your LXC container is running with **minimal resource usage**.

---

## **📌 4️⃣ Key Takeaways**
- **Use VMs** when you need **full isolation** and want to run **Windows or different Linux distributions**.
- **Use Containers** when you need **lightweight, fast, and efficient Linux-based applications**.
- **Proxmox supports both VMs and LXC Containers**, making it a powerful tool for virtualization.

---

