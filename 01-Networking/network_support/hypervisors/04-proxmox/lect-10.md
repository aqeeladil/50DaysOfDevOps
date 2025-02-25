# Proxmox User Management - Complete Guide with Demo

## 🛠 Prerequisites
Make sure you have:
- A **Proxmox VE** server up and running.
- Access to the **Proxmox web interface**.
- **Shell/Terminal access** to the Proxmox server.

---

## 👤 1. PAM Users (Linux System Users)

**What is a PAM User?**
- A **Linux system user** — exists at the OS level.
- Can **SSH into the Proxmox server**.
- **Doesn’t automatically have permissions** in Proxmox until assigned.

### 📝 Create a PAM User
1. **Create a PAM user in the Proxmox UI:**
   - Go to **Datacenter → Users → Add**
   - **Username:** `john`
   - **Realm:** `PAM (Linux system authentication)`
   - **Click Add**

2. **Verify the PAM user in the Linux system:**
```bash
cat /etc/passwd | grep john
```

3. **Add the PAM user to the Linux system:**
```bash
sudo adduser john
sudo passwd john
```

4. **Confirm the user exists on the system:**
```bash
cat /etc/passwd | grep john
```

5. **Test SSH access:**
```bash
ssh john@<proxmox-ip>
```

---

## 👤 2. PVE Users (Proxmox VE Users)

**What is a PVE User?**
- A **Proxmox-only user**, exists **only within the Proxmox UI**.
- **CANNOT SSH** into the server.
- **Only used for web interface access**.

### 📝 Create a PVE User
1. **Create a PVE user in the Proxmox UI:**
   - Go to **Datacenter → Users → Add**
   - **Username:** `mary`
   - **Realm:** `Proxmox VE authentication server (PVE)`
   - **Password:** Set a password for the user
   - **Click Add**

2. **Confirm the PVE user in the Proxmox UI:**
   - Go to **Datacenter → Users**, and you’ll see `mary` listed.

---

## 👥 3. Creating and Managing Groups

**Why use Groups?**
- To **assign permissions more easily** across multiple users.
- Users in a group **inherit the group’s permissions**.

### 📝 Create a Group
1. **Create a new group:**
   - Go to **Datacenter → Groups → Create**
   - **Group Name:** `admins`
   - **Click Add**

2. **Assign users to the group:**
   - Go to **Datacenter → Users**
   - Select user `john`, click **Edit**, and choose **Group: admins**
   - Repeat the same for `mary`

---

## 🔑 4. Assigning Permissions

**Permissions control what users or groups can access and manage.**

| Role          | Permissions              |
|---------------|-------------------------|
| Administrator | Full access              |
| PVEVMAdmin    | Manage virtual machines  |
| PVEAdmin      | Manage everything except users & permissions |

### 📝 Assign Group Permissions
1. **Assign permissions to the group:**
   - Go to **Datacenter → Permissions → Add → Group Permission**
   - **Path:** `/` (root, for full access)
   - **Group:** `admins`
   - **Role:** `Administrator`
   - **Click Add**

---

## 🧑‍💻 5. Testing Access

Let’s confirm everything works! 🚀

1. **Test `john`'s SSH access:**
```bash
ssh john@<proxmox-ip>
```
✅ You should be able to SSH successfully because `john` is a PAM user.

2. **Test `john`'s Proxmox GUI access:**
   - Go to the **Proxmox Web UI**
   - Log in with:
     - **Username:** `john`
     - **Realm:** `PAM`
   - You should see full admin access.

3. **Test `mary`'s Proxmox GUI access:**
   - Go to the **Proxmox Web UI**
   - Log in with:
     - **Username:** `mary`
     - **Realm:** `PVE`
   - You should see full admin access.

4. **Test `mary`'s SSH access:**
```bash
ssh mary@<proxmox-ip>
```
❌ This **won’t work** because `mary` is a PVE user and only exists within the Proxmox UI.

---

## ✅ Summary of Results

| Feature         | PAM User (`john`) | PVE User (`mary`) |
|-----------------|------------------|------------------|
| SSH Access      | ✅ Yes            | ❌ No             |
| Web UI Access   | ✅ Yes            | ✅ Yes            |
| Linux System User | ✅ Yes          | ❌ No             |
| Group Permissions | ✅ Inherited   | ✅ Inherited      |

---



