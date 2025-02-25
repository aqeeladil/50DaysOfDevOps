# Creating an Ubuntu 22.04 Template in Proxmox

This guide demonstrates how to create an Ubuntu 22.04 template in Proxmox using cloud images instead of traditional ISO files, along with cloud-init for easy VM configuration.

## Overview

Using cloud images offers several advantages:
- **Pre-installed OS**: No need to go through the installation process
- **Cloud-init integration**: Easily configure username, password, SSH keys, and networking
- **Faster deployment**: Clone VMs much more quickly
- **Consistency**: All VMs created from the template have identical base configurations

## Prerequisites

- Proxmox VE 7.0+ installed and operational
- SSH access to Proxmox host
- Internet access to download cloud images
- Basic understanding of Proxmox VM management

## Step 1: Creating the Base Virtual Machine

1. In the Proxmox web interface, click on "Create VM"

2. **VM Settings**:
   - **VM ID**: Use 900 (or any high number to place it at the bottom of the list)
   - **Name**: ubuntu-2204-template
   - **Node**: Select your preferred Proxmox node
   - Click "Next"

3. **OS Settings**:
   - Select "Do not use any media" since we'll use a cloud image instead of an ISO
   - Click "Next"

4. **System Settings**:
   - Check "QEMU Guest Agent" (this will be activated later)
   - Click "Next"

5. **Disk Settings**:
   - Delete the automatically created disk (we'll add one later from the cloud image)
   - Click "Next"

6. **CPU Settings**:
   - Leave defaults (1 socket, 1 core is sufficient for a template)
   - Click "Next"

7. **Memory Settings**:
   - Set to 1024MB (minimal but sufficient for a template)
   - Click "Next"

8. **Network Settings**:
   - Select your preferred network bridge (vmbr1 for dedicated VM network, or vmbr0 if you only have one)
   - Click "Next"

9. **Confirm Settings**:
   - Review all settings and click "Finish"

## Step 2: Configuring Cloud-Init

1. Select your newly created VM and go to the "Hardware" tab

2. Click "Add" and select "CloudInit Drive"
   - For storage, select your preferred storage (like local-lvm)
   - Click "Add"

3. Go to the "Cloud-Init" tab and configure:
   - **User**: Set your preferred username
   - **Password**: Set a secure password
   - **SSH Public Keys**: Paste your SSH public key (optional but recommended)

4. In the "Network" section:
   - Configure network to use DHCP
   - Click "Regenerate Image"

## Step 3: Configuring VGA Console

1. SSH into your Proxmox host:
   ```bash
   ssh root@your-proxmox-server
   ```

2. Run the following command to enable standard VGA for your VM (replace 900 with your VM ID):
   ```bash
   qm set 900 -vga std
   ```

   This ensures you'll be able to see console output when the VM boots.

## Step 4: Downloading and Preparing the Cloud Image

1. Find the URL for the Ubuntu 22.04 cloud image by visiting:
   ```
   https://cloud-images.ubuntu.com/minimal/releases/jammy/release/
   ```

2. Download the image to your Proxmox server:
   ```bash
   wget https://cloud-images.ubuntu.com/minimal/releases/jammy/release/ubuntu-22.04-minimal-cloudimg-amd64.img
   ```

3. Rename the image file with a .qcow2 extension:
   ```bash
   mv ubuntu-22.04-minimal-cloudimg-amd64.img ubuntu-2204.qcow2
   ```

4. Resize the image to your preferred size (32GB in this example):
   ```bash
   qemu-img resize ubuntu-2204.qcow2 32G
   ```

## Step 5: Importing the Disk to the VM

1. Import the prepared disk to your VM:
   ```bash
   qm importdisk 900 ubuntu-2204.qcow2 local-lvm
   ```
   (Replace 900 with your VM ID and local-lvm with your storage name)

2. In the Proxmox web interface:
   - Go to your VM
   - Go to the "Hardware" tab
   - Double-click the "Unused Disk 0" entry
   - If using SSD storage:
     - Check "Discard" option
     - Click "Advanced"
     - Check "SSD emulation"
   - Click "Add"

## Step 6: Configuring Boot Order and VM Options

1. Go to the "Options" tab of your VM

2. Find and click on "Boot Order"
   - Enable the hard disk (scsi0)
   - Drag it to second position (after CD-ROM)
   - Click "OK"

3. Optionally, enable "Start at boot" if you want VMs created from this template to start automatically when Proxmox boots

## Step 7: Converting to a Template

1. Right-click on your VM in the left sidebar

2. Select "Convert to Template"

3. Confirm the action. This will change the VM's status to template (shown by a different icon)

## Step 8: Creating a VM from the Template

1. Right-click on the template in the sidebar

2. Select "Clone"

3. Configure the clone:
   - **VM ID**: Choose a new ID (e.g., 799)
   - **Name**: Give your new VM a name (e.g., ubuntu-test)
   - **Mode**: Select "Full Clone" for a complete independent copy
   - Click "Clone"

4. Start the new VM and open the console:
   - Right-click the VM
   - Select "Start"
   - Click "Console"

5. Wait for the VM to boot fully and for cloud-init to complete its configuration

6. Log in with the username and password you configured in cloud-init

## Step 9: Installing the QEMU Guest Agent

1. Once logged in, update your package list:
   ```bash
   sudo apt update
   ```

2. Install the QEMU guest agent:
   ```bash
   sudo apt install qemu-guest-agent
   ```

3. Reboot the VM to activate the agent:
   ```bash
   sudo reboot
   ```

4. After reboot, verify the agent is running:
   ```bash
   systemctl status qemu-guest-agent
   ```

5. Test Proxmox integration by shutting down the VM from the Proxmox interface (right-click VM > Shutdown)

## Troubleshooting

- **VM not booting**: Verify boot order is configured correctly
- **No console output**: Check if the VGA configuration was applied correctly
- **No network connectivity**: Ensure cloud-init network settings are configured properly
- **Cannot login**: Wait for cloud-init to finish provisioning the user account

## Benefits of Using This Approach

- **Speed**: Creating new VMs takes seconds instead of minutes
- **Consistency**: Every VM starts with identical base configuration
- **Automation**: Cloud-init handles initial setup automatically
- **Resource efficiency**: Templates can be stored efficiently

## Additional Resources

- [Proxmox Documentation](https://pve.proxmox.com/pve-docs/)
- [Ubuntu Cloud Images](https://cloud-images.ubuntu.com/)
- [Cloud-Init Documentation](https://cloudinit.readthedocs.io/)

