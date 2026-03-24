
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
# Azure Private Link Implementation Guide

# Overview
This document outlines the implementation of **[Azure Private Link](https://docs.microsoft.com/en-us/azure/private-link/private-link-overview)** for secure, private connectivity to Azure services. It covers what was implemented, challenges encountered, and how each challenge was resolved.

---

# What I Implemented

### 1. **[Private Endpoint](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) Setup**
- Created [Private Endpoints](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview) for Azure services ([Storage Account](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview), [SQL Database](https://docs.microsoft.com/en-us/azure/azure-sql/database/sql-database-paas-overview), [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/overview))
- Configured endpoint connections in a virtual network ([VNet](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview))
- Established [private DNS zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview) for name resolution

# 2. **Network Architecture**
- Deployed [Virtual Network](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview) with multiple subnets
- Created Private Endpoint subnet with proper [Network Security Group (NSG)](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) rules
- Implemented [network policies](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview) to restrict traffic

# 3. **DNS Configuration**
- Set up Private DNS Zones for Azure services
- Configured DNS records to resolve service names to private IPs
- Linked DNS zones to virtual networks

# 4. **Access Control**
- Configured Azure Key Vault private endpoints
- Implemented Managed Identity for secure authentication
- Set up role-based access control (RBAC) policies

# 5. **Monitoring & Logging**
- Enabled Azure Monitor diagnostics
- Configured Network Watcher for traffic analysis
- Set up alerts for connection failures

---

# Challenges Faced & Resolutions

# **Challenge 1: DNS Resolution Failures**

#### Problem:
After creating private endpoints, the service URLs were not resolving to private IP addresses. Clients were still trying to connect to public IP addresses, bypassing the private endpoint.

# Root Cause:
- Private DNS zones were not properly linked to the VNet
- Azure services were still resolving to their public DNS names
- DNS query routing was not configured correctly

# Resolution:
 **Solution:**
1. Created Private DNS Zones specific to each Azure service:
   - `privatelink.database.windows.net` (SQL Database)
   - `privatelink.blob.core.windows.net` (Storage Account)
   - `privatelink.vaultcore.azure.net` (Key Vault)

2. Linked the Private DNS Zones to the VNet using:
   ```bash
   az network private-dns link vnet create \
     --resource-group myRG \
     --zone-name privatelink.blob.core.windows.net \
     --name myDNSLink \
     --virtual-network myVNet \
     --registration-enabled false
   ```

3. Verified DNS resolution:
   ```bash
   nslookup mystorageaccount.blob.core.windows.net
   ```

4. Added A records in Private DNS zones pointing to private endpoint IP addresses

---

# **Challenge 2: Network Security Group (NSG) Rules Blocking Traffic**

# Problem:
Applications deployed in the VNet could not communicate with the private endpoint due to NSG rules.

# Root Cause:
- Default NSG rules were too restrictive
- Outbound rules were blocking port 443 (HTTPS) traffic
- The private endpoint subnet had deny-all rules

# Resolution:
**Solution:**
1. Added explicit allow rules in the Private Endpoint subnet NSG:
   ```bash
   az network nsg rule create \
     --resource-group myRG \
     --nsg-name myNSG \
     --name AllowPrivateEndpoint \
     --direction Outbound \
     --source-address-prefixes '*' \
     --source-port-ranges '*' \
     --destination-address-prefixes 'PrivateEndpoint' \
     --destination-port-ranges '443' \
     --access Allow \
     --protocol Tcp
   ```

2. Verified traffic flow using Azure Network Watcher
3. Tested connectivity from application VM to private endpoint

---

# **Challenge 3: Private Endpoint Connection Approval Process**

# Problem:
Unable to establish connections because private endpoint requests were not being approved. The service owner had to manually approve each connection.

# Root Cause:
- Azure services require manual approval of private endpoint connections
- Auto-approval was not enabled
- Connection requests were pending indefinitely

# Resolution:
 **Solution:**
1. Accessed the Azure resource (e.g., Storage Account)
2. Navigated to **Private endpoint connections** blade
3. Approved pending connection requests:
   ```bash
   az network private-endpoint-connection approve \
     --resource-group myRG \
     --resource-name myStorageAccount \
     --resource-type Microsoft.Storage/storageAccounts \
     --name PEConnection
   ```

4. For automation, enabled auto-approval via Azure Policy or ARM templates

---

# **Challenge 4: Service Connectivity Issues from On-Premises**

# Problem:
On-premises clients could not access Azure services through the private endpoint. The hybrid connectivity was not established.

# Root Cause:
- No VPN or ExpressRoute gateway configured
- DNS resolution not forwarding to Private DNS zones from on-premises
- Network routing was incomplete

# Resolution:
 **Solution:**
1. Deployed **VPN Gateway** or **ExpressRoute** for hybrid connectivity:
   ```bash
   az network vnet-gateway create \
     --resource-group myRG \
     --name myVPNGateway \
     --public-ip-address myPublicIP \
     --vnet myVNet \
     --gateway-type Vpn \
     --vpn-type RouteBased
   ```

2. Configured DNS forwarding from on-premises DNS servers to Azure DNS (168.63.129.16):
   - Set up Conditional Forwarders for private DNS zones
   - Pointed to Azure DNS IP 168.63.129.16

3. Created appropriate UDRs (User Defined Routes) for proper traffic routing

4. Tested connectivity from on-premises workstation:
   ```bash
   ping mystorageaccount.blob.core.windows.net
   ```

---

# **Challenge 5: Managed Identity and Key Vault Access**

# Problem:
Applications using Managed Identity could not authenticate to Key Vault through the private endpoint.

# Root Cause:
- Managed Identity had no RBAC permissions on Key Vault
- Service Principal was not assigned proper roles
- Private endpoint was created but RBAC policies were missing

# Resolution:
 **Solution:**
1. Assigned **Key Vault Secrets User** role to the Managed Identity:
   ```bash
   az role assignment create \
     --assignee-object-id <managed-identity-id> \
     --role "Key Vault Secrets User" \
     --scope /subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.KeyVault/vaults/<vault-name>
   ```

2. Updated the firewall settings on Key Vault to allow access from the VNet:
   - Set firewall to "Disabled" or allow specific VNet/Subnet

3. Tested authentication using Managed Identity:
   ```csharp
   var credential = new DefaultAzureCredential();
   var client = new SecretClient(new Uri("https://mykeyvault.vault.azure.net/"), credential);
   ```

---

# **Challenge 6: Monitoring and Troubleshooting Connection Failures**

# Problem:
Difficult to diagnose connection failures. No visibility into which requests were failing or why.

# Root Cause:
- Diagnostics were not enabled on private endpoints
- Network Watcher was not capturing traffic flows
- Azure Monitor logs were not configured

# Resolution:
**Solution:**
1. Enabled **Diagnostic Settings** on private endpoints:
   ```bash
   az monitor diagnostic-settings create \
     --name myPrivateEndpointDiagnostics \
     --resource /subscriptions/<sub-id>/resourceGroups/<rg-name>/providers/Microsoft.Network/privateEndpoints/<pe-name> \
     --logs '[{"category":"PENetworkTraffic","enabled":true}]' \
     --workspace /subscriptions/<sub-id>/resourceGroups/<rg-name>/providers/Microsoft.OperationalInsights/workspaces/<workspace-name>
   ```

2. Set up **Network Watcher Flow Logs** to monitor traffic:
   ```bash
   az network watcher flow-log create \
     --resource-group myRG \
     --network-watcher-name myNetworkWatcher \
     --name myFlowLog \
     --nsg myNSG \
     --storage-account mystorageaccount \
     --enabled true
   ```

3. Created queries in **Azure Monitor** to analyze logs and troubleshoot issues

4. Set up alerts for failed connection attempts

---

# Final Architecture

```
┌─────────────────────────────────────────────┐
│         On-Premises Network                 │
│  (DNS Forwarding + VPN/ExpressRoute)        │
└────────────────────┬────────────────────────┘
                     │
                 VPN Gateway
                     │
┌────────────────────▼────────────────────────┐
│         Azure Virtual Network               │
│  ┌──────────────────────────────────────┐   │
│  │    Application Subnet                │   │
│  │  ┌──────────────────────────────┐   │   │
│  │  │   Virtual Machine / App      │   │   │
│  │  │  (Managed Identity)          │   │   │
│  │  └──────────────────────────────┘   │   │
│  └──────────────────────────────────────┘   │
│                                             │
│  ┌──────────────────────────────────────┐   │
│  │    Private Endpoint Subnet           │   │
│  │  ┌─────────────────────────────┐    │   │
│  │  │  Private Endpoint (PE)      │    │   │
│  │  │  192.168.1.10               │    │   │
│  │  └─────────────────────────────┘    │   │
│  │  ┌─────────────────────────────┐    │   │
│  │  │  Private DNS Zone           │    │   │
│  │  │  (privatelink.blob...)      │    │   │
│  │  └─────────────────────────────┘    │   │
│  └──────────────────────────────────────┘   │
└────────────────────┬────────────────────────┘
                     │ (Private Connection)
          ┌──────────▼──────────┐
          │  Azure Services     │
          │  - Storage Account  │
          │  - Key Vault        │
          │  - SQL Database     │
          └─────────────────────┘

---

## 🔍 Troubleshooting Quick Reference

| Issue | Quick Check |
|-------|------------|
| DNS not resolving | Check Private DNS Zone links to VNet |
| Connection refused | Verify NSG allow rules for port 443 |
| Pending approval | Check Azure resource for private endpoint connection requests |
| On-premises can't connect | Verify VPN/ExpressRoute and DNS forwarders |
| Managed Identity fails | Check Key Vault RBAC roles and firewall |
| Can't see logs | Enable Diagnostic Settings and check Log Analytics |

---

# Resources

- [Azure Private Link Documentation](https://docs.microsoft.com/en-us/azure/private-link/)
- [Private DNS Zones](https://docs.microsoft.com/en-us/azure/dns/private-dns-overview)
- [Network Security Groups](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)
- [Azure Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/)

---

# Conclusion

Implementing Azure Private Link requires careful attention to network configuration, DNS resolution, and access control. By addressing each challenge systematically and following best practices, a secure and reliable private connectivity solution can be established for Azure services.
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
