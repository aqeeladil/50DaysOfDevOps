# Linux User Management

## 1. Check Existing Users
**Command:**
```bash
cat /etc/passwd
```
**Explanation:**  
- The `/etc/passwd` file contains user account information.
- Each line represents a user, showing details like username, UID, GID, home directory, and shell.

To list only usernames:
```bash
cut -d: -f1 /etc/passwd
```

---

## 2. View User Information
**Command:**
```bash
id testuser
```
**Explanation:**  
- Displays the user’s UID (User ID), GID (Group ID), and group memberships.

Alternative:
```bash
getent passwd testuser
```
- Retrieves full user details from `/etc/passwd`.

---

## 3. Create a New User
**Command:**
```bash
sudo useradd -m -s /bin/bash testuser
sudo passwd testuser
```
**Explanation:**  
- `-m`: Creates a home directory (`/home/testuser`).
- `-s /bin/bash`: Sets the default shell to Bash.
- `passwd`: Sets the user’s password.

---

## 4. Modify User Information
**Command:**
```bash
sudo usermod -l newuser testuser
```
**Considerations:**  
- This only changes the username.
- Update the home directory if necessary:
  ```bash
  sudo usermod -d /home/newuser -m newuser
  ```

---

## 5. Delete a User
**Command:**
```bash
sudo userdel -r newuser
```
**Explanation:**  
- `-r`: Removes the user’s home directory and mail spool.
- Without `-r`, the home directory remains intact.

---

## 6. Check User Groups
**Command:**
```bash
groups testuser
```
or
```bash
id -Gn testuser
```
**Explanation:**  
- Lists all groups the user belongs to.

---

## 7. Add User to a Group
**Command:**
```bash
sudo usermod -aG developers testuser
```
**Explanation:**  
- `-aG`: Adds (`a`) the user to the group (`G`).

---

## 8. Set User Permissions
**Command:**
```bash
sudo chown root:root /data
sudo chmod 700 /data
```
**Explanation:**  
- `chown root:root /data`: Sets root as the owner.
- `chmod 700 /data`: Grants full permissions to root, denying access to others.

---

## 9. Restrict User to a Single Directory
**Commands:**
```bash
sudo chroot /home/testuser
```
or  
Using a restricted shell:
```bash
sudo usermod -s /usr/sbin/nologin testuser
```
**Explanation:**  
- `chroot`: Restricts the user to `/home/testuser` (requires proper setup).
- `usermod -s /usr/sbin/nologin`: Prevents direct shell access.

---

## 10. Manage Password Policies
**Command:**
```bash
sudo chage -M 90 testuser
```
**Explanation:**  
- `-M 90`: Sets a password expiry of 90 days.

Alternative: Edit `/etc/login.defs`  
```bash
PASS_MAX_DAYS 90
```

---

## 11. List All User Accounts
**Command:**
```bash
awk -F: '{print $1, $6, $7}' /etc/passwd
```
**Explanation:**  
- Extracts the username, home directory, and shell from `/etc/passwd`.

---

## 12. Lock and Unlock a User Account
**Commands:**
```bash
sudo passwd -l testuser  # Lock
sudo passwd -u testuser  # Unlock
```
**Explanation:**  
- Locking prevents login but doesn’t delete the account.

---

## 13. Check Last Login Information
**Command:**
```bash
lastlog
```
**Explanation:**  
- Displays last login details of all users.

---

## 14. Set Up User Quotas
**Commands:**
1. Enable quotas:
   ```bash
   sudo apt install quota
   ```
2. Edit `/etc/fstab` and enable quotas:
   ```
   /dev/sda1 /home ext4 defaults,usrquota,grpquota 0 1
   ```
3. Create quota files:
   ```bash
   sudo mount -o remount /home
   sudo quotacheck -cum /home
   sudo quotaon /home
   ```
4. Set quota for `testuser`:
   ```bash
   sudo edquota -u testuser
   ```
   - Set the hard limit to **1GB**.

---

## 15. Create a User with Specific Shell
**Command:**
```bash
sudo useradd -m -s /bin/bash shelluser
```
**Explanation:**  
- `-s /bin/bash`: Sets Bash as the default shell.

---

Would you like any additional details on these commands? 🚀

