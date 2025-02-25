# Proxmox Container Template Setup and Cloning Guide

## Overview
This guide walks you through creating and configuring an LXC container in Proxmox, converting it to a reusable template, and cloning new containers from that template. Each cloned container will have unique SSH keys and machine IDs.

---

## 1. Accessing Proxmox Web Interface
Open your browser and navigate to:

```
https://<your-proxmox-server-ip>:8006
```

---

## 2. Creating a New Container
- Click **Create CT** in the Proxmox web interface.
- Fill in the details:
    - **Hostname:** `ubuntu-container-1`
    - **Password:** Set a root password
    - **Template:** Choose an Ubuntu LXC template
    - **Storage:** Select `local-lvm` or your preferred storage
    - **Disk Size:** 8 GB (or preferred size)
    - **CPU:** 1 core
    - **Memory:** 1024 MB
    - **Network:** Bridge `vmbr0`, DHCP enabled
- Click **Finish**.

---

## 3. Start and Access the Container
- Right-click the container -> **Start**
- Access the console: Right-click -> **Console**
- OR SSH into the container:

```bash
ssh root@<container-ip>
```

---

## 4. Update and Clean the Container
**Update the container:**

```bash
sudo apt update && sudo apt dist-upgrade -y
```

**Clean the APT cache:**

```bash
sudo apt clean
```

**Remove unnecessary packages:**

```bash
sudo apt auto-remove -y
```

---

## 5. Remove SSH Host Keys
Every machine should have unique SSH keys:

```bash
sudo rm /etc/ssh/ssh_host_*
```

⚠️ **Important:** Do NOT disconnect your SSH session after this step.

---

## 6. Clear the Machine ID

```bash
sudo truncate -s 0 /etc/machine-id
```

---

## 7. Power Off the Container

```bash
sudo poweroff
```

---

## 8. Convert Container to Template
- Right-click the container -> **Convert to Template**
- Confirm the action. The icon will change to a template icon.

---

## 9. Clone the Template
- Right-click the template -> **Clone**
- **Name:** `webserver-ct-1`
- **Clone Mode:** Full Clone
- **Target Storage:** `local-lvm`
- Click **Clone**

Repeat this step to create additional containers.

---

## 10. Start the Cloned Containers
- Right-click each cloned container -> **Start**

---

## 11. Regenerate SSH Keys for Cloned Containers
For each new container:

- Open the console or SSH into the container.
- Remove old SSH keys:

```bash
sudo rm /etc/ssh/ssh_host_*
```

- Regenerate new SSH keys:

```bash
sudo dpkg-reconfigure openssh-server
```

---

## 12. Verify Unique Machine ID
Check that each container has a unique machine ID:

```bash
cat /etc/machine-id
```

---

## 13. Done! 🎉
You’ve successfully:

- ✅ Created a clean, optimized container
- ✅ Converted it into a reusable Proxmox template
- ✅ Cloned multiple containers from the template
- ✅ Regenerated unique SSH keys and machine IDs for each container

