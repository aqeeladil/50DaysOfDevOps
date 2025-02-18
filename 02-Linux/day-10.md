## Partition Management and File Systems

1. Partition Types:
o What is the purpose of a data partition versus a swap partition? When would you 
use each type in a Linux environment?

2. File System Selection:
o Compare and contrast the FAT, exFAT, HFS Plus, and Ext file systems. What are the 
advantages and disadvantages of each in terms of compatibility, performance, and 
features?

3. File System Performance:
o Which file system would you recommend for a high-performance server with large 
files and why? Discuss the impact of file system choice on performance.

4. File System Features:
o Explain how Ext4 provides features like journaling and support for large files. How 
does this differ from the FAT file system?

5. Data Recovery:
o If a data partition is corrupted, which file systems (FAT, exFAT, HFS Plus, Ext) are 
more resilient, and what tools or methods can you use to recover data from these 
file systems?

6. Creating Partitions:
o Using parted, how would you create a new primary partition of size 20GB on 
/dev/sda? Provide the command sequence you would use.

7. Viewing Current Partitions:
o Describe how to use parted to list all partitions on a disk. What command would 
you use, and what information can you expect to see?

8. Modifying Partitions:
o If you want to resize a partition to increase its size by 10GB using parted, what steps 
would you take? Include any necessary commands.

9. Formatting Partitions:
o After creating a new partition using parted, how would you format it to Ext4? Provide 
the command used for formatting.

10. Setting Flags
o Explain how to set the boot flag on a partition using parted. Why is this important for 
a bootable disk?

11. Removing Partitions:
o How would you safely remove a partition using parted? Describe the commands 
and precautions you would take to avoid data loss

