
# 🚀 Day 09 - Attach Azure Network Interface (NIC) to Virtual Machine

## 🎯 Objective
Attach an existing Network Interface Card (NIC) to an existing Azure Virtual Machine.

This task introduces Azure network interface management, which is essential for advanced networking, traffic segregation, and multi-network communication in cloud environments.

---

## 🧠 Scenario Overview
The Datacenter DevOps team is migrating workloads to Azure incrementally.  
To improve network management and connectivity, an existing network interface must be attached to an existing virtual machine.

---

## 🧩 Requirements Summary

- Existing VM: `datacenter-vm`
- Existing NIC: `datacenter-nic`
- Region: `eastus`
- Attach `datacenter-nic` to `datacenter-vm`
- Ensure NIC status becomes attached
- Ensure VM initialization is completed before submission

---

# 🛠️ Method 1: Azure Portal (GUI)

## Step 1: Login to Azure Portal
- Navigate to https://portal.azure.com
- Sign in using your Azure account

---

## Step 2: Stop the Virtual Machine
Azure requires the VM to be stopped before attaching an additional NIC.

- Search for **Virtual Machines**
- Select `datacenter-vm`
- Click **Stop**

Wait until VM status changes to:

```text
Stopped (deallocated)
````

---

## Step 3: Open Networking Section

* Inside `datacenter-vm`
* Click **Networking**
* Navigate to **Network settings**
* Under **Network interfaces**, click **Attach network interface**

---

## Step 4: Attach Existing NIC

Select:

* **Network interface**: `datacenter-nic`

Click **OK** or **Attach**

---

## Step 5: Start the Virtual Machine

* Go back to VM Overview
* Click **Start**

Wait for VM initialization to complete.

---

## Step 6: Verify NIC Attachment

* Navigate to:

  * VM → Networking
* Verify `datacenter-nic` appears under attached network interfaces

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

Identify the resource group containing:

* `datacenter-vm`
* `datacenter-nic`

---

## Step 3: Stop the Virtual Machine

```bash
az vm deallocate \
  --name datacenter-vm \
  --resource-group <existing-resource-group>
```

Wait for VM to stop completely.

---

## Step 4: Attach Existing NIC

```bash
az vm nic add \
  --vm-name datacenter-vm \
  --nics datacenter-nic \
  --resource-group <existing-resource-group>
```

This command:

* Attaches NIC `datacenter-nic`
* Associates it with VM `datacenter-vm`

---

## Step 5: Start the Virtual Machine

```bash
az vm start \
  --name datacenter-vm \
  --resource-group <existing-resource-group>
```

Wait for VM initialization to complete.

---

# 🔍 Verification

## Verify Attached NICs

```bash
az vm nic list \
  --vm-name datacenter-vm \
  --resource-group <existing-resource-group> \
  --output table
```

Expected output should include:

```text
datacenter-nic
```

---

## Verify VM Running State

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

# 🖼️ Architecture Overview

```text
                +------------------------+
                |     datacenter-vm      |
                |    Azure Virtual VM    |
                +-----------+------------+
                            │
          ---------------------------------------
          │                                     │
          ▼                                     ▼
+-------------------+               +-------------------+
| Primary NIC       |               | datacenter-nic    |
| Existing Adapter  |               | Attached NIC      |
+-------------------+               +-------------------+
```

---

## ✅ Validation Checklist

* Network interface `datacenter-nic` attached successfully
* NIC attached to VM `datacenter-vm`
* NIC status shows attached
* VM initialization completed successfully
* VM returned to running state after NIC attachment
* Resource verified using Azure Portal and Azure CLI

---

## 📝 Key Takeaways

* Azure VMs can have multiple network interfaces attached
* Additional NICs help separate traffic and improve network design
* Azure requires VM deallocation before attaching secondary NICs
* NIC management is important for enterprise networking architectures
* Azure NIC concepts are similar to AWS Elastic Network Interfaces (ENI)

---
