# Active Directory Identity Administration: OUs, Users, and Security Groups

**Windows Server 2019 | Active Directory | ADUC | PowerShell | Windows 11**

## Project Overview

I built and administered an Active Directory identity structure representing users and departments across Toronto and Edmonton business locations. Using both Active Directory Users and Computers (ADUC) and PowerShell, I created organizational units, global security groups, and domain user accounts; assigned users to appropriate groups; enforced a password change at first sign-in; and validated domain authentication from a Windows 11 workstation.

This project demonstrates the identity-administration tasks commonly performed by help desk, service desk, and junior systems administration teams.

## Simulated Business Scenario

A growing organization needs a structured way to manage employee accounts across multiple locations. Creating every account in the default Active Directory containers would make administration, policy targeting, and access management difficult as the organization grows.

To address this, I organized directory objects by location, grouped users according to their department or access requirements, and verified that newly created users could authenticate from a domain-joined workstation.

## Project Objectives

- Create organizational units for logical separation of directory objects.
- Create global security groups for department-based membership.
- Create and configure domain user accounts.
- Require new users to change their temporary passwords at first sign-in.
- Add users to one or multiple security groups.
- Verify group memberships in Active Directory.
- Validate a new user's domain sign-in from a Windows 11 client.
- Repeat common administration tasks with PowerShell.

## Lab Environment

| Component | Technology | Purpose |
| --- | --- | --- |
| Domain controller | Windows Server 2019 | Hosts Active Directory Domain Services |
| Client workstation | Windows 11 Pro | Validates domain authentication and the first-sign-in process |
| GUI administration | Active Directory Users and Computers | Manages OUs, users, groups, and memberships |
| Automation | Windows PowerShell and the ActiveDirectory module | Creates and verifies directory objects through commands |

## Directory Design

| Directory object | Example | Administrative purpose |
| --- | --- | --- |
| Location-based OU | Toronto, Edmonton | Organizes users and groups by business location |
| Global security group | `E_Marketing` | Groups users with a shared department or access requirement |
| Domain user | Example employee account | Provides an individual identity for domain authentication |

> **Project scope:** This lab demonstrates identity organization and group membership. Assigning the groups to file, printer, or application permissions is covered separately in resource-access projects.

## Skills Demonstrated

- Active Directory identity and access administration
- Organizational unit design
- Domain user provisioning
- Global security-group creation
- Single and multiple group assignments
- Account and membership verification
- Password-change-at-first-sign-in configuration
- Windows domain authentication
- PowerShell administration with the ActiveDirectory module
- Secure handling of temporary passwords
- Technical documentation

## Implementation Summary

### 1. Created Organizational Units

I used ADUC to create location-based organizational units. This provides a logical structure for managing related users and groups and creates a foundation for future Group Policy targeting and delegated administration.

<p align="center">
  <img src="https://i.imgur.com/bB0TK3e.png" width="750" alt="Creating a location-based organizational unit in Active Directory">
</p>

### 2. Created Global Security Groups

Within the appropriate OU, I created global security groups to represent departments and access requirements. Group-based administration is more scalable and easier to audit than assigning permissions directly to individual users.

<p align="center">
  <img src="https://i.imgur.com/fB7YJe8.png" width="750" alt="Global security groups created in the Toronto organizational unit">
</p>

### 3. Provisioned Domain User Accounts

I created domain user accounts with standardized sign-in names and temporary passwords. I enabled **User must change password at next logon** so users would set private passwords during their first domain sign-in.

<p align="center">
  <img src="https://i.imgur.com/2CMH502.png" width="750" alt="Domain user accounts created in an Active Directory organizational unit">
</p>

### 4. Assigned and Verified Group Memberships

I added users to their required security groups through both the user object and the group object's **Members** tab. I also assigned a user to multiple groups in one operation and confirmed the results from the user's **Member Of** tab.

<p align="center">
  <img src="https://i.imgur.com/0FluxwU.png" width="750" alt="Verifying a user's security-group memberships in Active Directory">
</p>

### 5. Validated Domain Authentication

From a domain-joined Windows 11 workstation, I signed in with a newly created domain account. The user was required to replace the temporary password before Windows completed the sign-in, confirming that the account and password setting worked as intended.

<p align="center">
  <img src="https://i.imgur.com/xOJkJaP.png" width="750" alt="Windows requiring a new domain user to change the temporary password">
</p>

<p align="center">
  <img src="https://i.imgur.com/wyXcr52.png" width="750" alt="Successful password change during the new user's first domain sign-in">
</p>

### 6. Repeated Administration Tasks with PowerShell

I used the ActiveDirectory PowerShell module to create an OU, create a global security group, provision a user, and assign the user to the appropriate group. PowerShell makes repetitive administration more consistent and prepares the process for future bulk provisioning.

## Secure PowerShell Examples

The following commands show a corrected and more secure version of the workflow. The temporary password is entered as a `SecureString` instead of being written directly into the script or repository.

### Create an Organizational Unit

```powershell
Import-Module ActiveDirectory

$DomainPath = "DC=Adeniyi,DC=com"
$OuPath = "OU=Edmonton,$DomainPath"

New-ADOrganizationalUnit `
    -Name "Edmonton" `
    -Path $DomainPath `
    -ProtectedFromAccidentalDeletion $true
```

### Create a Global Security Group

```powershell
New-ADGroup `
    -Name "E_Marketing" `
    -SamAccountName "E_Marketing" `
    -GroupScope Global `
    -GroupCategory Security `
    -Path $OuPath `
    -Description "Edmonton Marketing users"
```

### Create and Enable a Domain User

```powershell
$Password = Read-Host "Enter a temporary password" -AsSecureString

New-ADUser `
    -Name "Karu Jaru" `
    -GivenName "Karu" `
    -Surname "Jaru" `
    -SamAccountName "Karu.Jaru" `
    -UserPrincipalName "Karu.Jaru@adeniyi.com" `
    -AccountPassword $Password `
    -Path $OuPath `
    -Enabled $true `
    -ChangePasswordAtLogon $true
```

### Add the User to a Security Group

```powershell
Add-ADGroupMember `
    -Identity "E_Marketing" `
    -Members "Karu.Jaru"
```

### Verify the Created Objects and Membership

```powershell
Get-ADOrganizationalUnit -Identity $OuPath

Get-ADUser `
    -Identity "Karu.Jaru" `
    -Properties Enabled, PasswordLastSet, MemberOf |
    Select-Object Name, SamAccountName, Enabled, PasswordLastSet, MemberOf

Get-ADGroupMember -Identity "E_Marketing"
```

## Validation

I validated the implementation by confirming that:

- The Toronto and Edmonton organizational units were created in the intended domain path.
- Global security groups appeared inside the correct OU.
- Domain user accounts were enabled and available in ADUC.
- Users appeared in the expected groups.
- Multiple memberships appeared in the user's **Member Of** tab.
- A new user could authenticate from a domain-joined Windows 11 workstation.
- Windows enforced the required password change at first sign-in.
- The updated password was accepted and the user completed the sign-in process.

## Troubleshooting Reference

| Symptom | Likely cause | Verification or resolution |
| --- | --- | --- |
| PowerShell cannot find an OU | The distinguished name or domain path is incorrect | Run `Get-ADOrganizationalUnit -Filter * | Select-Object Name, DistinguishedName` and copy the correct path |
| A user cannot sign in | The account is disabled, locked, expired, or the wrong sign-in format is being used | Check the account in ADUC or with `Get-ADUser`, then try `DOMAIN\username` or the user's UPN |
| A group membership does not appear in the user's session | The user's existing access token has not refreshed | Sign out and back in, then run `whoami /groups` on the client |
| A new password is rejected | The password does not meet the domain password policy | Review complexity, length, history, and minimum-age requirements |
| `New-ADUser` fails | A required parameter is missing or the username already exists | Review the error, confirm the OU path, and check with `Get-ADUser -Filter 'SamAccountName -eq "Karu.Jaru"'` |

## Security and Administration Practices

- Never publish passwords in scripts, screenshots, CSV files, or repository documentation.
- Use secure prompts, an approved secrets-management process, or automatically generated temporary credentials.
- Require users to change temporary passwords at first sign-in.
- Assign resource access to security groups instead of directly to individual accounts.
- Follow least privilege when delegating user and group administration.
- Use clear naming standards so accounts and groups remain easy to identify and audit.
- Disable or remove inactive accounts according to the organization's access-review process.

## Key Takeaways

This project demonstrated how a well-organized directory makes user administration easier to scale and troubleshoot. Organizational units provide structure, while security groups allow administrators to manage access through membership instead of repeatedly assigning permissions to individual users.

It also showed the value of combining ADUC with PowerShell: the GUI is useful for individual support tasks and visual verification, while PowerShell improves consistency and efficiency when the same task must be repeated.

<details>
<summary><strong>View the Complete ADUC Walkthrough</strong></summary>

### Create an Organizational Unit

1. In **Server Manager**, open **Tools > Active Directory Users and Computers**.

   <p align="center"><img src="https://i.imgur.com/UABQkcS.png" width="750" alt="Opening Active Directory Users and Computers from Server Manager"></p>

2. Right-click the domain, select **New**, and then select **Organizational Unit**.

   <p align="center"><img src="https://i.imgur.com/rOdUPzj.png" width="750" alt="Opening the new organizational unit dialog"></p>

3. Enter the OU name and create the object.

   <p align="center"><img src="https://i.imgur.com/eQIoRdd.png" width="750" alt="Naming a new organizational unit"></p>

### Create Global Security Groups

1. Right-click the appropriate OU and select **New > Group**.

   <p align="center"><img src="https://i.imgur.com/uoPJbQw.png" width="750" alt="Creating a group in an organizational unit"></p>

2. Enter the group name and configure it as a global security group.

   <p align="center"><img src="https://i.imgur.com/HPJ63kQ.png" width="750" alt="Configuring a new global security group"></p>

3. Repeat the process for the additional department or access groups.

   <p align="center"><img src="https://i.imgur.com/GhgybJp.png" width="750" alt="Security groups created in the organizational unit"></p>

### Create Domain Users

1. Right-click the appropriate OU and select **New > User**.

   <p align="center"><img src="https://i.imgur.com/ENncCqx.png" width="750" alt="Creating a user in an organizational unit"></p>

2. Enter the employee's name and user logon name.

   <p align="center"><img src="https://i.imgur.com/xfB3MWb.png" width="750" alt="Entering a new domain user's identity information"></p>

3. Assign a temporary password and keep **User must change password at next logon** selected.

   <p align="center"><img src="https://i.imgur.com/RTx3xST.png" width="750" alt="Configuring a temporary password for a new domain user"></p>

4. Review the account information and create the user.

   <p align="center"><img src="https://i.imgur.com/2YskZaJ.png" width="750" alt="Reviewing the new Active Directory user account"></p>

5. Repeat the process for the additional AD users.

   <p align="center"><img src="https://i.imgur.com/iMYNWmc.png" width="750" alt="Multiple users created in an organizational unit"></p>

### Add Users to Security Groups

1. Right-click a user and select **Add to a group**.

   <p align="center"><img src="https://i.imgur.com/zNL84DP.png" width="750" alt="Adding an Active Directory user to a group"></p>

2. Enter the group name, select **Check Names**, and confirm the selection.

   <p align="center"><img src="https://i.imgur.com/owc3DUR.png" width="750" alt="Selecting a security group for the user"></p>

3. Confirm that Active Directory completed the membership change.

   <p align="center"><img src="https://i.imgur.com/Y8AJdcr.png" width="750" alt="Successful Active Directory group membership operation"></p>

### Add Members from the Group Object

1. Open a group and select its **Members** tab.

   <p align="center"><img src="https://i.imgur.com/TknOtne.png" width="750" alt="Opening the Members tab of a security group"></p>

2. Select **Add**.

   <p align="center"><img src="https://i.imgur.com/9RepiM4.png" width="750" alt="Adding a member from the group properties"></p>

3. Enter the user's name, select **Check Names**, and confirm the account.

   <p align="center"><img src="https://i.imgur.com/kezgZZn.png" width="750" alt="Selecting a user to add to the security group"></p>

4. Confirm that the user now appears in the group's membership list.

   <p align="center"><img src="https://i.imgur.com/RrVdCws.png" width="750" alt="Verifying the user in the security group's membership list"></p>

### Add a User to Multiple Groups

1. Right-click the user and select **Add to a group**.

   <p align="center"><img src="https://i.imgur.com/EZgdSmm.png" width="750" alt="Opening the group assignment action for a user"></p>

2. Enter multiple group names separated by semicolons, select **Check Names**, and confirm the selection.

   <p align="center"><img src="https://i.imgur.com/O44uhmE.png" width="750" alt="Assigning an Active Directory user to multiple groups"></p>

3. Confirm that Active Directory completed the operation.

   <p align="center"><img src="https://i.imgur.com/SgpnGZp.png" width="750" alt="Successful multiple group assignment"></p>

4. Open the user's properties and verify the memberships from the **Member Of** tab.

   <p align="center"><img src="https://i.imgur.com/TQIaMx1.png" width="750" alt="Reviewing all groups assigned to a user"></p>

### Validate the New User's Domain Sign-In

1. On the Windows 11 client, sign out and enter the new domain user's credentials.

   <p align="center"><img src="https://i.imgur.com/avKNWzq.png" width="750" alt="Signing in to Windows with the new domain account"></p>

2. Windows prompts the user to change the temporary password.

   <p align="center"><img src="https://i.imgur.com/lM8RkiY.png" width="750" alt="First-sign-in password change prompt"></p>

3. Enter and confirm a new password that meets the domain policy.

   <p align="center"><img src="https://i.imgur.com/6Ijzeqk.png" width="750" alt="Changing the temporary domain password"></p>

4. Confirm the successful password change and complete the sign-in.

   <p align="center"><img src="https://i.imgur.com/VbePA7N.png" width="750" alt="Successful domain password change"></p>

</details>

<details>
<summary><strong>View the PowerShell Administration Evidence</strong></summary>

### Create an OU with PowerShell

The OU was created with `New-ADOrganizationalUnit` and verified in the directory.

<p align="center"><img src="https://i.imgur.com/LImtzoy.png" width="750" alt="Creating an organizational unit with PowerShell"></p>

### Create a Security Group with PowerShell

The department security group was created in the Edmonton OU with `New-ADGroup`.

<p align="center"><img src="https://i.imgur.com/cKTg1n6.png" width="750" alt="Creating an Active Directory security group with PowerShell"></p>

### Assign the User to the Group with PowerShell

The user was added to the security group with `Add-ADGroupMember`.

<p align="center"><img src="https://i.imgur.com/iPVFSRf.png" width="750" alt="Adding a user to an Active Directory group with PowerShell"></p>

### Verify the Group Membership

The user's membership was confirmed from the group's **Members** tab in ADUC.

<p align="center"><img src="https://i.imgur.com/rfrqRp7.png" width="750" alt="Verifying the PowerShell-created Active Directory group membership"></p>


</details>

## Related Projects

- [Active Directory Domain Services Deployment and Windows Client Integration](https://github.com/AdeniyiAdesakin/Install-Active-Directory-Domain-Services-and-Join-Client-s-Computer-to-Active-Directory)
- [Group Policy Object Implementations](https://github.com/AdeniyiAdesakin/Group-Policy-Object-GPO-implementations)
- [Bulk Active Directory User Provisioning with PowerShell](https://github.com/AdeniyiAdesakin/Import-bulk-Users-from-a-CSV-Spreadsheet-with-PowerShell-)
- 



