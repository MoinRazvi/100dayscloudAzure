## 🎯 Objective
Create a Public IP Address resource in Azure to enable external connectivity for Azure resources such as Virtual Machines, Load Balancers, and Application Gateways.

This task introduces Azure Public IP resources, which are essential for internet-facing communication.

---

## 🧠 Scenario Overview
The Nautilus DevOps team is migrating workloads to Azure incrementally.  
As part of the infrastructure setup, a Public IP Address resource must be provisioned to support external access for future Azure services.

---

## 🧩 Requirements Summary

- Allocate a Public IP Address
- Public IP name: `nautilus-pip`

---

# 🛠️ Method 1: Azure Portal (GUI)

## Step 1: Login to Azure Portal
- Navigate to https://portal.azure.com
- Sign in using your Azure account

---

## Step 2: Search for Public IP Addresses
- In the top search bar, type **Public IP addresses**
- Click **Public IP addresses**
- Click **+ Create**

---

## Step 3: Configure Basics

Fill in the following details:

- **Subscription**: Select your subscription
- **Resource Group**: Select the existing resource group
- **Region**: Select the required region
- **Name**: `nautilus-pip`
- **IP Version**: IPv4
- **SKU**: Basic
- **Assignment**: Dynamic

Leave the remaining settings as default.

Click **Review + Create**

---

## Step 4: Review and Create
- Verify all configurations
- Click **Create**

Wait for deployment to complete.

---

# 💻 Method 2: Azure CLI

## Step 1: Login to Azure

```bash
az login
````

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

## Step 3: Create the Public IP Address

```bash
az network public-ip create \
  --name nautilus-pip \
  --resource-group <existing-resource-group> \
  --sku Basic \
  --allocation-method Dynamic
```

This command:

* Creates a Public IP named `nautilus-pip`
* Uses IPv4
* Assigns a dynamic public IP address

---

# 🔍 Verification

## Verify Public IP Resource

```bash
az network public-ip show \
  --name nautilus-pip \
  --resource-group <existing-resource-group> \
  --query "{Name:name, IPAddress:ipAddress, ProvisioningState:provisioningState}" \
  --output table
```

Expected output:

```text
Name           IPAddress      ProvisioningState
-------------  -------------  -----------------
nautilus-pip   20.x.x.x       Succeeded
```

---

# 🖼️ Architecture Overview

```text
                Internet
                    │
                    ▼
          +------------------+
          |   Public IP      |
          |  nautilus-pip    |
          +------------------+
                    │
                    ▼
          +------------------+
          | Azure Resources  |
          | - Virtual VM     |
          | - Load Balancer  |
          | - App Gateway    |
          +------------------+
```

---

## ✅ Validation Checklist

* Public IP resource `nautilus-pip` created successfully
* Public IP assigned successfully
* Resource visible in Azure Portal
* Resource verified using Azure CLI
* Provisioning state shows `Succeeded`

---

## 📝 Key Takeaways

* Public IP addresses enable internet connectivity for Azure resources
* Azure supports Dynamic and Static public IP allocation
* Public IPs are commonly attached to VMs, Load Balancers, and Gateways
* Azure networking components are similar to AWS Elastic IP concepts
* Proper public IP management is important for security and cost optimization

---
