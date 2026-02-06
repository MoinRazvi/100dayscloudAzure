# 🚀 Day 03 – Create Azure Virtual Machine Using Azure CLI

## 🎯 Objective
Create an **Azure Virtual Machine using the Azure CLI** as part of an incremental cloud migration.  
This task focuses on **CLI-based resource provisioning**, which is essential when GUI access is unavailable and for automation-driven environments.

---

## 🧠 Scenario Overview
The Nautilus DevOps team is migrating workloads to Azure.  
Due to access restrictions, the team **cannot use the Azure Portal** and must manage resources exclusively via the **azure-client host** using the **Azure CLI**.

---

## 🧩 Requirements Summary

- VM name: `datacenter-vm`
- Image: **Ubuntu 22.04 LTS**
- VM size: **Standard_B2s**
- Admin username: `azureuser`
- SSH authentication: Generate SSH keys
- Storage account type: **Standard_LRS**
- OS disk size: **30 GB**
- Ensure VM is in **running state** after creation

---

## 🛠️ Step-by-Step: Azure CLI Method

### Step 1: Login to Azure
From the `azure-client` host, authenticate using Azure CLI:

```bash
az login
````

Verify the correct subscription:

```bash
az account show
```

---

### Step 2: Create the Virtual Machine

Run the following command to create the VM:

```bash
az vm create \
  --name datacenter-vm \
  --resource-group <existing-resource-group> \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --storage-sku Standard_LRS \
  --os-disk-size-gb 30
```

This command:

* Creates a VM named `datacenter-vm`
* Uses Ubuntu 22.04 LTS
* Sets VM size to Standard_B2s
* Generates SSH keys automatically
* Configures a 30 GB OS disk with Standard_LRS storage

---

### Step 3: Verify VM Status

Check that the VM is running:

```bash
az vm get-instance-view \
  --name datacenter-vm \
  --resource-group <existing-resource-group> \
  --query "instanceView.statuses[?starts_with(code,'PowerState/')].displayStatus" \
  --output table
```

Expected output:

```text
VM running
```

---

## 🔐 SSH into the Virtual Machine

Retrieve the public IP address:

```bash
az vm show \
  --name datacenter-vm \
  --resource-group <existing-resource-group> \
  --show-details \
  --query publicIps \
  --output tsv
```

Connect using SSH:

```bash
ssh azureuser@<public-ip-address>
```

---


## ✅ List All Resource Groups

Run:

```bash
az group list --output table
```

### Example Output

```text
Name                Location    Status
------------------  ----------  --------
myResourceGroup     westus      Succeeded
rg-kodekloud-lab    eastus      Succeeded
```

👉 Use the **Name** column value as your resource group.

---

## ✅ Get Resource Group Only (Clean Output)

If you want **just names**:

```bash
az group list --query "[].name" --output tsv
```

---

## ✅ Check a Specific Resource Group (If You Think You Know It)

```bash
az group show --name <resource-group-name>
```

Example:

```bash
az group show --name rg-kodekloud-lab
```

---

## ✅ Find Which Resource Group an Existing VM Uses (Very Useful)

Since you already created `devops-vm` on Day 02:

```bash
az vm list --query "[].{Name:name, ResourceGroup:resourceGroup}" --output table
```

Example output:

```text
Name        ResourceGroup
----------  -----------------
devops-vm   rg-kodekloud-lab
```

👉 Use **the same resource group** for Day 03 unless the task specifies otherwise.

---

## ✅ Best Practice (Senior Tip 💡)

Before creating any VM, always run:

```bash
az group list --output table
az vm list --output table
```

This avoids:

* Duplicate resource groups
* Wrong region deployments
* Policy failures in lab subscriptions

---

## 🎯 What to Do Next

Once you find the resource group name, run:

```bash
az vm create \
  --name datacenter-vm \
  --resource-group <FOUND_RESOURCE_GROUP> \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --storage-sku Standard_LRS \
  --os-disk-size-gb 30
```

---

## ✅ Validation Checklist

* Azure VM `datacenter-vm` created successfully
* Ubuntu 22.04 LTS image used
* VM size set to Standard_B2s
* Admin username configured as `azureuser`
* SSH keys generated automatically
* OS disk size configured to 30 GB
* Storage account type set to Standard_LRS
* VM is in running state
* Successfully connected to the VM via SSH

---

## 📝 Key Takeaways

* Azure CLI enables full resource management without Portal access
* CLI-based provisioning is ideal for automation and CI/CD pipelines
* SSH key authentication is the default and most secure option
* Disk and VM size selection impacts performance and cost
* Azure CLI workflows closely mirror AWS CLI-based EC2 provisioning

---
