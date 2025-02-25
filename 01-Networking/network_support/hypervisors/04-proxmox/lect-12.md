# Proxmox Firewall Configuration Guide

## 📌 Introduction
The **Proxmox Firewall** is a built-in security feature that allows you to control network traffic at different levels:

- **Data Center Level** → Rules apply to all nodes in the cluster.
- **Node (Host) Level** → Rules apply to a specific server (host).
- **Container/VM Level** → Rules apply to a specific virtual machine (VM) or container.

> ⚠️ **Warning:** If you enable the firewall without adding rules, it will block all incoming traffic—including SSH and the Web UI—locking you out!

---

## 🔧 Step 1: Understanding the Firewall Layout

Before enabling the firewall, you should understand how Proxmox organizes firewall rules:

- **Datacenter Level:** Affects all nodes in the cluster.
- **Node (Host) Level:** Affects only a single Proxmox server.
- **Container/VM Level:** Affects only a specific virtual machine or container.

---

## 💻 Step 2: Accessing the Proxmox Firewall

1. **Log in to Proxmox Web UI**  
   - Open a web browser and go to:
     ```
     https://<your-proxmox-ip>:8006
     ```
   - Log in with your root credentials.

2. **Navigate to the Firewall Settings**  
   - Click on **Datacenter → Firewall** (for the entire cluster).
   - Click on **Node → Firewall** (for a single server).
   - Click on **VM/Container → Firewall** (for a specific VM).

---

## 🚀 Step 3: Adding Firewall Rules Before Enabling the Firewall

> 🛑 **Do NOT enable the firewall yet!** First, we will add rules to allow essential services.

### 📝 Rule 1: Allow Web Console (Port 8006)

1. Go to **Datacenter → Firewall** (or your node’s firewall).
2. Click **Add Rule**.
3. Select:
   - **Action:** ACCEPT
   - **Direction:** IN
   - **Protocol:** TCP
   - **Destination Port:** `8006`
   - **Comment:** Allow Proxmox Web UI
4. Click **Add** and then **Apply Changes**.

✅ **Web UI will remain accessible when the firewall is enabled.**

### 📝 Rule 2: Allow SSH Access (Port 22)

1. Click **Add Rule**.
2. Select:
   - **Action:** ACCEPT
   - **Direction:** IN
   - **Protocol:** TCP
   - **Destination Port:** `22`
   - **Comment:** Allow SSH access
3. Click **Add** and then **Apply Changes**.

✅ **SSH will remain accessible.**

### 📝 Rule 3: Allow Ping (ICMP)

1. Click **Add Rule**.
2. Select:
   - **Action:** ACCEPT
   - **Direction:** IN
   - **Protocol:** ICMP
   - **Comment:** Allow Ping (ICMP)
3. Click **Add** and then **Apply Changes**.

✅ **Ping will remain working.**

---

## ⚠️ Step 4: Enabling the Firewall (Without Locking Yourself Out!)

Now that essential rules are in place, we can safely enable the firewall.

### Enable Firewall for the Node (Host)

1. Go to **Datacenter → Firewall**.
2. Click on **Options**.
3. Find **Firewall** and set it to **Enabled**.
4. Click **OK**.

✅ **Firewall is now enabled with the rules added!**

---

## 🛠 Step 5: Testing the Firewall

1. **Test Web UI Access**  
   - Open a browser and go to `https://<your-proxmox-ip>:8006`.
   - If it loads, ✅ **Web UI is accessible**.

2. **Test SSH Access**  
   - Open a terminal and run:
     ```
     ssh root@<your-proxmox-ip>
     ```
   - If it connects, ✅ **SSH is accessible**.

3. **Test Ping**  
   - Open a terminal and run:
     ```
     ping <your-proxmox-ip>
     ```
   - If it responds, ✅ **Ping is working**.

---

## 🚑 Step 6: Recovering from a Lockout (If Needed)

If you get locked out (can't access SSH or Web UI), disable the firewall manually:

1. **Access Proxmox via Console**
   - If you have **physical access**, use a keyboard and monitor.
   - If you have **IPMI (remote KVM)**, use it to access the terminal.

2. **Disable the Firewall via CLI**
   ```
   nano /etc/pve/firewall/cluster.fw
   ```
   - Find the line:
     ```
     ENABLE=1
     ```
   - Change it to:
     ```
     ENABLE=0
     ```
   - Save the file and exit (`CTRL + X`, then `Y`, then `ENTER`).

3. **Restart Proxmox Networking**
   ```
   systemctl restart pve-firewall
   ```

✅ **Your firewall is now disabled, and you should regain access!**

---

## 🎯 Step 7: Best Practices

- **Always add essential rules before enabling the firewall.**
- **Restrict SSH access (port 22) to specific IPs** for added security.
- **Regularly check logs** to ensure no unintended blocks.

---

## 🎬 Demo Summary

| **Step** | **Action Taken** | **Result** |
|----------|----------------|------------|
| 1️⃣ | Add Web UI rule (port 8006) | ✅ Web UI remains accessible |
| 2️⃣ | Add SSH rule (port 22) | ✅ SSH remains accessible |
| 3️⃣ | Add Ping rule (ICMP) | ✅ Ping remains working |
| 4️⃣ | Enable Firewall | ✅ Firewall is now active |
| 5️⃣ | Test access | ✅ Everything works as expected |
| 6️⃣ | Recovery (if locked out) | ✅ Disable firewall via CLI |

---

## 🛡️ Conclusion
The **Proxmox Firewall** is a powerful security tool, but misconfiguration can lock you out. By following this guide, you can **safely enable and configure the firewall** while ensuring access to critical services.

