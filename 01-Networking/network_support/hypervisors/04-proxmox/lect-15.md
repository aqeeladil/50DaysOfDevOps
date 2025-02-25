# 📂 Shared NFS Storage for Proxmox Using TrueNAS

This guide walks through setting up shared NFS storage for Proxmox Virtual Environment (PVE) using TrueNAS. This setup enables centralized storage for VM disk images, backups, and ISOs — perfect for high availability and live migration.

---

## 🛠 Prerequisites

- **TrueNAS installed and running** (virtual or physical)
- **Proxmox VE installed** (single node or cluster)
- **Both machines on the same network**

---

## 🌀 Step 1: Set Up Datasets on TrueNAS

1. **Log in to the TrueNAS Web UI**
2. Navigate to **"Storage" > "Pools"** and select your storage pool
3. Click **"Add Dataset"** and create:
    - **Dataset Name:** `pve_shared` (for VM disk images, templates, ISOs)
    - **Dataset Name:** `pve_backups` (for VM and container backups)
4. **Set permissions:**
    - Go to **"Permissions"** on each dataset
    - Change ownership to a **proxmox user** (or create one)
    - Set permissions to **Read/Write/Execute** for the user and group

---

## 🌐 Step 2: Configure NFS Shares in TrueNAS

1. Go to **"Sharing" > "Unix (NFS) Shares"** and click **"Add"**
2. For `pve_shared`:
    - **Path:** `/mnt/yourpool/pve_shared`
    - **Allow non-root access:** ✅
    - **Authorized networks:** Your Proxmox network subnet (e.g., `192.168.1.0/24`)
3. Click **"Save"** and enable the NFS service
4. Repeat for `pve_backups`

---

## 💻 Step 3: Mount NFS Shares on Proxmox

1. Log in to the **Proxmox Web UI**
2. Go to **"Datacenter" > "Storage" > "Add" > "NFS"**
3. Configure the backup storage:
    - **ID:** `nfs-backups`
    - **Server:** IP of your TrueNAS server (e.g., `192.168.1.100`)
    - **Export:** `/mnt/yourpool/pve_backups`
    - **Content:** **VZDump backup files**
4. Add shared VM storage:
    - **ID:** `nfs-shared`
    - **Server:** IP of TrueNAS
    - **Export:** `/mnt/yourpool/pve_shared`
    - **Content:** **Disk image, Container, ISO image, VZDump backups**

---

## 🚀 Step 4: Test the Storage

1. Go to **"Datacenter" > "Storage"** and select `nfs-shared`
2. Upload an **ISO image** to test file access
3. Create a new **VM or container** and store its disk on `nfs-shared`
4. Run a **backup job** and store it in `nfs-backups`

---

## ✅ Step 5: Confirm Shared Storage (Optional HA)

1. Ensure multiple Proxmox nodes see and access the NFS storage
2. Enable **High Availability (HA)** and migrate VMs without moving storage

---


