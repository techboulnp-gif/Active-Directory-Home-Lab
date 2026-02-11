# 🔐 On-Premise Active Directory Home Lab

## 📋 Objective

To simulate a **corporate network environment** by configuring a **Windows Server 2022 Domain Controller** and managing enterprise user accounts. This project demonstrates proficiency with **Active Directory Domain Services (AD DS)**, **DHCP/DNS configuration**, **PowerShell scripting**, and **Group Policy Management**.

---

## 🛠️ Tools & Technologies Used

- **VirtualBox** - Hypervisor for virtual machine management
- **Windows Server 2022 ISO** - Domain Controller operating system
- **Windows 10 ISO** - Client machine for testing
- **PowerShell** - Bulk user creation and automation scripts
- **Active Directory Domain Services (AD DS)** - User and computer management
- **DHCP/DNS** - Network services configuration
- **Group Policy Management** - Security policies and configurations

---

## 🔧 Key Skills Demonstrated

- ✅ **Active Directory Domain Services (AD DS) Installation & Configuration**
- ✅ **Domain Controller Promotion**
- ✅ **DHCP & DNS Configuration**
- ✅ **Bulk User Creation via PowerShell Scripting**
- ✅ **Organizational Units (OUs) & Group Policy Objects (GPOs)**
- ✅ **User Account Management & Permissions**
- ✅ **Network Topology Design & Implementation**

---

## 📊 Network Diagram

```
┌─────────────────────────────────────────┐
│   Virtual Network (172.16.0.0/24)       │
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────────────┐                   │
│  │   DC01           │                   │
│  │ Windows Server   │                   │
│  │      2022        │                   │
│  │ 172.16.0.1       │                   │
│  │ mylab.local      │                   │
│  └──────────────────┘                   │
│           │                             │
│           ├─ AD DS                      │
│           ├─ DNS                        │
│           └─ DHCP                       │
│           │                             │
│  ┌────────┴──────────┐                  │
│  │                   │                  │
│  ▼                   ▼                  │
│ CLIENT1            CLIENT2              │
│ (Windows 10)       (Windows 10)         │
│                                         │
└─────────────────────────────────────────┘
```

---

## 🚀 Implementation Steps

### Phase 1: Infrastructure Setup

#### Step 1️⃣: Resource Calibration

**Action:** Provisioning the virtual machine with **4GB RAM** and **2 CPUs** to ensure host system stability.

**Evidence:**
![Hardware Summary](Active-Directory-Lab/docs/phase-1/01_DC01_Hardware_Summary.png)

---

#### Step 2️⃣: OS Selection (Part 1)

**Action:** Selecting the **Windows Server 2022 Evaluation ISO**.

**Evidence:**
![OS Selection 1](Active-Directory-Lab/docs/phase-1/01b_OS_Selection.png)

---

#### Step 3️⃣: OS Selection (Part 2)

**Action:** Ensuring the **Desktop Experience** version is installed for GUI-based management.

**Evidence:**
![OS Selection 2](Active-Directory-Lab/docs/phase-1/02_DC01_OS_Selection.png)

---

#### Step 4️⃣: Initial Deployment

**Action:** Successful OS installation and first **Administrator** login to DC01.

**Evidence:**
![First Login](Active-Directory-Lab/docs/phase-1/03_DC01_First_Login.png)

---

#### Step 5️⃣: Standardized Naming

**Action:** Implementing corporate naming standards by renaming the server to **DC01**.

**Evidence:**
![Rename DC01](Active-Directory-Lab/docs/phase-1/04_DC01_Renamed.png)

---

#### Step 6️⃣: Domain Verification

**Action:** Confirming successful promotion of **DC01** to the **mylab.local** domain.

**Evidence:**
![Domain Success](Active-Directory-Lab/docs/phase-1/05_DC01_Domain_Verified.png)

---

#### Step 7️⃣: Static Network Identity

**Action:** Implementation of **static IPv4 (172.16.0.1)** and **DNS services** to ensure service persistence.

**Evidence:**
![Static IP Config](Active-Directory-Lab/docs/phase-1/06_Static_IP_Config.png)

---

### Phase 2: Network Multi-Homing & PowerShell Automation

#### Step 1️⃣: Network Multi-Homing (Dual NICs)

**Action:** Configured dual **Network Interface Cards (NICs)**. One adapter is set to **NAT** for external updates, while the other is set to an **Internal Network** for isolated lab communication.

**Evidence:**
![Network Config](1_Dual_NICs.png)

---

#### Step 2️⃣: Administrative Environment Prep

**Action:** Launched the **PowerShell ISE** as Administrator to begin the automation workflow.

**Evidence:**
![ISE Setup](2_PowerShell_ISE_Open.png)

---

#### Step 3️⃣: Script Implementation

**Action:** Implemented a **foreach loop** script designed to parse a **names.txt** file and generate standardized **Active Directory user objects**.

**Evidence:**
![Script Logic](3_Script_Pasted.png)

---

#### Step 4️⃣: Persistence & Documentation

**Action:** Saved the automation logic as a reusable **.ps1 script** for future deployment and auditing.

**Evidence:**
![Script Saved](4_Script_File_Saved.png)

---

#### Step 5️⃣: Data Integration Verification

**Action:** Verified that the **names.txt** source file was correctly mapped to the script's input variable.

**Evidence:**
![Data Ready](5_Script_and_Names_Ready.png)

---

#### Step 6️⃣: Live Execution (Bulk Creation)

**Action:** Executed the script. The console reflects **real-time creation of 1,000+ accounts** in the domain.

**Evidence:**
![Script Running](6_Script_Running.png)

---

#### Step 7️⃣: Final Active Directory Audit

**Action:** Verified the successful creation of all objects within the **_EMPLOYEES Organizational Unit (OU)**.

**Evidence:**
![Final Audit](7_AD_Users_Verified.png)

---

## ✅ Outcomes & Results

- ✅ Successfully built a **functional domain environment** with Windows Server 2022 Domain Controller
- ✅ Configured enterprise-grade services:
  - **Active Directory Domain Services**
  - **DHCP (Dynamic Host Configuration Protocol)**
  - **DNS (Domain Name System)**
  - **Group Policy Management**
- ✅ Demonstrated **scalability** by creating and managing **1,000+ user accounts**
- ✅ Implemented **security policies** using Group Policy Objects
- ✅ Validated **domain functionality** with successful client machine authentication

---

## 🎓 Key Learnings & Skills Acquired

- Understanding of enterprise **directory services architecture**
- Proficiency with **PowerShell scripting** for automation
- **Network service configuration** (DHCP/DNS)
- **Security policy implementation** using GPOs
- **User and computer account management** in enterprise environments
- **Troubleshooting domain-related issues**
- Best practices for **identity and access management**

---

## 📝 Next Steps / Future Enhancements

- Implement **Group Managed Service Accounts (gMSA)**
- Configure **Multi-Domain Forest** topology
- Set up **Active Directory Certificate Services (AD CS)**
- Implement **Single Sign-On (SSO)** solutions
- Deploy **Azure AD Connect** for hybrid cloud integration
- Add **advanced network segmentation**
- Implement **Kerberos authentication hardening**

---

## 📚 Resources & References

- [Microsoft Active Directory Documentation](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-domain-services)
- [PowerShell Active Directory Module](https://docs.microsoft.com/en-us/powershell/module/activedirectory/)
- [Group Policy Overview](https://docs.microsoft.com/en-us/windows-server/identity/group-policy/group-policy-overview)
- [DHCP Configuration Guide](https://docs.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-top)

---

**Created by:** Art Johnson | **Date:** 2026 | **Status:** ✅ Complete
