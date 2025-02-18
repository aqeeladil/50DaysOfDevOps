## Task: Create a new LVM setup with a logical volume

1. Install LVM (if not already installed):
2. Initialize a physical volume on a new disk (e.g., /dev/sdb):
3. Create a volume group named vg_data:
4. Create a logical volume named lv_storage of size 10GB:
5. Format the logical volume with a file system (e.g., Ext4):
6. Mount the logical volume to a directory (e.g., /mnt/storage):
7. Verify the setup by checking the mounted file systems:
8. Create a snapshot of the logical volume (e.g., lv_storage_snapshot):
9. List the logical volumes to confirm the snapshot creation