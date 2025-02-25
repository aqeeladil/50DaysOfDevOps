# Proxmox Virtual Machine Creation Guide

This guide provides comprehensive instructions for creating and configuring virtual machines in Proxmox VE.

## Prerequisites

Before creating a virtual machine in Proxmox, ensure you have:

- A functioning Proxmox VE installation
- Admin access to the Proxmox web interface
- Sufficient hardware resources (CPU, RAM, storage)
- An ISO image for your operating system

## Resource Planning

Check available resources before creating VMs:

1. Log into the Proxmox web interface
2. View the Summary tab to check:
   - Available memory (RAM)
   - CPU usage
   - Storage space

## Creating a Virtual Machine

### Basic Configuration

1. Click the "Create VM" button in the top-right corner
2. Configure the VM ID and Name:
   - **Node**: Select your Proxmox node
   - **VM ID**: Choose a unique ID (default starts at 100)
   - **Name**: Give your VM a descriptive name (e.g., "web-server")
   - **Resource Pool**: Optional grouping (can be left empty)

### OS Selection

#### Adding an ISO Image

If you don't have the required ISO:

1. Navigate to local storage > ISO Images
2. Click "Download from URL"
3. Paste the URL of your ISO
4. Click "Query URL" to verify, then "Download"
5. Wait for download to complete

#### OS Settings

Select your downloaded ISO and configure OS settings:

- **ISO Image**: Choose from your available ISOs
- **Guest OS Type**: Select appropriate OS (Linux, Windows, Other)
- **Version**: Select specific version if applicable

### System Settings

Configure system components:

- **SCSI Controller**: Default (VirtIO SCSI) works for most cases
- **Graphics Card**: Default is sufficient for server VMs
- **BIOS**: Leave as default (SeaBIOS) unless you need UEFI

### Disk Configuration

Set up virtual disk:

- **Bus/Device**: Leave as default (SCSI)
- **Storage**: Select your storage pool (e.g., "local-lvm")
- **Disk Size**: Choose appropriate size (e.g., 16GB)
- **Format**: Use default (qcow2/raw depending on storage)
- **Enable Discard**: Check this if your host uses SSD storage (enables TRIM)

### CPU Allocation

Configure CPU resources:

- **Sockets**: Usually leave at 1
- **Cores**: Start with 1 core (increase only if needed)
- **Type**: Host (for best performance)

> **Recommendation**: Start with minimal CPU allocation and increase later if needed.

### Memory Allocation

Configure RAM:

- **Memory**: Allocate RAM based on VM needs

Minimum recommendations:
- Linux servers: 1GB minimum
- Windows: 2GB minimum
- Production databases/services: 4GB+

### Network Configuration

Set up networking:

- **Bridge**: Select your network bridge (default: vmbr0)
- **Model**: VirtIO offers best performance
- **MAC Address**: Auto-generated or custom

> **Best Practice**: For production environments, separate management traffic from VM traffic using different network bridges.

## VM Options

Configure additional options before starting the VM:

1. Select your VM from the left sidebar
2. Click on "Options" tab
3. Configure critical settings:
   - **Start at boot**: Enable for production VMs
   - **Start/shutdown order**: Set for dependent services
   - **Guest agent**: Should be enabled (requires installation in the guest OS)

## OS Installation

1. Click the "Start" button to boot the VM
2. Click "Console" to view the VM's display
3. Follow the OS installation process

### Ubuntu Server Example

1. Select language and keyboard layout
2. Configure network (DHCP is usually fine)
3. Set up storage (use entire disk for simplicity)
4. Create user account and password
5. Install OpenSSH for remote management
6. Complete installation and reboot

## Post-Installation Configuration

### System Updates

Update your newly installed system:

```bash
sudo apt update && sudo apt dist-upgrade
```

### QEMU Guest Agent

1. Install the QEMU guest agent:

```bash
sudo apt install qemu-guest-agent
```

2. Enable the guest agent in Proxmox:
   - Go to VM > Options
   - Edit "QEMU Guest Agent"
   - Check "Enabled"
   - Click "OK"

3. Restart the VM to apply changes:

```bash
sudo shutdown -r now
```

4. Verify guest agent is running:

```bash
systemctl status qemu-guest-agent
```

### Testing VM Functionality

Test that your VM is working properly:

1. Install a sample application (Apache web server):

```bash
sudo apt install apache2
```

2. Verify network connectivity:
   - Open a web browser
   - Navigate to the VM's IP address (e.g., http://192.168.1.100)
   - You should see the default Apache welcome page

## Best Practices

### Resource Allocation
- Start with minimal resources and increase based on monitoring
- Over-allocation can waste host resources

### VM ID Organization
- Develop a numbering scheme (e.g., 100-199: web servers, 200-299: databases)
- Use consistent naming conventions for easier management

### QEMU Guest Agent
- Always install for better integration with Proxmox
- Enables accurate memory reporting and clean shutdowns

### Templates
- After configuring a base VM, convert it to a template
- Use templates to quickly deploy new VMs with consistent configurations

### Snapshots
- Take snapshots before major changes
- Enables quick rollback if needed

## Troubleshooting

### VM Won't Start
- Check resource availability
- Verify ISO image is valid
- Check VM logs for specific errors

### Installation Issues
- Increase memory allocation if installation crashes
- Verify ISO checksum
- Try a different OS version

### Network Problems
- Verify bridge configuration
- Check VM network settings
- Confirm host firewall settings

### Performance Issues
- Monitor resource usage
- Adjust CPU, RAM based on actual utilization
- Consider storage I/O bottlenecks

---

This guide covers the basics of creating and configuring VMs in Proxmox. For more advanced configurations and detailed information, refer to the [official Proxmox documentation](https://pve.proxmox.com/pve-docs/).