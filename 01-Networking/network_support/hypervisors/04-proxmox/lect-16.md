# Proxmox VE Cluster Setup Guide 🚀

This guide walks you through setting up a **Proxmox VE Cluster** from scratch, including network setup, cluster creation, and live VM migration.

---

## 🛠 Prerequisites
- **3 Proxmox VE servers** installed and running (`pve1`, `pve2`, `pve3`)
- Consistent network setup across all servers
- All servers reachable over the network
- Root access to all Proxmox nodes

---

## 1️⃣ Network Setup
Ensure all Proxmox nodes have the **same network configuration**.

On each server:
1. Go to **Proxmox Web UI** (`https://<server-ip>:8006`)
2. Navigate to **System → Network**
3. Ensure at least two networks:
   - `vmbr0` → Management Network (Proxmox Web UI and SSH access)
   - `vmbr1` → VM Network (where VMs will run)

*If any of them are missing:*
1. Click **Create → Linux Bridge**
2. Name it `vmbr1`, set an IP if required, and bind the correct physical interface
3. Apply and reboot if needed

---

## 2️⃣ Configure Hostnames & DNS
Ensure all servers recognize each other by hostname.

On each server, edit `/etc/hosts`:

```bash
sudo nano /etc/hosts
```

Add these lines (replace IPs with your real server IPs):

```bash
192.168.1.100 pve1.local pve1
192.168.1.101 pve2.local pve2
192.168.1.102 pve3.local pve3
```

Save and exit.

---

## 3️⃣ Create the Proxmox Cluster
On `pve1` (the first server):
1. Go to **Datacenter → Cluster**
2. Click **Create Cluster**
3. Enter a Cluster Name (e.g., `my-cluster`)
4. Choose the **Network** for cluster communication (e.g., `192.168.1.0/24`)
5. Click **Create**

Once ready, `pve1` will appear in the cluster.

---

## 4️⃣ Join Other Nodes
On `pve2` and `pve3`:
1. Go to **Datacenter → Cluster**
2. Click **Join Cluster**
3. Go back to `pve1` → **Join Information** → Copy the join command
4. Paste the command in the Shell of `pve2` and `pve3`
5. Enter the root password of `pve1` when prompted
6. Wait for the nodes to join — they’ll appear in the Cluster view

---

## 5️⃣ Verify the Cluster
On any server, check the cluster status:

```bash
pvecm status
```

Expected Output:

```bash
Cluster information
-------------------
Name: my-cluster
Nodes: 3
Quorum: 2 (activity)
```

---

## 6️⃣ Create a VM
On `pve1`, create a virtual machine:
1. Go to **Datacenter → pve1 → Create VM**
2. Configure the VM with a disk on `local-lvm`, 2GB RAM, and 2 vCPUs
3. Install an OS like Ubuntu or use a Cloud-Init image
4. Start the VM and ensure it’s running

---

## 7️⃣ Live Migrate the VM
Move a running VM from `pve1` to `pve2` without downtime:
1. Right-click the running VM → **Migrate**
2. Choose **pve2** as the target
3. Confirm and watch the migration in real-time

Check the VM’s connectivity during migration:

```bash
ping <vm-ip>
```

---

## 8️⃣ Success! 🎉
- All nodes are working together in one unified cluster
- VMs can move between nodes without downtime
- Network and storage remain consistent across nodes

---
