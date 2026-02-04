# 🚀 Day 02 – Create Azure Virtual Machine (Ubuntu 22.04)

## 🎯 Objective
Create an **Azure Virtual Machine** as part of an incremental cloud migration strategy.  
This task focuses on provisioning a Linux VM using **standard Azure configurations** while following **real-world DevOps practices**.

- The Nautilus DevOps team is planning to migrate a portion of their infrastructure to the Azure cloud incrementally. As part of this migration, you are tasked with creating an Azure Virtual Machine (VM).

- The requirements are:

 1) Use the existing resource group.
 2) The VM name must be devops-vm, it should be in westus region.
 3) Use the Ubuntu 22.04 LTS image for the VM.
 4) The VM size must be Standard_B1s.
 5) Attach a default Network Security Group (NSG) that allows inbound SSH (port 22).
 6) Attach a 30 GB storage disk of type Standard HDD.
 7) The rest of the configurations should remain as default.
 8) After completing these steps, make sure you can SSH into the virtual machine.

---

## 🧠 Scenario Overview
The Nautilus DevOps team is migrating infrastructure to Azure in phases.  
As part of this migration, a Linux Virtual Machine must be created with predefined specifications to ensure consistency, security, and cost efficiency.

---

## 🧩 Requirements Summary

- Use the **existing resource group**
- VM name: `devops-vm`
- Region: `westus`
- Image: **Ubuntu 22.04 LTS**
- VM size: **Standard_B1s**
- Network Security Group: Allow inbound **SSH (port 22)**
- OS Disk: **30 GB**, type **Standard HDD**
- All other configurations: **Default**
- Ensure SSH access to the VM after creation

---

## 🛠️ Step-by-Step: Azure Portal (GUI Method)

### Step 1: Login to Azure Portal
- Navigate to https://portal.azure.com
- Sign in using your Azure account

---

### Step 2: Create a Virtual Machine
- Search for **Virtual machines**
- Click **Create** → **Azure virtual machine**

---

### Step 3: Basics Configuration
Fill in the following details:

- **Subscription**: Select your subscription
- **Resource Group**: Select the existing resource group
- **Virtual machine name**: `devops-vm`
- **Region**: `West US`
- **Image**: Ubuntu Server 22.04 LTS
- **Size**: Standard_B1s
- **Authentication type**: SSH public key
- **Username**: azureuser
- **SSH public key source**: Use existing SSH key

Click **Next: Disks**

---

### Step 4: Disks Configuration
- **OS disk size**: 30 GB
- **OS disk type**: Standard HDD
- Leave remaining options as default

Click **Next: Networking**

---

### Step 5: Networking Configuration
- **Virtual network**: Default
- **Subnet**: Default
- **Public IP**: Default
- **NIC network security group**: Basic
- **Public inbound ports**: Allow selected ports
- **Select inbound ports**: SSH (22)

Click **Next** until **Review + Create**

---

### Step 6: Review and Create
- Review all configurations
- Click **Create**
- Wait for deployment to complete

---
✅ Validation Checklist

* Virtual machine devops-vm created successfully
* VM deployed in westus region
* Ubuntu 22.04 LTS image in use
* VM size set to Standard_B1s
* Network Security Group allows inbound SSH on port 22
* OS disk size is 30 GB with Standard HDD
* Successfully connected to the VM using SSH

---

📝 Key Takeaways

* Azure VMs can be provisioned easily using standardized configurations
* Network Security Groups act as Azure’s virtual firewall
* SSH-based authentication is mandatory for secure Linux access
* Disk type and VM size selection directly impact cost and performance
* This process closely aligns with AWS EC2 provisioning concepts

---

## 🔐 SSH into the Virtual Machine

Once deployment is successful:

```bash
ssh -i <private-key.pem> azureuser@<public-ip-address>
