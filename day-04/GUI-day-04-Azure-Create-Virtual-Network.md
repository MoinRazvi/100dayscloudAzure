
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

A VNet is similar to a traditional datacenter network but provides Azure-native scalability, isolation, and security.

---

# 🛠️ Step-by-Step: Azure Portal (GUI Method)

## Step 1: Login to Azure Portal
- Navigate to https://portal.azure.com
- Sign in using your Azure account

---

## Step 2: Search for Virtual Networks
- In the top search bar, type **Virtual Networks**
- Click on **Virtual Networks**
- Click **+ Create**

---

## Step 3: Configure Basics

Fill in the following details:

- **Subscription**: Select your subscription
- **Resource Group**: Select the existing resource group
- **Name**: `xfusion-vnet`
- **Region**: `South Central US`

Click **Next: IP Addresses**

---

## Step 4: Configure IP Address Space

Under IPv4 address space:

- Add address space:
  
```text
10.0.0.0/16
````

Leave the default subnet settings as-is or remove if not needed.

Click **Review + Create**

---

## Step 5: Review and Create

* Verify all configurations
* Click **Create**

Wait for deployment completion.

---

## 🔍 Verify the Virtual Network

After deployment:

* Navigate to **Virtual Networks**
* Verify `xfusion-vnet` appears in the list
* Confirm:

  * Region = `southcentralus`
  * Address space = `10.0.0.0/16`

---

## ✅ Validation Checklist

* Virtual Network `xfusion-vnet` created successfully
* VNet deployed in `southcentralus` region
* IPv4 CIDR block assigned correctly
* Resource visible in Azure Portal

---

## 📝 Key Takeaways

* Virtual Networks are the foundation of Azure networking
* VNets provide isolation and secure communication between Azure resources
* CIDR block planning is important for scalability and future subnetting
* Azure networking concepts are similar to AWS VPC networking
* Proper network design is critical for cloud infrastructure deployments

---

