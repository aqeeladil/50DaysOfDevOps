# Terraform with Proxmox: Automating VM Provisioning

This guide provides a step-by-step tutorial on how to use **Terraform** to automate the creation of virtual machines (VMs) on **Proxmox**. Terraform is an Infrastructure as Code (IaC) tool that allows you to define and provision infrastructure using code. Proxmox is a powerful open-source virtualization platform.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Setting Up Proxmox](#setting-up-proxmox)
3. [Installing Terraform](#installing-terraform)
4. [Configuring Terraform for Proxmox](#configuring-terraform-for-proxmox)
5. [Running Terraform](#running-terraform)
6. [Verifying the VM](#verifying-the-vm)
7. [Cleaning Up](#cleaning-up)
8. [Example Outputs](#example-outputs)

---

## Prerequisites
Before starting, ensure you have the following:
1. **Proxmox Server**:
   - A working Proxmox installation.
   - Access to the Proxmox web interface.
2. **Template in Proxmox**:
   - A VM template (e.g., Debian 12) that Terraform will clone to create new VMs.
3. **Terraform Installed**:
   - Terraform installed on your local machine or a management server.
4. **API Access**:
   - Proxmox API access enabled (default on Proxmox).

---

## Setting Up Proxmox
### 1. Create a Dedicated User
1. Log in to the Proxmox web interface.
2. Go to **Datacenter > Users**.
3. Click **Add** and create a new user (e.g., `terraform`).

### 2. Create a Role with Necessary Permissions
1. Go to **Datacenter > Permissions > Roles**.
2. Create a new role (e.g., `terraform-provision`).
3. Assign the following permissions to the role:
   - **Datastore**: Allocate space, audit.
   - **VM**: Allocate, clone, configure, monitor, power management.

### 3. Create a Group and Assign the Role
1. Go to **Datacenter > Permissions > Groups**.
2. Create a new group (e.g., `terraform`).
3. Assign the `terraform-provision` role to the group.

### 4. Assign the User to the Group
1. Go to **Datacenter > Users**.
2. Edit the `terraform` user and assign it to the `terraform` group.

### 5. Generate an API Token
1. Go to **Datacenter > Users**.
2. Select the `terraform` user and click **Add Token**.
3. Provide a token name (e.g., `terraform-token`) and uncheck **Privilege Separation**.
4. Save the **Token ID** and **Secret Key** securely.

---

## Installing Terraform
1. **Download Terraform**:
   - Visit the [Terraform download page](https://www.terraform.io/downloads.html).
   - Download the appropriate binary for your OS (e.g., Linux amd64).

2. **Install Terraform**:
   ```bash
   unzip terraform_<version>_linux_amd64.zip
   sudo mv terraform /usr/local/bin/
   terraform --version