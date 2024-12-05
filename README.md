<h1>Creating Organizational Units, Groups & Users in Active Directory</h1>
<p>The purpose of creating OUs, Groups, and Users in Active Directory is to organize and manage network resources, assign appropriate permissions, and streamline user and group administration for security and access control.</p>
<h3>*Creating Organizational Units</h3>
<p>1. Go to Server manager-dashboard > Tools >Active Directory Users and Computers</p>
<p align="center"><img src="https://i.imgur.com/Jk0i5NN.png" height="50%" width="50%" alt="image"/>

<p>2. On the dashboard, right click on the domain name, go to New, then click Organizational Unit</p>
<p align="center"><img src="https://i.imgur.com/tLc36FQ.png" height="50%" width="50%" alt="image"/>

<p>3. On the New object -Organizational Unit screen, in the name space, type in the OU name you intend to create.</p>
<p align="center"><img src="https://i.imgur.com/SJSrsWn.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Creating Global Groups</h3>
<p>1. To create Global Groups in Toronto OU, from the Active Directory Users and Computer's dashboard, right click on the OU created, go to New and then click on Group</p>
<p align="center"><img src="https://i.imgur.com/zeK3BgN.png" height="50%" width="50%" alt="image"/>

<p>2. On the New Object - Group, type in the Group name in the space provided and click OK</p>
<p align="center"><img src="https://i.imgur.com/TZ8uRiB.png" height="50%" width="50%" alt="image"/>

<p>3. Repeated above steps 1 and 2 to create more groups in TorontoOU</p>
<p align="center"><img src="https://i.imgur.com/4s8QNOI.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Creating Domain User Accounts and assign them to the groups</h3>
<p>1. While on the Active Directory Users and Computers' dashboard, right click on the Organizational Unit, go to New, then click User</p>
<p align="center"><img src="https://i.imgur.com/1gUs4oc.png" height="50%" width="50%" alt="image"/>

<p>2. On the New Object - User, input the first name, last name, a user logon name and click NEXT</p>
<p align="center"><img src="https://i.imgur.com/ZNxSdwF.png" height="50%" width="50%" alt="image"/>

<p>3. On the next page, input the password, leave the “User must change password at next logon” checked, then click NEXT</p>
<p align="center"><img src="https://i.imgur.com/qgddFlJ.png" height="50%" width="50%" alt="image"/>

<p>4. On the next page, review the information and click FINISH</p>
<p align="center"><img src="https://i.imgur.com/MJGZOPD.png" height="50%" width="50%" alt="image"/>

<p>5. After creating the first user, I created more users by repeating Step 1-4.</p>
<p align="center"><img src="https://i.imgur.com/HppqZGM.png" height="50%" width="50%" alt="image"/>

<h3>*To add users to Groups</h3>
<p>1. Right-click on the User and click on Add to a group</p>
<p align="center"><img src="https://i.imgur.com/zNL84DP.png" height="50%" width="50%" alt="image"/>

<p>2. On the next page, in the” Enter the object names to select”, type in the Group you want to add user to, click check names to confirm then click OK</p>
<p align="center"><img src="https://i.imgur.com/owc3DUR.png" height="50%" width="50%" alt="image"/>

<p>3. You will get a prompt that that “The Add to Group operation was succesfully completed”, just click OK</p>
<p align="center"><img src="https://i.imgur.com/6N1yAys.png" height="50%" width="50%" alt="image"/>

<h3>*Another method to add Users to Groups</h3>
<p>1. Double-click on the Group and go to Members tab</p>
<p align="center"><img src="https://i.imgur.com/2O2Gamm.png" height="50%" width="50%" alt="image"/>

<p>2. While on the Members Tab, click on Add </p>
<p align="center"><img src="https://i.imgur.com/1veIP9e.png" height="50%" width="50%" alt="image"/>

<p>3. On the “Select Users, Contacts, Computers, Server Accounts or Groups” screen, in the “Enter the object names to select” box, type in the name and click on check names, then click OK</p>
<p align="center"><img src="https://i.imgur.com/wBi0wPG.png" height="50%" width="50%" alt="image"/>

<p>4. Next you can see the name shown in the Member’s tab, click Apply, then click OK</p>
<p align="center"><img src="https://i.imgur.com/QXSpavs.png" height="50%" width="50%" alt="image"/>

<h3>*To add a user to more than one or multiple groups.</h3>
<p>1. Right click on the user and click on Add to a group</p>
<p align="center"><img src="https://i.imgur.com/vAQIvXP.png" height="50%" width="50%" alt="image"/>

<p>2. On the select groups screen, enter all the group names in the “Enter the object names to select” box, all seperated by a semi-colon, then click check names to verify and click OK to finish</p>
<p align="center"><img src="https://i.imgur.com/KbMXyU0.png" height="50%" width="50%" alt="image"/>

<p>3. You are shown “The Add to Group operation was successfully completed” message.</p>
<p align="center"><img src="https://i.imgur.com/Y5VEIKP.png" height="50%" width="50%" alt="image"/>

<p>4. To verify user is added to all group, right-click on the user and go to properties, then click on Member Of. You can all the groups this user belongs to</p>
<p align="center"><img src="https://i.imgur.com/TQIaMx1.png" height="50%" width="50%" alt="image"/>

<br>

<h3>*Verify login newly created Users</h3>
<p>1. Sign out of any existing account in the client's computer and type the username and password of the new user created in the OU</p>
<p align="center"><img src="https://i.imgur.com/WD4PM0O.png" height="50%" width="50%" alt="image"/>

<p>2. You are greeted with the message “The user’s password must be changed before signing in, click OK</p>
<p align="center"><img src="https://i.imgur.com/LWzNMX6.png" height="50%" width="50%" alt="image"/>

<p>3. Type in the new password and confirm password ,then hit Enter</p>
<p align="center"><img src="https://i.imgur.com/Ag0Vbw1.png" height="50%" width="50%" alt="image"/>

<p>4. You can then see the password has been changed, click OK and you are in</p>
<p align="center"><img src="https://i.imgur.com/lnr6Rtm.png" height="50%" width="50%" alt="image"/>

<br>
<br>
<br>

<h1>Using Windows Powershell</h1>

<h3>*Create Organizational Units (OUs) using Powershell</h3>
<p>To create an OU using powershell, I type the following command <b><i> “New-ADOrganizationalunit -name Edmonton -Path “DC=Adeniyi,DC=Com”</i></b></p>
<p align="center"><img src="https://i.imgur.com/y0bS0Zg.png" height="50%" width="50%" alt="image"/>

<h3>*Create Group using Powershell</h3>
<p>To create a group in an OU, I used the following command to create an E_Marketing security group in the Edmonton OU I created earlier <b><i>“New-ADGroup -name “E_Marketing” -Path “OU=Edmonton,DC=Adeniyi,DC=Com”</i></b>.</p>
<p align="center"><img src="https://i.imgur.com/DHDu1wj.png" height="50%" width="50%" alt="image"/>

<h3>*Create Users using Powershell</h3>
<p>To create a user in Edmonton OU, I used the following command;  <b><i>“New-ADUser -name "Karu Jaru" GivenName “Karu.Jaru” SAMAccountName “Karu.Jaru” UserPrincipalName “Karu.jaru@adeniyi.com” -AccountPassword (ConvertToSecureString "Newuser123!" -AsPlainText -Force) -path "OU=Edmonton,DC=Adeniyi,DC=com" -PassThru | Enable-ADAccount”</i></b>.</p>
<p align="center"><img src="https://i.imgur.com/Hm8HcA9.png" height="50%" width="50%" alt="image"/>

<h3>*Add Users to Specified Groups using Powershell</h3>
<p>Now to add the user to specified groups, I used this command; <b><i>“Add-ADGroupMember -Identity E_marketing -Members Karu.Jaru”</i></b>.</p>
<p align="center"><img src="https://i.imgur.com/IMWxDjp.png" height="50%" width="50%" alt="image"/>

<br>

<p>To confirm the user has been added to the E_marketing security group, I clicked Edmonton OU in the Active Directory Users and Computer and go to E_marketing , then click on the Members tab to check and the user is there.</p>
<p align="center"><img src="https://i.imgur.com/VbIa3x4.png" height="50%" width="50%" alt="image"/>

<br>
