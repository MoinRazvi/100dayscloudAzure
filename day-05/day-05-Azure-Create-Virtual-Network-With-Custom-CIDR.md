
# 🚀 Day 05 – Create Azure Virtual Network with Custom CIDR
---

## 🎯 Objective
Create an Azure Virtual Network (VNet) with a custom IPv4 CIDR block to support segmented infrastructure deployment during Azure cloud migration.

This task focuses on foundational Azure networking and proper IP address planning for future workloads.

---

## 🧠 Scenario Overview
The Nautilus DevOps team is migrating workloads to Azure incrementally.  
As part of the networking foundation, separate Virtual Networks are being created for different services and environments.

---

## 🧩 Requirements Summary

- Create a Virtual Network named `nautilus-vnet`
- Region: `southcentralus`
- IPv4 CIDR block: `192.168.0.0/24`

---

# 🛠️ Method 1: Azure Portal (GUI)

## Step 1: Login to Azure Portal
- Navigate to https://portal.azure.com
- Sign in using your Azure account

---

## Step 2: Search for Virtual Networks
- In the top search bar, type **Virtual Networks**
- Click **Virtual Networks**
- Click **+ Create**

---

## Step 3: Configure Basics

Fill in the following details:

- **Subscription**: Select your subscription
- **Resource Group**: Select existing resource group
- **Name**: `nautilus-vnet`
- **Region**: `South Central US`

Click **Next: IP Addresses**

---

## Step 4: Configure IP Address Space

Under IPv4 address space:

```text
192.168.0.0/24
````

Leave default subnet settings unchanged unless specified.

Click **Review + Create**

---

## Step 5: Review and Create

* Verify all configurations
* Click **Create**

Wait for deployment to complete.

---

# 💻 Method 2: Azure CLI

## Step 1: Login to Azure

```bash
az login
```

Verify subscription:

```bash
az account show
```

---

## Step 2: Check Resource Groups

```bash
az group list --output table
```

Identify the existing resource group.

---

## Step 3: Create the Virtual Network

```bash
az network vnet create \
  --name nautilus-vnet \
  --resource-group <existing-resource-group> \
  --location southcentralus \
  --address-prefix 192.168.0.0/24
```

This command:

* Creates VNet `nautilus-vnet`
* Deploys it in `southcentralus`
* Assigns CIDR block `192.168.0.0/24`

---

# 🔍 Verification

## Verify Using Azure CLI

```bash
az network vnet show \
  --name nautilus-vnet \
  --resource-group <existing-resource-group> \
  --query "{Name:name, Location:location, AddressSpace:addressSpace.addressPrefixes}" \
  --output table
```

Expected output:

```text
Name             Location         AddressSpace
---------------  ---------------  ------------------
nautilus-vnet    southcentralus   192.168.0.0/24
```

---

# 🖼️ Architecture Overview

```text
Azure Region: southcentralus
        │
        ▼
+--------------------------+
|     nautilus-vnet        |
|    192.168.0.0/24        |
|                          |
|  Future Azure Resources  |
|  - Virtual Machines      |
|  - Databases             |
|  - Load Balancers        |
|  - Application Services  |
+--------------------------+
```

---

## ✅ Validation Checklist

* Virtual Network `nautilus-vnet` created successfully
* VNet deployed in `southcentralus` region
* IPv4 CIDR block set to `192.168.0.0/24`
* Resource visible in Azure Portal and Azure CLI

---

## 📝 Key Takeaways

* Virtual Networks provide logical isolation in Azure
* CIDR planning is critical for scalable cloud architecture
* Azure VNets are conceptually similar to AWS VPCs
* Smaller CIDR blocks help maintain tighter network segmentation
* GUI and CLI methods both support identical infrastructure provisioning

---

## 📌 Day 05 Status

Completed

This task strengthens Azure networking fundamentals and prepares the infrastructure for future subnet, NSG, and VM deployments.

````
<img width="1536" height="1024" alt="Azure-Cloud-5-50" src="https://github.com/user-attachments/assets/881eb46e-ed73-4678-a822-9323f9dd51ed" />
