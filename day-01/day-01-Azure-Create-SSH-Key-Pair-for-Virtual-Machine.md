# 🚀 Day 01 – Create SSH Key Pair for Azure Virtual Machine

## 🎯 Objective
Learn how to **create and manage an SSH key pair in Azure** for securely accessing Linux Virtual Machines.  
SSH key–based authentication is a **real-world cloud security best practice** and is preferred over password-based access.

---

## 🔐 Why SSH Key Pairs in Azure?
SSH keys provide:

- 🔒 Stronger security than passwords
- 🚫 Protection against brute-force attacks
- 🤖 Seamless automation for DevOps workflows
- ☁️ Standard authentication method for Azure Linux VMs

---

## 🧩 Components Involved

| Component | Purpose |
|---------|--------|
| SSH Public Key | Stored in Azure / VM |
| SSH Private Key | Stored securely by the user |
| Azure Virtual Machine | Uses SSH key for authentication |
| Azure Portal / Azure CLI | Used to generate or upload SSH keys |

---

## 🛠️ Step-by-Step: Azure Portal (GUI Method)

### 🔹 Step 1: Login to Azure Portal
- Navigate to https://portal.azure.com
- Sign in using your Azure account

---

### 🔹 Step 2: Navigate to SSH Keys
- Use the search bar and type **SSH keys**
- Click on **SSH keys** → **Create**

---

### 🔹 Step 3: Create SSH Key Pair
Provide the following details:

- **Subscription**: Select your subscription
- **Resource Group**: Create new or select existing
- **Region**: Choose nearest Azure region
- **Key pair name**: `azure-day1-key`
- **SSH key source**: Generate new key pair
- **Key type**: RSA
- **Key size**: 2048 or 4096

Click **Review + Create** → **Create**

---

### 🔹 Step 4: Download Private Key
- Download the private key file (`.pem`) when prompted
- Store it securely (⚠️ cannot be downloaded again)

---

## 🧪 Alternative Method: Azure CLI


az sshkey create \
  --name azure-day1-key \
  --resource-group myResourceGroup \
  --location eastus

---
## ✅ Validation Checklist

* SSH key pair created successfully
* Private key downloaded and stored securely
* Public key available in Azure
* SSH key ready to use with Linux Virtual Machines
---
## 📝 Key Takeaways

* SSH keys are the recommended authentication mechanism in Azure
* Password-based access should be avoided in production
* Private keys must never be shared or committed to GitConcepts directly map to AWS EC2 key pairs, easing multi-cloud learning
---
