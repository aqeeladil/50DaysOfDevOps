# Partition Management and File Systems

## 1. Partition Types

### Purpose of Partitions:
- **Data Partition**: Used to store user files, system files, and application data.
- **Swap Partition**: Used as virtual memory when physical RAM is full, improving system stability under heavy load.

### When to Use:
- **Data Partition**: Always needed to store system and user data.
- **Swap Partition**: Recommended for systems with limited RAM (e.g., servers or low-memory devices).

## 2. File System Selection

| File System | Compatibility | Performance | Features |
|-------------|--------------|-------------|----------|
| **FAT** | Universal (Windows, Linux, macOS) | Low | No journaling, 4GB file size limit |
| **exFAT** | Windows, macOS, Linux (with drivers) | Moderate | No journaling, supports large files |
| **HFS Plus** | macOS | Moderate | Journaling, macOS-specific features |
| **Ext (Ext4)** | Linux | High | Journaling, large file support, better performance |

## 3. File System Performance

### Recommended File System for High-Performance Server:
- **Ext4 or XFS**: Efficient for large files and high-performance needs.
- **Impact on Performance**:
  - Journaling reduces data corruption risk.
  - Block size and indexing optimize file handling speed.

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
- **Ext4**: `fsck`, `extundelete`
- **FAT/exFAT**: `testdisk`, `photorec`
- **HFS Plus**: `diskutil`, `fsck_hfs`

## 6. Creating Partitions

To create a new primary partition of size 20GB on `/dev/sda`:
```bash
sudo parted /dev/sda mkpart primary ext4 0% 20GB
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

## 9. Formatting Partitions

After creating a partition, format it to Ext4:
```bash
sudo mkfs.ext4 /dev/sda1
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

---
This README provides a practical guide to partition management and file system selection in Linux. Use the provided commands and explanations to efficiently manage storage on your system.

