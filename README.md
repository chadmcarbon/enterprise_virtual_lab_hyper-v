# Enterprise Virtual Lab (Hyper-V)

## Overview
This project simulates a real-world enterprise network using virtualization in **Hyper-V on Windows 11**.  
It replicates the layered architecture of a corporate IT environment with perimeter security, centralized identity, and internal routing.

---

## Topology

**Internet ⇄ pfSense Firewall ⇄ Internal LAN (10.0.1.0/24)**  
  ↳ **DC01 – Windows Server 2022 (10.0.1.10)**  
  ↳ **Future Clients – Windows 10/11 (10.0.1.x)**  

---

## Components

| Component | Role | IP / Network | Description |
|------------|------|---------------|--------------|
| **pfSense (FW01)** | Firewall / Router | WAN: DHCP (192.168.x.x) <br> LAN: 10.0.1.1/24 | Handles NAT, routing, and perimeter security between external and internal networks. |
| **Windows Server 2022 (DC01)** | Domain Controller | 10.0.1.10/24 | Hosts Active Directory, DNS, and DHCP. Central identity service for the lab. |
| **Windows 10 Client (planned)** | Domain-joined workstation | 10.0.1.x/24 | Used for domain login, Group Policy testing, and monitoring exercises. |
| **Virtual Switches** | Network Segmentation | External + Internal | `CPC_External_Virtual_Switch` connects pfSense WAN to the Internet. `HQ_Internal_LAN` connects all internal VMs securely. |

---

## Objectives
- Build a realistic enterprise topology with routing and identity separation.  
- Practice **Active Directory**, **DNS**, and **DHCP** administration.  
- Implement **network segmentation** and **firewall policies**.  
- Prepare for **SOC** and **SIEM** projects within a hybrid environment.  

---

## Current Progress
✅ Virtual switches created  
✅ pfSense installed and configured (WAN + LAN)  
✅ Internal LAN operational (10.0.1.0/24)  
✅ Windows Server 2022 installed and statically configured  
🚧 Domain Controller promotion pending  
🚧 DNS and DHCP configuration pending  
🚧 Client VM deployment pending  

---

## Immediate Next Steps

1. **Promote DC01 to northwind.local**  
   - Establish the Active Directory forest and define the internal namespace.  

2. **Add DNS and DHCP Roles**  
   - Provide centralized name resolution and IP assignment across the network.  
   - Configure DHCP scope: `10.0.1.50 – 10.0.1.200`.  

3. **Create Organizational Units (Departments & Roles)**  
   - Structure: Finance, HR, Sales, Operations, IT.  
   - Enables granular Group Policy targeting and easier user management.  

4. **Create Security Groups Using AGDLP**  
   - Implement access layering with Global Groups (GG-Users) and Domain Local Groups (DLG-Modify/Read).  
   - Mimics real-world enterprise permissions structure.  

5. **Bulk-Create Users and Service Accounts via PowerShell**  
   - Automate user provisioning using CSV input and PowerShell scripting.  
   - Reinforces automation and administrative best practices.   