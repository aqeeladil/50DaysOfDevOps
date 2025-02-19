# Create and Format a New Partition Using `parted`

This guide provides step-by-step instructions to create and format a new partition using `parted` on Linux.

---

## **Step 1: Open `parted` on the Disk**
Run the following command to open `parted` on your chosen disk:

```bash
sudo parted /dev/sda
```
- Replace `/dev/sda` with the correct disk name.

---

## **Step 2: Display the Current Partitions**
Before making changes, check the existing partitions:

```bash
print
```
- This will display the partition table and help determine available space.

---

## **Step 3: Create a New 30GB Partition**
Inside the `parted` prompt, create a new partition:

```bash
mkpart primary ext4 0% 30GB
```
- `mkpart` creates a new partition.
- `primary` specifies it as a primary partition.
- `ext4` sets the file system type (this is optional at this stage).
- `0% 30GB` defines the start and end of the partition.

Exit `parted` by typing:
```bash
quit
```

---

## **Step 4: Format the New Partition to Ext4**
Format the newly created partition:

```bash
sudo mkfs.ext4 /dev/sdaX
```
- Replace `/dev/sdaX` with the actual partition name (e.g., `/dev/sda3`).

---

## **Step 5: Verify the New Partition**
Check if the partition is successfully created and formatted:

```bash
lsblk -f
```
or
```bash
sudo blkid
```
- These commands display the partitions and their file system details.

---

## **Step 6: Mount the New Partition**
Create a mount point and mount the partition:

```bash
sudo mkdir -p /mnt/new_partition
sudo mount /dev/sdaX /mnt/new_partition
```
- Replace `/dev/sdaX` with the correct partition name.

---

## **Step 7: Confirm the Partition is Mounted**
Verify that the partition is mounted:

```bash
df -h | grep /mnt/new_partition
```
or
```bash
mount | grep /dev/sdaX
```

---

## **Optional: Make the Mount Permanent**
To ensure the partition mounts automatically at boot, add it to `/etc/fstab`:

```bash
echo "/dev/sdaX /mnt/new_partition ext4 defaults 0 2" | sudo tee -a /etc/fstab
```

---

### **Notes:**
- Be careful when selecting a disk (`/dev/sda`) to avoid data loss.
- Always back up important data before modifying partitions.
- Use `lsblk` to confirm disk and partition names.





