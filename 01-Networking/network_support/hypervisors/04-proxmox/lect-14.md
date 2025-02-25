# Proxmox Network Setup: Management and VM Network Separation

## Overview
This guide walks through the process of setting up separate **management** and **VM networks** in Proxmox, ensuring network isolation and better security.

---

## 1. Current Network Setup

### Log in to Proxmox Web UI
Open your browser and go to the Proxmox web console:
```
https://<proxmox-ip>:8006
```

### Check Existing Network Configuration
Navigate to:
```
Datacenter > Node (Proxmox server) > System > Network
```
You’ll see the following:
```
vmbr0        - Linux Bridge (Management Network)
enp5s0f0     - Physical Ethernet Port (10GbE)
enp5s0f1     - Another Ethernet Port (10GbE)
```
`vmbr0` is the default bridge for management traffic, with an IP like `192.168.1.100/24`.

---

## 2. Create a Separate VM Network (Linux Bridge)

### Create a New Bridge
1. Click **Create** > **Linux Bridge**.

### Configure the New Bridge (`vmbr1`)
- **Name:** `vmbr1`
- **IP Address:** Choose a separate subnet for the VM network:
```
10.10.10.1/24
```
- **Gateway:** Leave blank (Proxmox only needs one gateway).
- **Bridge Ports:** Select an unused interface like `enp5s0f1`.
- **Comment:** `VM Network`

### Apply Configuration
Click **Create** and **Apply Configuration** when prompted.

### Confirm New Network
```
vmbr0       - Management Network (192.168.1.100/24)
vmbr1       - VM Network (10.10.10.1/24)
```

---

## 3. Assign VMs to the New Network

### Select a Virtual Machine
Go to:
```
Datacenter > Node > VM > Hardware
```

### Edit the Network Device
1. Click **Network Device** > **Edit**.
2. Change **Bridge** from `vmbr0` to `vmbr1`.
3. Click **OK**.

### Verify IP Address
Start the VM and check its IP address:
```
ip a
```
You should see an address like `10.10.10.x`.

---

## 4. Test Network Separation

### Management Network (`vmbr0`)
- Access Proxmox web interface from the management network (`192.168.1.x`).

### VM Network (`vmbr1`)
- VMs should have IPs like `10.10.10.x`.
- Accessing the Proxmox web interface from a VM on this network **should not work** unless firewall rules allow it.

---

## 5. (Optional) Advanced Setup

- **Set up VLANs:** Further isolate traffic using VLANs (`10.10.10.0/24` for app servers, `10.10.20.0/24` for databases).
- **Configure Firewall Rules:** Ensure only authorized devices can access the management network.
- **Create a Proxmox Cluster:** Replicate the VM network (`vmbr1`) on all nodes.

---

## Final Thoughts
You’ve successfully set up **network separation** in Proxmox, ensuring:
- **Management network (`vmbr0`)** is isolated and secure.
- **VM network (`vmbr1`)** keeps virtual machine traffic separate.
- **Better performance and security** overall.

