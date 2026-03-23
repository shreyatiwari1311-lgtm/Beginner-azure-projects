
# Beginner-Azure-Projects
Welcome to my azure learning repository! 
This repo contais hand-on projects  and practical exercise i've built while learning Microsoft Azure.

# About This Repository
This repository is designed to showcase my journey in Azure Cloud.
Each project focuses on real-world concepts and help me build storng cloud fundamentals.

#  Projects Included
# APP SERVICES 


#  1. Azure App Services

* Deployed a web application using Azure App Services
* Learned how to host and manage web apps in Azure
* Explored basic configuration and deployment process

 **Project Guide:**
👉 [View Full PDF](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/app%20services%20%20%281%29.pdf)
#  Azure Service Endpoints Project

##  Project Overview

This project demonstrates how to securely connect Azure resources using **Azure Service Endpoints**, ensuring that traffic flows through the **Azure backbone network** instead of the public internet.

It highlights how to **restrict access to Azure services** (like Storage Accounts) and allow communication only from a specific **Virtual Network (VNet)**.

---

##  Project Objective

* Implement **Azure Service Endpoints**
* Secure critical Azure resources
* Restrict public access to services
* Enable **VNet-based access control**

---

##  Azure Services Used

*  [Azure Virtual Network (VNet)](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview)
*  [Subnet](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-subnet)
*  [Azure Storage Account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-overview)
*  [Service Endpoints](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview)

---

##  Detailed Documentation

 **Step-by-step implementation guide:**
👉 [View Full Project PDF](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/services%20endpoints.pdf)

---

##  Implementation Steps

1. Created an **Azure Virtual Network (VNet)**
2. Added a **Subnet** within the VNet
3. Enabled **Service Endpoints** on the subnet
4. Created an **Azure Storage Account**
5. Configured **network restrictions** on the storage account
6. Allowed access only from the selected **VNet/Subnet**
7. Validated secure access and blocked public traffic

---

##  Key Concept Explained

**Azure Service Endpoints** extend your VNet identity to Azure services.

✔ Traffic remains within the **Microsoft Azure network**
✔ Eliminates exposure to the **public internet**
✔ Enhances **data security and access control**

---

## Project Outcome

* Secured Azure Storage using **Service Endpoints**
* Successfully restricted unauthorized/public access
* Ensured **private and secure communication** between Azure resources

---

##  Real-World Use Cases

* Secure **backend application services**
* Restrict access to **databases and storage accounts**
* Implement **enterprise-grade network security**

---

##  Author

**Shreya Tiwari**
🔗 [Visit My GitHub Profile](https://github.com/shreyatiwari1311-lgtm)

---

# VNET TO VNET PEERING
#  1. VNet to VNet Peering

* Created two Virtual Networks
* Connected them using **VNet Peering**
* Tested communication between networks

 **Project Guide:**
👉 [View Full PDF](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/vnet%20to%20vnet%20peering%20.pdf)

#  Azure VNet to VNet Peering Project

# Overview

This project demonstrates how to create **VNet to VNet Peering** in Microsoft Azure.
VNet peering allows two virtual networks to communicate with each other securely using Azure's backbone network.

---

# Objective

* Understand Azure Virtual Networks (VNet)
* Configure VNet Peering between two VNets
* Enable communication between resources in different networks

---

# Services Used

* Azure Virtual Network
* Subnets
* Network Security Groups (NSG)
* Azure Portal

---

# Architecture

* VNet-1 (Region A)
* VNet-2 (Region B or same region)
* Peering connection between both VNets

---

# Step-by-Step Implementation

# Step 1: Create VNet-1

* Go to Azure Portal
* Create a Virtual Network
* Add address space (e.g., 10.0.0.0/16)
* Create subnet (e.g., 10.0.1.0/24)

# Step 2: Create VNet-2

* Create another VNet
* Use different address space (e.g., 10.1.0.0/16)
* Add subnet

# Step 3: Configure VNet Peering

* Go to VNet-1 → Peerings → Add

* Connect to VNet-2

* Enable:

  * Allow virtual network access
  * Allow forwarded traffic (optional)

* Repeat same from VNet-2

# Step 4: Verify Connection

* Deploy VM in both VNets
* Try ping or SSH/RDP between them

---
# Documentation

👉 [View Full PDF Guide](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/vnet%20to%20vnet%20peering%20.pdf)

---

# Key Learnings

* VNet peering is fast and private
* No need for VPN gateway
* Works across regions

---

# Author

Shreya Tiwari
Beginner in Azure & Cloud ☁️
