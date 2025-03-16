<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

<p>
</p>
<p>
In this lab we will create two VMs in the same VNET. One will be a Domain Controller (Domain-Controller), and the other will be a Client machine ( Device-1). We will change the DC to a static IP because its offering Active Directory services to the client machine. The client machine will be joined to the domain. We will control the DNS settings on the client machine, the client machine will use the Domain Controller as its DNS server. 
</p>
<br />

<p>
<img src="https://i.imgur.com/d22FHIm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC-1 has to have a static Private IP Address. Client one will connect to DC-1 to ensure connectivity we will try to ping  Domain Controller-1 from Devie-1. At first, the ping will not work correctly. We have to enable ICMPv4 on the firewall on Domain-Controller. Now we can ping Domain Controller-1 successfully from Device-1
</p>
<br />

<p>
<img src="https://i.imgur.com/HvZBWzc.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/1lrrGPw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Now, we will log back into Domain-Controller to install Active Directory Users & Computers. Promote the VM to Domain-Controller, set up a new forest as "mydomain.com," and afterwards restart and then log back into Domain-Controller as user "mydomain.com\Teach". If you performed the steps properly, you should be able to run AD Users & Computers, as shown below.
</p>

<br />
</p>
Excellent! We can start creating Organizational Units (OU). Let's first create an OU named _EMPLOYEES. Create another OU named _ADMINS. To do that, right-click on the domain area. Select New ->Organizational Unit and fill out the field. Then click inside of your OU and right-click, select new and select user, and fill out the information for your new user. The user should be named Kayla Lewis. She is going to be an Admin, so her username will be kayla_admin. Lastly add Kayla to the domain admins security group. 
</p>

<br />
</p>

From now on, you can use kayla_admin as the administrator account. Now, we will join Device-1 to the domain (mydomain.com) from the Azure portal. We will change Device-1's DNS settings to the Domain Controller's Private IP address. After you do that, restart Device-1 from within the Azure portal. Our picture below shows verification that device-1 is on the Domain-Controller DNS. 
</p>

<br />
</p>

</p>
<p>
</p>
<p>
We have to join Client-1 to the domain to do so, navigate to your system settings and go to about. Off to the right, select rename this pc (advanced). From there, select to change the domain. Enter "mydomain.com" After that, enter your credentials from mydomain.com\Teach. Your computer will restart, and then device-1 will be a part of mydomain.com
</p>
<br />
<p>
  <p>
<img src="https://i.imgur.com/Ze0Em5e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, Device-1 is a part of the domain. Set up a remote desktop for non-administrative users on Device-1. We have to log into Device-1 as an admin and open system properties. Click on "Remote Desktop" and allow "domain users" access to the remote desktop. After completing those steps, you should be able to log into Device-1 as a user.
</p>
<br />

<p>
  <p>
<img src="https://i.imgur.com/SApOKiE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, to verify that regular users can RDP into Device-1 we will use a script to generate thousands of users into the domain. We will input the script in powershell; after the users are created we will select one and RDP into Device-1.
</p>
<br />
<img src="https://i.imgur.com/EzWG8ug.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<p>
  <p>
<img src="https://i.imgur.com/Gkpe68K.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/n3gMwQV.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
As you can see, the Powershell script created a user with the username "gar.visen" We were able to login to Deive-1 with his credentials as a regular user. 
</p>
![image](https://github.com/user-attachments/assets/f697ca18-a8b2-4ce0-931c-bca690eb3391)

![image](https://github.com/user-attachments/assets/38182ec6-839a-406d-b672-0dce7910da92)

![image](https://github.com/user-attachments/assets/c4534db4-a951-48f7-b4b4-60e65619f57c)

![image](https://github.com/user-attachments/assets/e7bbe8d6-dfec-4f88-9a62-2851388f2c15)

![image](https://github.com/user-attachments/assets/4965abca-a3e1-4293-8cf5-187b0d3941ad)

![image](https://github.com/user-attachments/assets/e4405ccd-0c00-41ba-a858-9db7e4c79b21)

![image](https://github.com/user-attachments/assets/393a1612-9f7a-428a-8923-ef103b07e038)

![image](https://github.com/user-attachments/assets/e1f9a872-a425-4366-80d2-b7530281d32b)

Right-click on the start menu
![image](https://github.com/user-attachments/assets/038794a3-eb9c-485b-8dd9-19e388a0e3eb)

windows firewall
![image](https://github.com/user-attachments/assets/f3ce3d75-ffd5-455f-9b90-311cf1252333)

![image](https://github.com/user-attachments/assets/ddd1c960-49d3-4e37-bb1e-aad7e9371794)


![image](https://github.com/user-attachments/assets/8808b9d6-0e82-40be-a88d-57898d59e41d)

![image](https://github.com/user-attachments/assets/44cdfd9d-0013-4dfb-a659-8feb306c7929)


![image](https://github.com/user-attachments/assets/9d63400a-08af-479b-95cc-ffe56ae1b8f8)

![image](https://github.com/user-attachments/assets/2bbf3da6-a8f9-43da-bb0d-eec7c20f06e9)

![image](https://github.com/user-attachments/assets/96935f01-a8ce-475b-822c-9c98bf4359eb)


![image](https://github.com/user-attachments/assets/15ad75ad-2d7c-4601-823c-370bf61d3dc2)


![image](https://github.com/user-attachments/assets/23e80abe-9259-4899-9e63-6dc42104fe84)


![image](https://github.com/user-attachments/assets/316ca738-6f7c-48f3-84bf-0040c59df1a6)

![image](https://github.com/user-attachments/assets/f993e0b1-2c82-4434-be22-a883dd8bbca1)

![image](https://github.com/user-attachments/assets/50616f4d-95fd-46cf-b707-c3abca51d165)

![image](https://github.com/user-attachments/assets/6b51b5d8-f153-4755-b514-4c6d997a2bab)

![image](https://github.com/user-attachments/assets/ec7ede08-0cf1-4fab-911c-e89fdb5f5d70)

![image](https://github.com/user-attachments/assets/db428345-9c91-4db2-a7b0-3a7108e8fe92)

![image](https://github.com/user-attachments/assets/654f93d0-5b46-4ea9-8d3c-f261166809f7)


![image](https://github.com/user-attachments/assets/f40b504a-bc86-48c7-985e-f85c4727687b)

![image](https://github.com/user-attachments/assets/7d8212ea-9417-4b90-9a70-9ba1b6e54d84)
![image](https://github.com/user-attachments/assets/b5f3ee90-47dc-457a-bef2-3905169ff811)

![image](https://github.com/user-attachments/assets/44b602d4-94fc-4c8d-9ea0-64a9a0b6c684)

![image](https://github.com/user-attachments/assets/cbda33fc-e0d9-4561-9a48-0da2965ec2f1)
 The Domain Controller will automatically restart.
Login using username mydomain.com\Teach
![image](https://github.com/user-attachments/assets/c3634d17-c92f-4dc1-aa2b-d5036804bc1c)

![image](https://github.com/user-attachments/assets/4106fb82-c560-4534-ab06-99fc148033c3)
![image](https://github.com/user-attachments/assets/c7a83f57-a3fc-44f1-bd7f-09eeed11c790)

![image](https://github.com/user-attachments/assets/ecb2230b-0f50-44ef-b4ae-b4339a03e8e1)

![image](https://github.com/user-attachments/assets/8e30397c-63a3-487a-9383-f4ddd24f8b6e)
![image](https://github.com/user-attachments/assets/fccfe012-7f57-4200-b385-65bc5ffdc856)

![image](https://github.com/user-attachments/assets/65a1f519-0fca-4f57-a618-5fdbe89afa13)

![image](https://github.com/user-attachments/assets/ca3108e9-1896-4916-8be4-157272a1336e)
![image](https://github.com/user-attachments/assets/97fc17d9-af3f-4159-9e1d-2450cafe66ca)
Password: Password1

Now join device 1 to domain

![image](https://github.com/user-attachments/assets/1b215bcc-7d59-4568-bc2a-08b6eb485b22)

![image](https://github.com/user-attachments/assets/6edebd65-a7db-4785-9d93-9b9964acb65d)
![image](https://github.com/user-attachments/assets/4cd37995-a5ed-4836-844e-10adde707191)

![image](https://github.com/user-attachments/assets/fd185a16-fc50-4c65-b362-67c197272a1e)

![image](https://github.com/user-attachments/assets/f0f96371-e359-4880-8154-779dcd2c76b6)

Check to see if device-1 is in the domain computers 
![image](https://github.com/user-attachments/assets/5257c48f-d214-4087-99b7-58b4f5a77645)



In Domain Controller, drag Device-1 from Computers into _CLIENTS
![image](https://github.com/user-attachments/assets/433631cf-80b9-45f7-bdb7-e732e22f5566)

![image](https://github.com/user-attachments/assets/565536bf-155c-4fb9-8350-9ed71fbc4c60)

In Device-1, log in using kayla_ admin credentials

![image](https://github.com/user-attachments/assets/25e05d25-8fc6-4f73-9640-7d300ae35ffa)
![image](https://github.com/user-attachments/assets/7e538c1e-6b84-4fda-9894-5b2f3fef39ba)

In Domain Controller, Open Windows Powershell ISE, open a new file, paste script, and save as create users 
![image](https://github.com/user-attachments/assets/809354fd-b363-4ccc-a487-59f6d8cb41e6)

![image](https://github.com/user-attachments/assets/64980667-3f06-4638-9f59-1f10c738a81a)


Open Active Directory Users and Computers > Run > type "dsa.msc"

![image](https://github.com/user-attachments/assets/9d164568-f4af-41b3-8d4c-3ea31d827e05)

Next, configure group policy to lock out the account after 3 attempts:
Run > gpmc.msc
![image](https://github.com/user-attachments/assets/4149a951-b40e-4945-8aee-14fb026011fc)
Account Lockout Duration:
Definition: The time in minutes an account remains locked before automatically being unlocked.
Configuration: Double-click on this setting, select Define this policy setting, and then set the duration (e.g., 30 minutes).
Account Lockout Threshold:
Definition: The number of failed log-on attempts that will trigger an account lockout.
Configuration: Double-click on this setting, select Define this policy setting, and then set the threshold (e.g., 3 invalid attempts).
Reset Account Lockout Counter After:
Definition: The time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed log-on attempts.
Configuration: Double-click on this setting, select Define this policy setting, and then set the time (e.g., 15 minutes).
![image](https://github.com/user-attachments/assets/172844fb-7458-4d68-a4ea-72c8b97f1007)
In Device-1, log in as kayla_admin, open Admins Command Prompt, and type gpupdate /force. Then, check it with gpresult /r
(Run > cmd >CRTL+Shift +Enter)
![image](https://github.com/user-attachments/assets/35d69305-04c4-4936-a27d-9b9df6775684)
![image](https://github.com/user-attachments/assets/ba154c0c-e901-45fa-97d1-91c937d2da12)

In Device, log in as a new user:  mydomain.com\gar.visen, typing random passwords

![image](https://github.com/user-attachments/assets/dc755c9f-79b2-409f-a58d-1e18bf01b75a)

![image](https://github.com/user-attachments/assets/8f20ab9a-7c40-4f2f-bb49-ff9e55c492ab)

In Domain Controller, log in as kayla_admin and unlock gar.visen account
![image](https://github.com/user-attachments/assets/156a6943-db47-4420-a759-8e771074efdf)

![image](https://github.com/user-attachments/assets/80c0e0cc-469a-4173-8e26-f568df786c92)

![image](https://github.com/user-attachments/assets/630eaa9a-929c-4ec5-93ad-718aa7db81d4)

In Device-1, use mydomain.com\gar.visen and Password1 to login.
![image](https://github.com/user-attachments/assets/f7d79d0d-7f93-4fe4-ae3c-dc8f2863d72a)
It works!

Observe logs in n Device-1, Run> eventvwr.msc CTRL+SHIFT+ENTER
Sign in using kayla_admin credentials
![image](https://github.com/user-attachments/assets/fc112815-974a-4ca3-b68d-32b061eb9e78)
![image](https://github.com/user-attachments/assets/d6300ad1-c5aa-4cb1-96b9-e5ccbd164f32)


As an admin in Active Directory, you can do a few things quickly: Disable an account, reset a Password, add a user to a group, etc...
![image](https://github.com/user-attachments/assets/02ba64ad-34f5-4a66-a936-8a2373940124)


I know this was long, but I hope it was helpful. Have a great one!
