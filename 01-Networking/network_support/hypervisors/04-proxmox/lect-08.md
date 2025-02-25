# Proxmox LXC Container Setup with Apache Web Server

## 🛠 Prerequisites
- A running **Proxmox VE** (Virtual Environment) instance.
- Access to the Proxmox Web UI.
- Basic familiarity with Linux commands.

---

## 1️⃣ Download LXC Template

1. **Open Proxmox Web UI:**  
   Navigate to your Proxmox server’s web interface:  
   `https://<your-proxmox-ip>:8006`

2. **Go to Storage:**  
   - In the left sidebar, click your Proxmox node (like `proxmox01`).
   - Under **"local (proxmox01)"**, click **"CT Templates"**.

3. **Download an OS Template:**  
   - Click **"Templates"** at the top.
   - Find and select **"ubuntu-20.04-standard"** or **"ubuntu-22.04-standard"**.
   - Click **Download** and wait for it to finish.

---

## 2️⃣ Create the LXC Container

1. **Click "Create CT":**  
   In the top right of the Proxmox interface, click **"Create CT"**.

2. **Set Basic Details:**  
   - **Hostname:** `web-server-ct`  
   - **Password:** Set a root password.  
   - **(Optional) SSH Key:** Paste your public SSH key here if you want SSH access.

3. **Select Template:**  
   - Choose the **Ubuntu 20.04** or **Ubuntu 22.04** template you downloaded earlier.

4. **Set Storage and Disk Size:**  
   - **Storage:** `local-lvm` (or whichever storage you prefer).  
   - **Disk Size:** 16GB (or more if needed).

5. **CPU and Memory:**  
   - **Cores:** `1` (or more if required).  
   - **RAM:** `1024MB` (1GB) is good for web servers.

6. **Network Configuration:**  
   - **Bridge:** `vmbr0` (usually the default network bridge).  
   - **IP Address:** `DHCP` (Proxmox will assign an IP automatically).  
   - **MAC Address:** Leave on auto.  
   - **DNS Settings:** Use **host settings**.

7. **Finish Setup:**  
   Click **Finish** and wait for the container to be created.

---

## 3️⃣ Start and Access the LXC Container

1. **Start the Container:**  
   - Right-click your container (`web-server-ct`).
   - Click **Start**.

2. **Open Console:**  
   - Right-click the container again and choose **Console**.
   - Log in as `root` with the password you set earlier.

3. **Check IP Address:**  
   Once inside the console, run:  
   ```bash
   ip a
   ```
   Note the IP address — you’ll use this to access the server.

---

## 4️⃣ Update and Install Apache Web Server

1. **Update Package Lists:**  
   ```bash
   apt update
   ```

2. **Install Apache:**  
   ```bash
   apt install apache2 -y
   ```

3. **Start Apache:**  
   ```bash
   systemctl start apache2
   ```

4. **Enable Apache on Boot:**  
   ```bash
   systemctl enable apache2
   ```

---

## 5️⃣ Test Apache from Browser

1. Open a browser and enter the IP address of the container:  
   ```
   http://<container-ip>
   ```

2. You should see the default **Apache2 Ubuntu Default Page** — this means Apache is running successfully!

---

## 6️⃣ (Optional) Enable SSH Access

1. **Create a New User:**  
   ```bash
   adduser deployuser
   ```

2. **Add User to sudo Group:**  
   ```bash
   usermod -aG sudo deployuser
   ```

3. **Enable SSH Access:**  
   By default, Proxmox LXC containers **disable root SSH login** for security. Let’s enable it for your new user:

   Open the SSH config file:  
   ```bash
   nano /etc/ssh/sshd_config
   ```

   Find and modify these lines:  
   ```
   PermitRootLogin no
   PasswordAuthentication yes
   ```

4. **Restart SSH Service:**  
   ```bash
   systemctl restart ssh
   ```

5. **SSH into the Container:**  
   From your local machine:  
   ```bash
   ssh deployuser@<container-ip>
   ```

---

## 7️⃣ (Optional) Make the Container Auto-Start

1. Right-click your container and choose **"Options"**.
2. Click **"Start at boot"** and set it to **Yes**.

---

## 📝 Summary

- We set up an LXC container on Proxmox using an **Ubuntu 20.04 template**.
- Installed and started **Apache Web Server**.
- Accessed the default Apache page through the container’s IP address.
- (Optional) Enabled **SSH access** with a non-root user.
- Configured the container to **auto-start on boot**.

---

## 📦 Why LXC Containers?

- **Lightweight:** Faster and uses fewer resources than VMs.
- **Persistent:** Unlike Docker, LXC containers retain state after stopping.
- **Flexible:** Great for running full Linux environments with isolated processes.

