# LVM Setup Guide

## Task: Create a New LVM Setup with a Logical Volume

This guide explains how to set up Logical Volume Manager (LVM) on a new disk and create a logical volume, format it, mount it, and create a snapshot.

---

## **Step 1: Install LVM (if not installed)**

Install LVM package based on your Linux distribution:

```bash
sudo apt update && sudo apt install lvm2 -y    # Debian/Ubuntu
sudo yum install lvm2 -y                       # RHEL/CentOS
sudo dnf install lvm2 -y                       # Fedora
```

Enable and start the LVM service:

```bash
sudo systemctl enable lvm2-lvmetad
sudo systemctl start lvm2-lvmetad
```

---

## **Step 2: Initialize a Physical Volume**

Initialize a new disk (`/dev/sdb`) as a physical volume for LVM:

```bash
sudo pvcreate /dev/sdb
```

Verify the physical volume:

```bash
sudo pvs
sudo pvdisplay
```

---

## **Step 3: Create a Volume Group**

Create a volume group named `vg_data` using `/dev/sdb`:

```bash
sudo vgcreate vg_data /dev/sdb
```

Verify the volume group:

```bash
sudo vgs
sudo vgdisplay vg_data
```

---

## **Step 4: Create a Logical Volume**

Create a logical volume named `lv_storage` of size 10GB:

```bash
sudo lvcreate -L 10G -n lv_storage vg_data
```

Verify the logical volume:

```bash
sudo lvs
sudo lvdisplay /dev/vg_data/lv_storage
```

---

## **Step 5: Format the Logical Volume**

Format the logical volume with the Ext4 file system:

```bash
sudo mkfs.ext4 /dev/vg_data/lv_storage
```

---

## **Step 6: Mount the Logical Volume**

Create a mount point and mount the logical volume:

```bash
sudo mkdir -p /mnt/storage
sudo mount /dev/vg_data/lv_storage /mnt/storage
```

Make the mount persistent by adding an entry to `/etc/fstab`:

```bash
echo "/dev/vg_data/lv_storage /mnt/storage ext4 defaults 0 2" | sudo tee -a /etc/fstab
```

---

## **Step 7: Verify the Setup**

Check the mounted file systems:

```bash
df -hT
mount | grep /mnt/storage
```

---

## **Step 8: Create a Snapshot**

Create a snapshot of `lv_storage` named `lv_storage_snapshot` (size should be sufficient to store changes, e.g., 2GB):

```bash
sudo lvcreate -L 2G -s -n lv_storage_snapshot /dev/vg_data/lv_storage
```

---

## **Step 9: List Logical Volumes**

Verify that the snapshot has been created:

```bash
sudo lvs
sudo lvdisplay
```

---

