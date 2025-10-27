# Enterprise Virtual Lab (Hyper-V)

## Overview
This project simulates a 250-user, hybrid enterprise network using virtualization on Hyper-V.  
The core objective is to establish a secure, professional on-premises core and prepare the foundation for cloud integration (Azure/Entra ID) using best practices like **AGDLP** and **PowerShell automation**.

---

## 🧱 Topology & Network Core (Phase 1 Complete)
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

```text
enterprise.local
├── Employees (OU)          <-- GPO Target for All User Policies (Screen lock, etc.)
│   ├── Finance (OU)        <-- Contains: Finance Users & GG-Finance-Users
│   ├── HR (OU)             <-- Contains: HR Users & GG-HR-Users
│   ├── Sales (OU)
│   ├── Operations (OU)
│   ├── IT (OU)
│   └── Remote (OU)
│
├── Workstations (OU)       <-- GPO Target for Client Machines (BitLocker, Wallpaper)
├── Servers (OU)            <-- GPO Target for Server Security Baselines (FS01, WSUS01)
└── Service Accounts (OU)   <-- Container for Non-Human Identities (svc-backup, svc-adconnect)