
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

*Reference Document:** [GitHub Project - Private Link PDF](https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/private%20link.pdf)

# Overview
Implemented **[Azure Private Link](https://docs.microsoft.com/en-us/azure/private-link/private-link-overview)** for secure private connectivity to Azure services with [Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview), [DNS zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview), and [RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview).

---
# Implementation

- **[Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview)** - Configured for [Storage](https://docs.microsoft.com/en-us/azure/storage/), [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/), [SQL Database](https://docs.microsoft.com/en-us/azure/azure-sql/)
- **[Virtual Network](https://docs.microsoft.com/en-us/azure/virtual-network/)** - Multi-subnet architecture with proper [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) rules
- **[Private DNS Zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview)** - Linked to VNet for name resolution
- **[Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/)** - Secure authentication without secrets
- **[Monitoring](https://docs.microsoft.com/en-us/azure/azure-monitor/)** - [Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/) and diagnostics enabled

---

# Challenges & Solutions
#
# **1. DNS Resolution Failures**
**Issue:** Services resolved to public IP instead of private endpoint  
**Solution:** Linked [Private DNS Zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) to [VNet](https://docs.microsoft.com/en-us/azure/virtual-network/) and added A records pointing to private IPs

# **2. NSG Rules Blocking Traffic**
**Issue:** Port 443 outbound traffic was blocked  
**Solution:** Added explicit allow rules in [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) for private endpoint subnet

# **3. Connection Approval Delays**
**Issue:** Manual approval required for each private endpoint connection  
**Solution:** Approved pending connections and automated via [Azure Policy](https://docs.microsoft.com/en-us/azure/governance/policy/)

# **4. On-Premises Connectivity**
**Issue:** On-premises clients couldn't access private endpoints  
**Solution:** Deployed [VPN Gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/) and configured DNS forwarding

# **5. Managed Identity Access Issues**
**Issue:** Applications couldn't authenticate to [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/) through private endpoint  
**Solution:** Assigned **Key Vault Secrets User** [RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview) role to [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/)

# **6. No Visibility into Connection Failures**
**Issue:** Couldn't diagnose connection problems  
**Solution:** Enabled [Diagnostic Settings](https://docs.microsoft.com/en-us/azure/azure-monitor/) and [Network Watcher Flow Logs](https://docs.microsoft.com/en-us/azure/network-watcher/)

---

##  Best Practices

1. Link [Private DNS Zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) to [VNets](https://docs.microsoft.com/en-us/azure/virtual-network/)
2. Configure explicit [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) allow rules
3. Segment [Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) in separate subnets
4. Use [Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) with [RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview)
5. Enable monitoring from day one

---

# Quick Troubleshooting

| Issue | Fix |
|-------|-----|
| DNS not resolving | Link [Private DNS Zone](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) to [VNet](https://docs.microsoft.com/en-us/azure/virtual-network/) |
| Connection refused | Add [NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) allow rule for port 443 |
| Pending approval | Approve in [Azure resource](https://azure.microsoft.com/en-us/services/) |
| Auth fails | Assign [RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview) roles |

---

# Key Terms

- **[Private Link](https://docs.microsoft.com/en-us/azure/private-link/)** - Private connectivity to Azure services
- **[Private Endpoint](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview)** - Private network interface to Azure service
- **[Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/)** - Credential-less authentication
- **[NSG](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)** - Network firewall rules
-
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
