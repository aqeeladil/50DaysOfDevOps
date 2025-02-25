# Proxmox Backup and Snapshot Guide

This guide walks you through setting up and managing backups and snapshots in Proxmox.

---

## 1. Setting the Stage

**Assumptions:**
- Proxmox is installed and running.
- There is a virtual machine (VM) named `Ubuntu-Test`.
- The VM contains important configurations or data.

---

## 2. Creating a Snapshot

Snapshots save the current state of a VM and are perfect for quick, temporary backups.

1. Open **Proxmox Web Interface**: `https://your-proxmox-ip:8006`
2. Navigate to: **Datacenter** > **[Your Node]** > **[Your VM]**
3. Click on **Snapshots** in the left menu.
4. Click **Take Snapshot**.
5. Fill in the details:
   - **Name:** `Before-Update`
   - **Description:** `Snapshot before installing Nginx`
   - **Include RAM:** (Optional, saves the running state)
   - **Include Disk State:** (Keep this checked)
6. Click **Create**.

Your snapshot is now created!

---

## 3. Rolling Back a Snapshot

If something goes wrong, you can revert your VM to a previous state.

1. Go to the **Snapshots** tab of your VM.
2. Select the desired snapshot (e.g., `Before-Update`).
3. Click **Rollback**.
4. Confirm the rollback.

Your VM will instantly revert to the saved state.

---

## 4. Taking a Backup

Backups are more comprehensive and portable.

1. Navigate to: **Datacenter** > **[Your Node]** > **[Your VM]**.
2. Click **Backup** in the left menu.
3. Click **Backup Now**.
4. Choose your settings:
   - **Storage:** `local` or attached storage.
   - **Mode:**
      - `Snapshot` (minimal downtime)
      - `Suspend` (brief downtime)
      - `Stop` (most consistent, longest downtime)
   - **Compression:** `LZO` (faster) or `ZSTD` (smaller size).
   - **Backup Format:** `VMA` (default).
5. Click **Start**.

The VM backup will be saved as a `.vma` file.

---

## 5. Restoring a Backup

If needed, you can restore your VM from a backup.

1. Navigate to: **Datacenter** > **[Your Node]** > **[Storage]**.
2. Find the backup file (e.g., `Ubuntu-Test.vma`).
3. Click the backup and choose **Restore**.
4. Configure:
   - **VM ID:** (Same or new ID)
   - **Storage:** Where the VM’s disk will be restored.
5. Click **Restore**.

Your VM is now restored to the backup state.

---

## 6. Automating Backups

Automate backups to avoid manual effort.

1. Go to **Datacenter** > **Backup**.
2. Click **Add**.
3. Set your preferences:
   - **Node:** Your Proxmox server.
   - **Storage:** Where backups will be saved.
   - **Selection:** All VMs or specific ones.
   - **Schedule:** Cron format (e.g., `0 3 * * 5` for Fridays at 3 AM).
   - **Mode:** `Snapshot`, `Suspend`, or `Stop`.
   - **Compression:** `LZO` or `ZSTD`.
4. Click **Create**.

Backups will now run on the set schedule.

---


