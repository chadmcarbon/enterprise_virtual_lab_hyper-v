# Enterprise Virtual Lab (Hyper-V)

## Overview
This project simulates a real-world enterprise network using virtualization in **Hyper-V on Windows 11**. It replicates the layered architecture of a corporate IT environment with perimeter security, centralized identity, and internal routing.

---

## Topology

**Internet ⇄ pfSense Firewall ⇄ Internal LAN**  
  ↳ **DC01 – Windows Server 2022 (10.0.1.10)**  
  ↳ **Future Clients – Windows 10/11 (10.0.1.x)**  

---

## Components

- **pfSense Firewall (FW01)**
  - Firewall/Router 
  - Handles NAT, routing, and perimeter security between external and internal networks.
  
- **Windows Server 2022 (DC01)**
  - Domain Controller
  - Hosts Active Directory, DNS, and DHCP.
  - Central Identity service for the lab.

- **Virtual Switches**
  - Network Segmentation (External and Internal)
  - External virtual switch connects pfSense WAN to the Internet.
  - Internal virtual switch connects all internal VMs securely

---

## Objectives
- Build a realistic enterprise topology with routing and identity separation.  
  
- Demonstrate **Active Directory**, **DNS**, and **DHCP** administration.  
  
- Implement **network segmentation** and **firewall policies**.   

---

## Current Progress
✅ Virtual switches created  
✅ pfSense installed and configured (WAN + LAN)  
✅ Internal LAN operational (10.0.1.0/24)  
✅ Windows Server 2022 installed and statically configured
✅ Domain Services (AD DS) successfully installed
✅ Active Directory Forest created
✅ DHCP and DNS Roles configured
✅ Created Department OUs 


---

## Immediate Next Steps 

1. **Create Security Groups Using AGDLP**  
   - Implement access layering with Global Groups (GG-Users) and Domain Local Groups (DLG-Modify/Read).  
   - Mimics real-world enterprise permissions structure.  

2. **Bulk-Create Users and Service Accounts via PowerShell**  
   - Automate user provisioning using CSV input and PowerShell scripting.  
   - Reinforces automation and administrative best practices.  