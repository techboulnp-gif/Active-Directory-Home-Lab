# 🔐 On-Premise Active Directory Home Lab

## 📋 Objective

To simulate a **corporate network environment** by configuring a Windows Server 2019 Domain Controller and managing enterprise user accounts. This project demonstrates proficiency with **Active Directory Domain Services (AD DS)**, **DHCP/DNS configuration**, **PowerShell scripting**, and **Group Policy Management**.

---

## 🛠️ Tools & Technologies Used

- **VirtualBox** - Hypervisor for virtual machine management
- **Windows Server 2019 ISO** - Domain Controller operating system
- **Windows 10 ISO** - Client machine for testing
- **PowerShell** - Bulk user creation and automation scripts
- **Active Directory Domain Services (AD DS)** - User and computer management
- **DHCP/DNS** - Network services configuration
- **Group Policy Management** - Security policies and configurations

---

## 🔧 Key Skills Demonstrated

✅ **Active Directory Domain Services (AD DS) Installation & Configuration**
✅ **Domain Controller Promotion**
✅ **DHCP & DNS Configuration**
✅ **Bulk User Creation via PowerShell Scripting**
✅ **Organizational Units (OUs) & Group Policy Objects (GPOs)**
✅ **User Account Management & Permissions**
✅ **Network Topology Design & Implementation**

---

## 📊 Network Diagram

```
┌─────────────────────────────────────────┐
│      Virtual Network (192.168.1.0/24)   │
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────────────────────────────┐   │
│  │  Domain Controller (DC1)         │   │
│  │  OS: Windows Server 2019         │   │
│  │  Role: AD DS, DHCP, DNS          │   │
│  │  IP: 192.168.1.5                 │   │
│  └──────────────────────────────────┘   │
│           ⬇️ DHCP/DNS                   │
│                                         │
│  ┌──────────────────────────────────┐   │
│  │  Client Machine (CLIENT1)        │   │
│  │  OS: Windows 10                  │   │
│  │  Role: Domain Member             │   │
│  │  IP: 192.168.1.100 (DHCP)        │   │
│  └──────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

![Network Diagram Placeholder](https://via.placeholder.com/600x300?text=AD+Network+Topology)

---

## 🚀 Implementation Steps

### Step 1️⃣: Virtual Machine Setup & Network Configuration

**Objective:** Create and configure virtual machines with proper network settings.

**Actions Taken:**
1. Created two virtual machines in VirtualBox:
   - **DC1** (Domain Controller) - Windows Server 2019
   - **CLIENT1** (Member Client) - Windows 10
2. Configured network settings:
   - Internal network adapter for domain communication
   - Static IP for DC1 (192.168.1.5)
   - DHCP-enabled adapter for CLIENT1
3. Installed Windows Server 2019 and Windows 10 operating systems

**Screenshot:** ![VM Setup Placeholder](https://via.placeholder.com/600x400?text=VirtualBox+VM+Configuration)

---

### Step 2️⃣: Installing Active Directory Domain Services (AD DS)

**Objective:** Install and configure Active Directory on the Domain Controller.

**Actions Taken:**
1. Opened **Server Manager** on Windows Server 2019
2. Added **Active Directory Domain Services** role
3. Created a new forest and domain: `corp.local`
4. Set domain functional level: Windows Server 2016
5. Configured DSRM (Directory Services Restore Mode) password

**PowerShell Command Example:**
```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

**Screenshot:** ![AD DS Installation Placeholder](https://via.placeholder.com/600x400?text=Active+Directory+Installation)

---

### Step 3️⃣: Post-Deployment Configuration & Domain Controller Promotion

**Objective:** Finalize domain controller setup and configure network services.

**Actions Taken:**
1. Promoted DC1 to Domain Controller for `corp.local` forest
2. Configured DNS zones (Forward & Reverse Lookup Zones)
3. Set up **DHCP** on DC1:
   - Scope: 192.168.1.100 - 192.168.1.200
   - Default Gateway: 192.168.1.5
   - DNS Servers: 192.168.1.5
4. Authorized DHCP server in Active Directory
5. Joined CLIENT1 to the `corp.local` domain

**Screenshot:** ![Domain Controller Setup Placeholder](https://via.placeholder.com/600x400?text=DC+Configuration+Complete)

---

### Step 4️⃣: Bulk User Creation Using PowerShell

**Objective:** Automate user account creation for enterprise simulation.

**Actions Taken:**
1. Created 1,000+ mock user accounts using PowerShell script
2. Organized users in Organizational Units (OUs):
   - `OU=Sales`
   - `OU=IT`
   - `OU=Finance`
   - `OU=HR`
3. Set standardized user properties:
   - Email addresses
   - Phone numbers
   - Manager assignments
   - Group memberships

**PowerShell Script Example:**
```powershell
# Create new user in Active Directory
New-ADUser -Name "John Smith" `
  -SamAccountName "jsmith" `
  -UserPrincipalName "jsmith@corp.local" `
  -Path "OU=Sales,DC=corp,DC=local" `
  -Enabled $true `
  -AccountPassword (ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force)

# Bulk import from CSV
Import-Csv -Path "C:\users.csv" | ForEach-Object {
  New-ADUser -Name $_.Name -SamAccountName $_.SamAccountName -UserPrincipalName $_.UserPrincipalName
}
```

**Result:** ✅ **1,000+ users successfully created and organized**

**Screenshot:** ![User Creation Placeholder](https://via.placeholder.com/600x400?text=1000+Users+Created)

---

### Step 5️⃣: Group Policy Management

**Objective:** Implement security policies across the domain.

**Actions Taken:**
1. Created Group Policy Objects (GPOs) for:
   - **Password Policy**: Minimum 12 characters, complexity required
   - **Account Lockout**: 5 failed attempts = 30-minute lockout
   - **Audit Policy**: Track user logons and access
2. Applied GPOs to organizational units
3. Tested policy enforcement on client machines

**Screenshot:** ![Group Policy Placeholder](https://via.placeholder.com/600x400?text=Group+Policy+Objects)

---

## ✅ Outcomes & Results

✅ **Successfully built a functional domain environment** with Windows Server 2019 Domain Controller

✅ **Configured enterprise-grade services:**
- Active Directory Domain Services
- DHCP (Dynamic Host Configuration Protocol)
- DNS (Domain Name System)
- Group Policy Management

✅ **Demonstrated scalability** by creating and managing 1,000+ user accounts

✅ **Implemented security policies** using Group Policy Objects

✅ **Validated domain functionality** with successful client machine authentication

---

## 🎓 Key Learnings & Skills Acquired

- Understanding of enterprise directory services architecture
- Proficiency with PowerShell scripting for automation
- Network service configuration (DHCP/DNS)
- Security policy implementation
- User and computer account management
- Troubleshooting domain-related issues
- Best practices for identity and access management

---

## 📝 Next Steps / Future Enhancements

- Implement **Group Managed Service Accounts (gMSA)**
- Configure **Multi-Domain Forest** topology
- Set up **Active Directory Certificate Services (AD CS)**
- Implement **Single Sign-On (SSO)** solutions
- Deploy **Azure AD Connect** for hybrid cloud integration

---

## 📚 Resources & References

- [Microsoft Active Directory Documentation](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-domain-services)
- [PowerShell Active Directory Module](https://docs.microsoft.com/en-us/powershell/module/activedirectory/)
- [Group Policy Overview](https://docs.microsoft.com/en-us/windows-server/identity/group-policy/group-policy-overview)
- [DHCP Configuration Guide](https://docs.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-top)

---

**Created by:** Art Johnson | **Date:** 2026 | **Status:** ✅ Complete
