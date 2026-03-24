
# Beginner-Azure-Projects
Welcome to my azure learning repository! 
This repo contais hand-on projects  and practical exercise i've built while learning Microsoft Azure.

# About This Repository
This repository is designed to showcase my journey in Azure Cloud.
Each project focuses on real-world concepts and help me build storng cloud fundamentals.

#  Projects Included
# APP SERVICES 
 What I Built

In this project, I deployed a web application using Azure App Services.
I configured the app to run in a managed environment, enabling easy deployment, scalability, and monitoring without managing infrastructure.
# Challenges Faced
Understanding how App Services works compared to Virtual Machines
Issues during deployment and configuration
Managing application settings and runtime environment
Difficulty in accessing the app due to configuration errors

# How I Resolved
Learned the core concepts of App Services and deployment models
Fixed deployment issues by carefully following step-by-step configuration
Updated application settings and runtime stack properly
Tested and verified the application after each change to ensure it was working correctly# Azure App Services

* Deployed a web application using Azure App Services
* Learned how to host and manage web apps in Azure
* Explored basic configuration and deployment process

 **Project Guide:**
👉 [View Full PDF](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/app%20services%20%20%281%29.pdf)
# Azure Private Link Implementation

**Reference:** [GitHub Project - Private Link PDF](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/private%20link.pdf)

---

# Overview

Implemented **[Azure Private Link](https://docs.microsoft.com/en-us/azure/private-link/)** for secure, private connectivity to Azure services. Created [Virtual Networks](https://docs.microsoft.com/en-us/azure/virtual-network/), [Storage Accounts](https://docs.microsoft.com/en-us/azure/storage/), and [Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) with [Managed Identities](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) for secure authentication.

---

# What Was Implemented

**1. [Virtual Network (VNet)](https://docs.microsoft.com/en-us/azure/virtual-network/)** - Created "india-vnt" with subnet configuration (172.24.0.0/16 CIDR block, subnet-1: 172.24.0.0 - 172.24.255.255)

**2. [Storage Account](https://docs.microsoft.com/en-us/azure/storage/)** - Created "shreyablob" in Central India with blob storage enabled, container "mycont" for data storage

**3. [Private Endpoint](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview)** - Created "storageendpoint" connected to Storage Account blob service, linked to india-vnt subnet

**4. [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/)** - Configured for secure authentication without storing credentials

**5. [RBAC Roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/)** - Assigned appropriate permissions for resource access

**6. [Network Security](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)** - Configured public network access restrictions, disabled from all networks

---

# Challenges & Solutions

**1. Network Configuration Issues**
- Had to properly configure [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) rules for subnet access
- Solution: Added explicit allow rules for private endpoint traffic

**2. Storage Account Public Access**
- Public network access initially enabled for all networks
- Solution: Disabled public access, enforced private endpoint-only connectivity

**3. Private Endpoint Connectivity**
- Challenges with [DNS resolution](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) for private endpoints
- Solution: Configured private endpoint properly in correct subnet and verified connection status

**4. Managed Identity Permissions**
- [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) needed proper role assignments
- Solution: Assigned roles through [RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/) for secure access

**5. CLI Operations**
- Commands like `az storage blob list` were initially blocked by network rules
- Solution: Ensured proper authentication and network configuration


---

# Best Practices Applied

1. Use [Private DNS Zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) for proper name resolution
2. Implement [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) rules for network security
3. Segment [Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) in separate subnets
4. Use [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) over access keys
5. Disable public network access when using [Private Links](https://docs.microsoft.com/en-us/azure/private-link/)
6. Enable monitoring and diagnostics for troubleshooting

---

# Quick Reference

| Component | Resource Name | Status |
|-----------|--------------|--------|
| [Virtual Network](https://docs.microsoft.com/en-us/azure/virtual-network/) | india-vnt | Created |
| [Storage Account](https://docs.microsoft.com/en-us/azure/storage/) | shreyablob | Created |
| [Private Endpoint](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) | storageendpoint | Approved |
| [Container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) | mycont | Created |
| [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) | myidentities | Configured |
| Region | Central India | Active |

---

# Key Learnings

- [Private Link](https://docs.microsoft.com/en-us/azure/private-link/) ensures data stays on Microsoft backbone network
- [Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) require proper [DNS](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) and [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) configuration
- [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) is more secure than access keys
- Public access should be disabled when using private connectivity
- Proper subnet segmentation is crucial for security


# Azure Service Endpoints Project
  
[View Project Documentation](https://raw.githubusercontent.com/shreyatiwari1311-lgtm/Beginner-azure-projects/main/services%20endpoints.pdf)

 Project Documentation:


# What I Built

In this project, I implemented Azure Service Endpoints to establish a secure connection between Azure services and a Virtual Network (VNet).
The goal was to restrict public access and allow communication only through the private Azure backbone network.

# Challenges Faced
Understanding the difference between Service Endpoints and Private Endpoints
Configuring secure access without breaking connectivity
Managing Network Security Group (NSG) rules correctly
Initial misconfiguration of subnet and service access settings
# How I Resolved Them
Studied Azure documentation to clearly understand Service Endpoint behavior
Carefully configured subnets and enabled service endpoints step-by-step
Updated NSG rules to allow only required traffic
Tested connectivity multiple times to ensure secure and proper access


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
