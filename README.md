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
![Hardware Summary](docs/phase-1/01_DC01_Hardware_Summary.png)

---

#### Step 2️⃣: OS Selection (Part 1)

**Action:** Selecting the **Windows Server 2022 Evaluation ISO**.

**Evidence:**
![OS Selection 1](docs/phase-1/01b_OS_Selection.png)

---

#### Step 3️⃣: OS Selection (Part 2)

**Action:** Ensuring the **Desktop Experience** version is installed for GUI-based management.

**Evidence:**
![OS Selection 2](docs/phase-1/02_DC01_OS_Selection.png)

---

#### Step 4️⃣: Initial Deployment

**Action:** Successful OS installation and first **Administrator** login to DC01.

**Evidence:**
![First Login](docs/phase-1/03_DC01_First_Login.png)

---

#### Step 5️⃣: Standardized Naming

**Action:** Implementing corporate naming standards by renaming the server to **DC01**.

**Evidence:**
![Rename DC01](docs/phase-1/04_DC01_Renamed.png)

---

#### Step 6️⃣: Domain Verification

**Action:** Confirming successful promotion of **DC01** to the **mylab.local** domain.

**Evidence:**
![Domain Success](docs/phase-1/05_DC01_Domain_Verified.png)

---

#### Step 7️⃣: Static Network Identity

**Action:** Implementation of **static IPv4 (172.16.0.1)** and **DNS services** to ensure service persistence.

**Evidence:**
![Static IP Config](docs/phase-1/06_Static_IP_Config.png)

---

### Phase 2: Domain Services & User Management

#### Step 1️⃣: Installing Active Directory Domain Services (AD DS)

**Objective:** Install and configure Active Directory on the Domain Controller.

**Actions Taken:**
- Opened **Server Manager** on Windows Server 2022
- Added **Active Directory Domain Services** role
- Created a new forest and domain: **mylab.local**
- Set domain functional level: **Windows Server 2016**
- Configured DSRM (Directory Services Restore Mode) password

**PowerShell Command Example:**
```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

---

#### Step 2️⃣: Post-Deployment Configuration & Domain Controller Promotion

**Objective:** Finalize domain controller setup and configure network services.

**Actions Taken:**
- Promoted DC01 to Domain Controller for **mylab.local** forest
- Configured **DNS zones** (Forward & Reverse Lookup Zones)
- Set up **DHCP** on DC01:
  - Scope: 172.16.0.100 - 172.16.0.200
  - Default Gateway: 172.16.0.1
  - DNS Servers: 172.16.0.1
  - Authorized DHCP server in Active Directory
- Joined CLIENT1 to the **mylab.local** domain

---

#### Step 3️⃣: Bulk User Creation Using PowerShell

**Objective:** Automate user account creation for enterprise simulation.

**Actions Taken:**
- Created **1,000+ mock user accounts** using PowerShell script with **names.txt** file
- Organized users in Organizational Units (OUs):
  - OU=Sales
  - OU=IT
  - OU=Finance
  - OU=HR
- Set standardized user properties:
  - Email addresses
  - Phone numbers
  - Manager assignments
  - Group memberships

**PowerShell Script Example:**
```powershell
# Bulk import from names.txt
$names = Get-Content "C:\names.txt"

foreach ($name in $names) {
    $samAccountName = ($name -split ' ')[0].ToLower() + ($name -split ' ')[1].ToLower().Substring(0,1)
    
    New-ADUser `
        -Name "$name" `
        -SamAccountName "$samAccountName" `
        -UserPrincipalName "$samAccountName@mylab.local" `
        -Path "OU=Users,DC=mylab,DC=local" `
        -Enabled $true `
        -AccountPassword (ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force)
}
```

**Result:**
- ✅ 1,000+ users successfully created and organized
- ✅ All users properly scoped to departmental OUs
- ✅ Standardized naming conventions applied

---

#### Step 4️⃣: Group Policy Management

**Objective:** Implement security policies across the domain.

**Actions Taken:**
- Created **Group Policy Objects (GPOs)** for:
  - **Password Policy:** Minimum 12 characters, complexity required
  - **Account Lockout:** 5 failed attempts = 30-minute lockout
  - **Audit Policy:** Track user logons and access
- Applied GPOs to organizational units
- Tested policy enforcement on client machines

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
