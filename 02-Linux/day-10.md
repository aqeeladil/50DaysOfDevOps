# Partition Management and File Systems

## 1. Partition Types

### Purpose of Partitions:
- **Data Partition**: Used to store user files, system files, and application data.
- **Swap Partition**: Used as virtual memory when physical RAM is full, improving system stability under heavy load.

### When to Use:
- **Data Partition**: Always needed to store system and user data.
- **Swap Partition**: Recommended for systems with limited RAM (e.g., servers or low-memory devices).
  - **Swap Size Recommendations**:
    - RAM < 2GB: Swap should be 2x RAM
    - RAM 2GB-8GB: Swap should be equal to RAM
    - RAM > 8GB: Swap should be 0.5x RAM (or omitted for high-memory systems)

## 2. File System Selection

| File System | Compatibility | Performance | Features |
|-------------|--------------|-------------|----------|
| **FAT** | Universal (Windows, Linux, macOS) | Low | No journaling, 4GB file size limit |
| **exFAT** | Windows, macOS, Linux (with drivers) | Moderate | No journaling, supports large files |
| **HFS Plus** | macOS | Moderate | Journaling, macOS-specific features |
| **Ext (Ext4)** | Linux | High | Journaling, large file support, better performance |
| **XFS** | Linux | High | Optimized for large files, ideal for databases |
| **NTFS** | Windows, Linux (read/write with drivers) | High | Journaling, Windows-specific features |

### When to Use:
- **Ext4**: Best for general Linux usage.
- **XFS**: Recommended for high-throughput workloads (e.g., databases, large file storage).
- **NTFS**: For shared storage between Windows and Linux.
- **exFAT**: Ideal for external drives with cross-platform support.

## 3. File System Performance

### Recommended File System for High-Performance Server:
- **Ext4 or XFS**: Efficient for large files and high-performance needs.
- **Impact on Performance**:
  - Journaling reduces data corruption risk.
  - Block size and indexing optimize file handling speed.
  - XFS handles parallel workloads better than Ext4.

## 4. File System Features

### Ext4 vs. FAT:
- **Ext4**:
  - Journaling for crash recovery.
  - Large file support (up to 16TB).
  - Reduced fragmentation.
- **FAT**:
  - No journaling.
  - 4GB file size limit.
  - Higher fragmentation over time.

## 5. Data Recovery

### Resiliency of File Systems:
- **Ext4**: More resilient due to journaling.
- **FAT/exFAT**: More prone to corruption; no built-in journaling.
- **HFS Plus**: Journaling provides some protection but mainly for macOS.

### Recovery Tools:
- **Ext4**: `fsck`, `extundelete`, `e2fsck`
- **FAT/exFAT**: `testdisk`, `photorec`
- **HFS Plus**: `diskutil`, `fsck_hfs`

#### Example: Checking and Repairing an Ext4 File System
```bash
sudo e2fsck -f /dev/sda1
```

## 6. Creating Partitions

To create a new primary partition of size 20GB on `/dev/sda`:
```bash
sudo parted /dev/sda mkpart primary ext4 0% 20GB
```

#### Example: Creating a Swap Partition
```bash
sudo parted /dev/sda mkpart primary linux-swap 20GB 24GB
sudo mkswap /dev/sda2
sudo swapon /dev/sda2
```

## 7. Viewing Current Partitions

To list all partitions on a disk:
```bash
sudo parted /dev/sda print
```
**Expected Output:**
- Partition number
- Start/End sectors
- Size
- File system type
- Flags (bootable, etc.)

## 8. Modifying Partitions

To increase a partition size by 10GB using parted:
```bash
sudo parted /dev/sda resizepart 1 30GB
```
### **Warning:**
- Ensure that there is free space available after the partition.
- Resizing partitions without proper backup can lead to data loss.

## 9. Formatting Partitions

After creating a partition, format it to Ext4:
```bash
sudo mkfs.ext4 /dev/sda1
```
#### Example: Formatting a New XFS Partition
```bash
sudo mkfs.xfs /dev/sda3
```

## 10. Setting Flags

To set the boot flag on a partition:
```bash
sudo parted /dev/sda set 1 boot on
```
### Importance:
- Required for bootable disks (especially for legacy BIOS systems).

## 11. Removing Partitions

To safely remove a partition:
```bash
sudo parted /dev/sda rm 1
```
### Precautions:
- Ensure backup of important data.
- Verify correct partition number before deletion.
- Check if the partition is mounted before removal using:
```bash
lsblk
```

---
