# Enterprise Virtual Lab (Hyper-V)

## Overview
This project simulates a 250-user, hybrid enterprise network using virtualization on Hyper-V. The core objective is to establish a secure, professional on-premises core and prepare the foundation for cloud integration (Azure/Entra ID) using best practices like AGDLP and PowerShell automation.

---

## Topology & Network Core (Phase 1 Complete)
The network is logically separated to enforce security and control traffic flow.

| Component | Role | Status | Network Configuration |
|------------|------|--------|------------------------|
| **pfSense Firewall (FW01)** | Perimeter Router/Gateway | ✅ CONFIGURED | LAN: 10.0.1.1/24 (Default Gateway). DHCP disabled. |
| **Windows Server 2022 (DC01)** | Domain Controller | ✅ CONFIGURED | Static IP: 10.0.1.10. Hosts AD DS, DNS, DHCP. |
| **Internal LAN (HQ)** | Network Segment | ✅ OPERATIONAL | DHCP Pool: 10.0.1.50–10.0.1.200. Subnet: 10.0.1.0/24. |
| **Virtual Switches** | Network Segmentation | ✅ CREATED | External_WAN (Internet Access) and HQ_Internal_LAN (Isolated Network). |

---

## 🧩 Active Directory & Security Architecture (Phase 1 Complete)
The entire identity and permissions structure has been deployed and populated using **PowerShell automation**.

### Organizational Unit (OU) Hierarchy
The OUs are structured for **Group Policy (GPO)** targeting and **administrative delegation**.

---

### 🔐 Access Control Model (AGDLP Implementation)
This model separates **membership** from **permission** through **group nesting**.

| Group Type | Example | Location | Function |
|-------------|----------|-----------|-----------|
| **Global Group (G)** | GG-Finance-Users | Departmental OU (Finance) | **Membership (WHO):** Contains user accounts. |
| **Domain Local Group (D)** | DLG-Finance-Modify | Parent Employees OU | **Permission (WHAT):** Applied to file shares (\\FS01\\Finance). |
| **Tiered Admin** | GG-Server-Admins | Inside DLG-Server-Admins | **Least Privilege:** Grants restricted server access only to senior IT staff. |

---

## ✅ Current Progress (Phase 1 Final State)

| Status | Achievement | Rationale |
|---------|--------------|------------|
| **Networking Core** | DHCP/DNS/Gateway Finalized | All clients receive correct network info automatically. |
| **AD Structure** | OU/Group Creation Complete | PowerShell scripts created all OUs, GGs, and DLGs. |
| **Provisioning** | 250 Users Created & Grouped | Bulk user creation completed with proper GG membership. |
| **Nesting** | AGDLP Finalized | All GGs nested into DLGs, completing the chain (User → GG → DLG). |

---

## 🚀 Immediate Next Steps (Phase 2)

| Step | Task | Rationale |
|------|------|------------|
| **1. Deploy & Join Servers** | Deploy and join **FS01 (10.0.1.20)** and **WSUS01 (10.0.1.30)** to the domain. | Integrates production servers into AD management. |
| **2. Configure Initial GPOs** | Create Password Policy (12-char min), Windows Update targeting, and AD Auditing GPOs. | Enforces baseline domain security. |
| **3. Configure File Shares** | Create file shares (\\FS01\\Finance, \\FS01\\HR) and apply NTFS permissions to **DLG** groups. | Validates the **AGDLP** model (final "P" layer). |

---

### 🧠 Concept Summary: AGDLP Flow
User Account (A)
↓ member of
Global Group (G)
↓ member of
Domain Local Group (DLG)
↓ assigned permissions on
Resource (P)

### Progress Screenshots
### Hyper-V Manager
![Hyper-V Manager](Images/hyper-v-created-vms.png)

### Virtual Switches
- Network segmentation between external and internal networks.  
- `External` connects pfSense WAN to the Internet.  
- `Internal` connects all internal VMs securely.  
![Virtual Switches Configuration](Images/hyper-v-virtual-switches.png)

### pfSense Firewall (FW01)
- Firewall/Router  
- Handles NAT, routing, and perimeter security between external and internal networks.  
![pfSense FW01 Status 1](Images/fw01-status-1.png) 

### Windows Server 2022 (DC01)
- Domain Controller  
- Hosts **Active Directory**, **DNS**, and **DHCP**.  
- Provides centralized identity services for the lab.  
![DC01 Hardware Settings](Images/dc01-hyper-v-hardware-settings.png)


![Configure DNS Name/Server](Images/set-dns.png)
![Configure DNS Exclusion](Images/dns-exclusion.png)
![Configure DHCP Server](Images/dhcp-server.png)
![Configure DHCP Options](Images/configure-dhcp.png)
![Server Login Screen](Images/server-screen-login.png)
![Create Active Directory OU GG ](Images/ad-gg-1.png)
![Create Active Directory OU DLG](Images/created-dlgs.png)

---

## Immediate Next Steps

1. **Bulk-Create Users and Service Accounts via PowerShell**  
   - Automate user provisioning using CSV and PowerShell scripting.  
   - Reinforces automation and real-world administrative practices.
 
---