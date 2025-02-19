# Package Management in Debian-based Systems

## 1. Basic Usage
### Install `curl`
```bash
sudo apt install curl
```

### Remove `vim` while preserving configuration files
```bash
sudo apt-get remove vim
```

---

## 2. Upgrading Packages
### Upgrade all installed packages
```bash
sudo apt update
sudo apt upgrade -y
```

### Difference between `apt upgrade` and `apt full-upgrade`
- `apt upgrade`: Upgrades installed packages **without** removing existing ones.
- `apt full-upgrade`: Upgrades packages but **may remove packages** if necessary.

#### Example Usage:
- Use `apt upgrade` for regular updates.
- Use `apt full-upgrade` when upgrading to a new OS version.

---

## 3. Searching for Packages
### Search for packages related to `git`
```bash
apt search git
```

### Check if `python3` is installed
```bash
apt list --installed | grep python3
```
Or:
```bash
dpkg -l | grep python3
```

---

## 4. Managing Package Configuration
### Difference between `apt remove` and `apt purge`
- `apt remove`: Removes the package but keeps configuration files.
- `apt purge`: Removes the package **and** its configuration files.

### Clean up unused dependencies
```bash
sudo apt autoremove
```

---

## 5. Updating Repositories
### Refresh package index
```bash
sudo apt update
```
### Why is this important?
It ensures the latest package versions are available and avoids outdated package errors.

---

## 6. Detailed Package Information
### Show details about `git`
```bash
apt show git
```

### Verify installation and check version
```bash
dpkg -l | grep git
```
Or:
```bash
git --version
```

---

## 7. Combining Commands
### Update, upgrade all packages, and remove unused dependencies
```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

### Install a package with recommended dependencies only
```bash
sudo apt install --install-recommends package-name
```

### Ignore unnecessary dependencies
```bash
sudo apt install --no-install-recommends package-name
```

---

## 8. Practical Scenario: Installing `nginx`
### Installation Steps
```bash
sudo apt update
sudo apt install nginx -y
```

### Start and Enable the Service
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Check the Status
```bash
sudo systemctl status nginx
```

### Fix Broken Packages
```bash
sudo apt --fix-broken install
```

---

## 9. Conflict Resolution
### Resolve Dependency Conflict
```bash
sudo apt install libdependency=2.0 libexample
```

### Check if Upgrading Affects Other Packages
```bash
apt show libdependency
apt depends libdependency
```

---

## 10. Package Source Management
### Add a New Repository
```bash
sudo add-apt-repository ppa:repository-name
sudo apt update
```

### Manually Add a Repository
```bash
echo "deb http://repository-url $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/custom-repo.list
sudo apt update
```

### Ensure Repository is Trusted
```bash
wget -qO - https://repository-url/key.gpg | sudo apt-key add -
```

### Check if the Package is Available
```bash
apt-cache search package-name
```

---
