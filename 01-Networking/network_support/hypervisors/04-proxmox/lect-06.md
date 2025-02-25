# Install Windows on Proxmox – Step-by-Step Guide

## 📌 Overview
This guide explains how to install **Windows 10/11** on **Proxmox Virtual Environment (PVE)**, including **VirtIO driver installation** for optimized performance.

---

## 📂 Step 1: Download Required Files

### 🔹 Windows ISO
- Download from Microsoft’s official website:
  - [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10)
  - [Windows 11 ISO](https://www.microsoft.com/en-us/software-download/windows11)
  - [Windows Server ISO](https://www.microsoft.com/en-us/evalcenter)

### 🔹 VirtIO Drivers
- Download the latest **VirtIO driver ISO**:
  - [VirtIO Windows Drivers](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/)

---

## 🔧 Step 2: Create a New Windows Virtual Machine

1. **Login to Proxmox Web Interface** (`https://your-proxmox-ip:8006`).
2. **Create VM** → Set **Name** (e.g., `Windows-10-VM`).
3. **OS Type**: Select **Microsoft Windows**.
4. **Select Windows ISO**.
5. **Disk Settings**:
   - **Bus/Controller**: `SCSI (virtio-scsi)`
   - **Disk Size**: `64GB` (recommended for Windows 10/11)
   - **Cache Mode**: `Write Back`
   - **Enable “Discard”** (for SSD TRIM support)
6. **CPU & RAM**:
   - **CPU**: `4 Cores` (or more)
   - **Type**: `host`
   - **RAM**: `8GB` (recommended)
   - **Enable Ballooning**.
7. **Network Adapter**:
   - **Model**: `VirtIO (paravirtualized)`
8. **Add VirtIO ISO**: Go to **Hardware → Add CD/DVD Drive** → Select **VirtIO driver ISO**.

---

## 🚀 Step 3: Install Windows with VirtIO Drivers

1. **Start the VM** → Open **Console**.
2. **Begin Windows Setup** → Select Language.
3. On the "Where do you want to install Windows?" screen, **no disks will appear**.
4. Click **"Load driver"** → **Browse VirtIO CD** → Select:
   ```
   viostor > w10 > amd64
   ```
5. **Continue installation**.

---

## 📥 Step 4: Install VirtIO Drivers in Windows

1. **Login to Windows**.
2. **Open File Explorer** → Navigate to **VirtIO CD drive**.
3. **Run `virtio-win-guest-tools.exe`** (automatically installs drivers).
4. **Manually install missing drivers (if needed)**:
   - **Network (Ethernet)**: `NetKVM > w10 > amd64`
   - **Balloon Memory Driver**: `Balloon > w10 > amd64`
   - **QXL Video Driver**: `QXL > w10 > amd64`

---

## 🔗 Step 5: Install QEMU Guest Agent

1. **Open VirtIO CD** → Install `qemu-ga-x86_64.msi`.
2. **Enable in Proxmox**:
   - Go to **Options** → Enable **QEMU Guest Agent**.

Now, Proxmox will correctly detect the **Windows IP address** and allow clean shutdowns.

---

## ⚙️ Step 6: Optimize Windows for Proxmox

### 💡 Enable VirtIO Disk Optimization
1. Open **Device Manager** (`devmgmt.msc`).
2. Expand **Disk Drives** → Right-click VirtIO Disk.
3. Go to **Policies** → Enable **Write-caching policy**.

### 🛠️ Enable TRIM for SSDs
Run the following command in **Command Prompt (Admin)**:
```powershell
fsutil behavior set DisableDeleteNotify 0
```

### ⚠️ Disable Windows Fast Startup
1. **Control Panel → Power Options**.
2. Click **"Choose what the power buttons do"**.
3. Disable **Fast Startup**.

---

## 🔑 Step 7: Activate Windows (Optional)

1. **Go to Settings → Activation**.
2. Enter a **valid Windows license key**.

For **Windows Server**, use **KMS Activation key**.

---

## 🛠 Step 8: Take a Proxmox Snapshot

1. **Go to Proxmox** → Select **Windows VM**.
2. Click **"Snapshots" → "Take Snapshot"**.
3. Name it **"Fresh Windows Install"**.

> This allows you to **restore Windows to a clean state** if needed.

---

## 🎯 Conclusion: Windows Runs Perfectly on Proxmox!
✅ Installed **Windows with VirtIO drivers**.
✅ Enabled **QEMU Guest Agent for better integration**.
✅ Optimized **storage, network, and CPU settings**.
✅ Windows now runs **smoothly inside Proxmox**!

---


