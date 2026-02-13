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

### Step 7: Static Network Identity
**Action:** Configured a static IPv4 address for the Domain Controller to ensure a consistent network identity. 
* **Configuration:** Assigned `172.16.0.1` with a `255.255.255.0` subnet mask.
* **Evidence:** ![Static IP Config](Active-Directory-Lab/docs/phase-1/static_ip.png)
 


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

### Phase 3: Active Directory Configuration & Domain Integration
**In this phase, I transformed the standalone server into a central management hub by implementing security policies, automating massive user growth, and integrating a workstation into the

#### Step 8️⃣: DHCP Role Installation
**Action:** Installed the **DHCP Server role** on DC01 to enable automatic IP address assignment for client machines on the internal network.
**Evidence:**
![DHCP Role](phase-3/9_DHCP_Role_Installed.png)
---

#### Step 9️⃣: DHCP Authorization
**Action:** **Authorized the DHCP server** in Active Directory to allow it to begin servicing client requests on the domain network.
**Evidence:**
![DHCP Authorized](phase-3/10_DHCP_Authorized.png)
---

#### Step 🔟: DHCP Scope Configuration
**Action:** Created and activated a **DHCP scope (172.16.0.100-200)** to automatically assign IP addresses to Windows 10 clients joining the domain.
**Evidence:**
![DHCP Scope](phase-3/11_DHCP_Scope_Active.png)
---

domain.**

#### Step 8️⃣: Security Hardening (Group Policy)
**Action:** I used the **Group Policy Management Editor** to enforce an enterprise-grade security baseline:
- **Minimum Password Length:** Increased to **12 characters**.
- **Complexity Requirements:** Enabled to ensure passwords meet modern security standards.
- **Enforce Password History:** Set to **24 passwords** to prevent "cycling" old credentials.
**Evidence:**
![Password Policy](phase-3/12_Password_Lockout_Policy.png)
---
### Step 9: Automation & "Big Data" Management
**Action:** Using a PowerShell script and a names.txt file, I automated the creation of **5,000** users.
* **The Display Limit:** During verification, I documented the AD safety limit, which defaults to 2,000 objects.
* **Verification:** Successfully customized the MMC view to confirm all **5,000 objects** were provisioned.
* **Evidence:** [Bulk Users](image_971c36.png)

  

---
### Step 10: Critical Troubleshooting: The Duplicate IP Conflict
**Action:** A major hurdle occurred when the Windows 10 client could not reach the Domain Controller.
* **Diagnosis:** Using `ipconfig /all`, I identified a `(Duplicate)` IP status for `172.16.0.1`.
* **Resolution:** Reconfigured the client with a unique static IP of `172.16.0.2`, restoring domain communication.
* **Evidence:** [IP Conflict](image_98081a.png)

  

---
#### Step 1️⃣1️⃣: Domain Join & Verification
**Action:** Successfully joined the workstation to **mylab.local**, receiving the "Welcome" handshake.
**Evidence:**
![Domain Join](phase-3/13_Domain_Join_Success.png)
---
#### Step 1️⃣2️⃣: User Authentication Confirmation
**Action:** Logged in to the client as **domain user fus.masa**. This confirmed that **DNS, DHCP, and AD Authentication** are all working in harmony.
**Evidence:**
![User Login](phase-3/14_Successful_Domain_User_Login.png)
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
