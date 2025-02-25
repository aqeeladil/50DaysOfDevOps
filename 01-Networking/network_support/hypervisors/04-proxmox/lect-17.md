# Proxmox Clustering and High Availability (HA)

## 📌 Overview
This guide explains how to set up **Proxmox Clustering** and enable **High Availability (HA)** to ensure VMs automatically restart on another node in case of failure.

---

## 🟢 What is Proxmox Clustering and HA?
- **Clustering**: Connecting multiple Proxmox servers (nodes) for centralized management.
- **High Availability (HA)**: Automatically migrates and restarts VMs if a node fails.

> **Example Scenario:**
> Suppose you have 3 Proxmox servers, and one crashes. HA will **automatically** move its VMs to another working node **without requiring manual intervention**.

---

## 🛠️ Prerequisites
### **1️⃣ Hardware Requirements**
✅ At least **3 Proxmox nodes**
✅ **Shared storage** (NFS, Ceph, or iSCSI)
✅ Dedicated **management network**

### **2️⃣ Software Requirements**
✅ Latest **Proxmox VE** installed
✅ Static **IP configuration**
✅ **SSH key authentication** enabled between nodes

---

## 📌 Step 1: Creating a Proxmox Cluster
### **1.1 Initialize the Cluster on the First Node**
1. Go to **Proxmox Web UI** → **Datacenter** → **Cluster** → **Create Cluster**.
2. Enter:
   - **Cluster Name**: `MyProxmoxCluster`
   - **Network Interface**: Choose the dedicated network interface.
3. Click **Create**.

### **1.2 Add Nodes to the Cluster**
1. On another Proxmox node, navigate to **Datacenter → Cluster**.
2. Click **Join Cluster**.
3. Copy the **Join Information** from the first node.
4. Paste it into the joining node’s UI.
5. Click **Join** and enter the root password when prompted.

#### ✅ Verify cluster status:
```bash
pvecm status
```

---

## 📌 Step 2: Setting Up Shared Storage
### **Why is Shared Storage Required?**
- VMs must use **shared storage** so that **all nodes** can access their disks.
- Without shared storage, HA **cannot migrate VMs** to another node.

### **2.1 Add Shared Storage**
1. Go to **Datacenter → Storage**.
2. Click **Add** and choose a shared storage type (**NFS, Ceph, or iSCSI**).
3. Configure it as follows:
   - **ID**: `SharedStorage`
   - **Server**: IP of the storage server
   - **Path**: `/mnt/shared` (Example for NFS)
4. Click **Add**.

#### ✅ Move existing VM disks to shared storage:
```bash
qm move_disk <VM_ID> <Storage_Name>
```

---

## 📌 Step 3: Enabling HA for a Virtual Machine
### **3.1 Add a VM to HA**
1. Shut down the VM.
2. Go to **Datacenter → HA → Add Resource**.
3. Select:
   - **Type**: VM
   - **VM ID**: Choose your VM
   - **Max Restart**: `3`
   - **Max Relocate**: `1`
4. Click **Add**.

---

## 📌 Step 4: Simulating a Node Failure (Demo)
### **4.1 Check Initial HA Status**
```bash
ha-manager status
```

### **4.2 Simulate a Failure**
To test HA, manually stop a node:
```bash
systemctl stop pve-cluster
```
Or unplug the network cable.

### **4.3 Observe Automatic Failover**
1. Run `ha-manager status` again.
2. The VM should migrate automatically.
3. The VM should be running on another node within **seconds**.

---

## 📌 Step 5: Verifying and Monitoring HA
Check HA logs:
```bash
journalctl -u pve-ha-lrm -f
```

Remove a VM from HA:
```bash
ha-manager remove <VM_ID>
```

---

## 🎯 Conclusion
✅ **Proxmox Clustering** enables centralized management.
✅ **High Availability (HA)** ensures automatic VM failover.
✅ **Shared Storage** is **mandatory** for HA.
✅ **At least 3 nodes** are required to prevent split-brain issues.

