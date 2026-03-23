
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
# Azure Service Endpoints Project
  
https://github.com/shreyatiwari1311-lgtm/Beginner-azure-projects/blob/main/services%20endpoints.pdf?raw=true

 Project Documentation:


 What I Built

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
