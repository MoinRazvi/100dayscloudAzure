
# 🚀 Day 04 – Create Azure Virtual Network (VNet)

## 🎯 Objective
Create an Azure Virtual Network (VNet) to support the gradual migration of infrastructure workloads into Azure.  

This task introduces the foundational networking component in Azure that enables secure communication between cloud resources.

---

## 🧠 Scenario Overview
The Nautilus DevOps team is migrating infrastructure to Azure in incremental phases.  
As part of the networking setup, a new Virtual Network must be created to host future Azure resources and workloads.

---

## 🧩 Requirements Summary

- Create a Virtual Network named `xfusion-vnet`
- Region: `southcentralus`
- Use any valid IPv4 CIDR block

---

## 🌐 What is a Virtual Network (VNet)?

An Azure Virtual Network (VNet) enables Azure resources to securely communicate with:

- Other Azure resources
- The internet
- On-premises environments
- Other VNets

A VNet is similar to a traditional network in a datacenter but provides Azure-native scalability, isolation, and security.

---

## 🛠️ Step-by-Step: Azure CLI Method

### Step 1: Login to Azure

```bash
az login
````

Verify the active subscription:

```bash
az account show
```

---

### Step 2: Check Available Resource Groups

```bash
az group list --output table
```

Identify the existing resource group to use.

---

### Step 3: Create the Virtual Network

Run the following command:

```bash
az network vnet create \
  --name xfusion-vnet \
  --resource-group <existing-resource-group> \
  --location southcentralus \
  --address-prefix 10.0.0.0/16
```

This command:

* Creates a Virtual Network named `xfusion-vnet`
* Deploys it in `southcentralus`
* Assigns the IPv4 CIDR block `10.0.0.0/16`

---

## 🔍 Verify the Virtual Network

Check whether the VNet was created successfully:

```bash
az network vnet list \
  --query "[].{Name:name, Location:location, AddressSpace:addressSpace.addressPrefixes}" \
  --output table
```

Expected output should include:

```text
Name           Location        AddressSpace
-------------  --------------  ----------------
xfusion-vnet   southcentralus  10.0.0.0/16
```

---

## ✅ Validation Checklist

* Virtual Network `xfusion-vnet` created successfully
* VNet deployed in `southcentralus` region
* IPv4 CIDR block assigned correctly
* Resource visible using Azure CLI

---

## 📝 Key Takeaways

* Virtual Networks are the foundation of Azure networking
* VNets provide isolation and secure communication between Azure resources
* CIDR block planning is important for scalability and future subnetting
* Azure CLI enables efficient infrastructure provisioning without portal access
* Azure VNet concepts are similar to AWS VPC networking

---

## 📌 Day 04 Status

Completed

This task establishes the networking foundation required for deploying and connecting future Azure resources securely within the cloud environment.

---

<img width="1536" height="1024" alt="Devops-4-50" src="https://github.com/user-attachments/assets/232b2eb9-c202-4737-b6c0-d7089e893bd1" />

