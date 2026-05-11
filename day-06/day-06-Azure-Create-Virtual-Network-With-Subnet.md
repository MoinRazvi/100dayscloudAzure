
## 🎯 Objective
Create an Azure Virtual Network (VNet) along with a subnet to establish the foundational networking layer for Azure workloads.

This task introduces subnetting within Azure VNets, which is essential for organizing and isolating cloud resources.

---

## 🧠 Scenario Overview
The Nautilus DevOps team is migrating workloads to Azure incrementally.  
As part of the networking setup, a Virtual Network and subnet are required to host future Azure resources securely and efficiently.

---

## 🧩 Requirements Summary

- Create a Virtual Network named `xfusion-vnet`
- Create a subnet named `xfusion-subnet`
- Region: `centralus`
- IPv4 CIDR block: `10.0.0.0/16`

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
- **Resource Group**: Select the existing resource group
- **Name**: `xfusion-vnet`
- **Region**: `Central US`

Click **Next: IP Addresses**

---

## Step 4: Configure IP Address Space

Under IPv4 address space:

```text
10.0.0.0/16
````

---

## Step 5: Configure Subnet

Under Subnets:

* **Subnet name**: `xfusion-subnet`
* **Subnet address range**:

```text
10.0.0.0/24
```

Click **Add**

Then click **Review + Create**

---

## Step 6: Review and Create

* Verify all configurations
* Click **Create**

Wait for deployment completion.

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

## Step 3: Create the Virtual Network and Subnet

```bash
az network vnet create \
  --name xfusion-vnet \
  --resource-group <existing-resource-group> \
  --location centralus \
  --address-prefix 10.0.0.0/16 \
  --subnet-name xfusion-subnet \
  --subnet-prefix 10.0.0.0/24
```

This command:

* Creates VNet `xfusion-vnet`
* Creates subnet `xfusion-subnet`
* Deploys resources in `centralus`
* Assigns IPv4 CIDR block `10.0.0.0/16`

---

# 🔍 Verification

## Verify Virtual Network

```bash
az network vnet show \
  --name xfusion-vnet \
  --resource-group <existing-resource-group> \
  --output table
```

---

## Verify Subnet

```bash
az network vnet subnet list \
  --vnet-name xfusion-vnet \
  --resource-group <existing-resource-group> \
  --output table
```

Expected subnet output:

```text
Name             AddressPrefix
---------------  ---------------
xfusion-subnet   10.0.0.0/24
```

---

# 🖼️ Architecture Overview

```text
Azure Region: centralus
        │
        ▼
+-----------------------------------+
|          xfusion-vnet             |
|           10.0.0.0/16             |
|                                   |
|   +---------------------------+   |
|   |      xfusion-subnet       |   |
|   |        10.0.0.0/24        |   |
|   |                           |   |
|   |  Future Azure Resources   |   |
|   |  - Virtual Machines       |   |
|   |  - Databases              |   |
|   |  - App Services           |   |
|   +---------------------------+   |
+-----------------------------------+
```

---

## ✅ Validation Checklist

* Virtual Network `xfusion-vnet` created successfully
* Subnet `xfusion-subnet` created successfully
* Resources deployed in `centralus` region
* IPv4 CIDR block configured as `10.0.0.0/16`
* Subnet address range configured correctly
* Resources visible in Azure Portal and Azure CLI

---

## 📝 Key Takeaways

* Subnets divide VNets into smaller logical network segments
* Proper subnetting improves scalability and security
* Azure VNets and subnets are conceptually similar to AWS VPCs and subnets
* Azure CLI enables fast and repeatable infrastructure provisioning
* Network planning is critical before deploying production workloads

---

