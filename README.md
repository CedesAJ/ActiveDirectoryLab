# ActiveDirectoryLab

First, create a new resource group and name it "ActiveDirectoryLab".

<br>Next, create a new virtual network and name it "ActiveDirectoryVnet".
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/f6eca432-63e6-46ef-98e0-1f092d355959" />

<br>Create a virtual machine name "dc1" with Windows Server 2022 and install it to the "ActiveDirectoryLab" resource group and "ActiveDirectoryVnet" network. Use "labuser" as the username and create a password. Review and create the virtual machine.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/e68bf12f-4733-4748-b646-1edb97216e73" />

<br>Create a virtual machine name "client1" with Windows 10 and install it to the "ActiveDirectoryLab" resource group and "ActiveDirectoryVnet" network. Use "labuser" as the username and create a password. Review and create the virtual machine.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/601dfd73-5654-4d47-80c8-bdce1bb08b8d" />

<br>Change the "dc1" NIC to a static IP. First go to the virtual machines in Azure. Then, select "dc1". Select "Network Settings". Select "ipconfig" at the top with the green NIC picture then select "ipconfig1" link. On the right under Private IP address settings under allocation, select "Static"  and "Save".
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/d907de47-4eff-4a75-936e-6b8cd43a39cb" />

<br>Next, connect to "dc1" using Remote Desktop Connection and entering the public ip address.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/e420d9d1-45ec-4258-a0ae-4913f17b2a7e" />

<br>Disable Windows Firewall. Cllick the start button then select run and type "wf.msc". Click on the Windows Defender Firewall Properties and turn off in all the tabs and click "Apply" and "OK"

<br>Point the virtual machine "client1" to look up DNS on "dc-1" by setting the DNS server as the Private IP of "dc1". Click on virtual machines in the Azure portal and select "client1" and then "Network Settings". Then click on the NIC at the top labeled as "ipconfig1". Select the DNS Servers then select the "Custom" bullet under DNS servers and enter the Private IP address of "dc1" then click "Save" at the top.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/fd5558df-13fb-4f9a-a94d-e1cdc39fc5c3" />

<br>Restart "client1".
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/18e79841-5253-4680-be1d-a0d999cb7fa8" />

<br>Log into the "client1" virtual machine using Remote Desktop Connection.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/d94dc709-af8b-4fbd-924b-7092df7cc9bd" />

<br>Ping "dc1" private address to test the connection.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/0be6997e-9901-41c3-8d38-6b1e6772b5b7" />

<br>Look at the DNS Server information by using "ipconfig /all".
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/0ee9a8c3-899e-49da-a030-21d5f5a5f279" />

<br>Now, set up the Active Directory Services on "dc1". Connect to "dc1". Click on the start button and select "Server Manager". Click on "Add roles and features" and "Next" three times. Check the box for "Active Directory Domain Services" and select "Add Features". Keep pressing "Next" until you can't anymore. Check the box to "Restart the destination server automatically. 
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/254d44fb-a612-4c15-a45c-c9062902f667" />

<br>Now promote "dc1" to a "Domain Controller". Click on the flag icon and click on the link to promote server to a domain controller. Next click the bullet by "Add a new forest" and type "mydomain.com". Select the "Next" button. Enter a password and click "Next". Uncheck the box by "Create DNS delegation" then click the "Next" button. Keep clicking the "Next" button until you can't anymore. Then select the "Install" button. After installation is complete the virtual machine will restart.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/8aef9b35-aead-4c38-b47e-4b00de7ac51f" />

<br>Connect to “dc1” by using "mydomain\labuser" as the username.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/087fa5f5-41df-4634-b5d8-9537fa2009f6" />

<br>Create a new "Organizational Unit" in active directory called "_EMPLOYEES". 
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/369bd86d-ebcb-4a4a-a6b2-6d511f1c4183" />

<br>Create a new "Organizational Unit" in active directory called "_ADMINS". 
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/48d00da9-86de-4d88-8dd0-122937a9bc7e" />

<br>Add a new user in Active Directory named "Jane Doe" under the "_ADMINS" directory and use “jane_admin” as the username.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/e8291ae3-487d-4c64-b4e6-fa187e03eba7" />

<br>Make "Jane Doe" a Domain Admin. Click on "Jane Doe" and select "Properties". Next, click on the "Member Of" tab and click "Add". Then type "Domain Admins" in the object name box and click "Check Names". Then click the "OK", "Apply" and "OK". Right click on the start button and select "Run" then type "logoff".
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/3c3fd17e-3af3-402a-bd34-5d8a7680aa1e" />

<br>Log on to "dc1" as "jane_admin".
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/47c44c15-514e-4594-b982-0aa45ac90133" />

<br>Now join "client1" to the domain. Log into "client-1". Right click on the start button and select "System", "Rename this PC", and "Change". Click the "Domain" bullet. Type "mydomain.com" and click on the "OK" button. When a pop up window appears, enter "jane_admin" credentials . Once completed, the virtual machine will restart.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/a511627b-b01b-4269-975f-632a76248ef0" />

<br>Now log into "dc1" and create a new tree in the Active Directory called "_Clients". Click on the start button. Then select the "Windows Administrative Tools" and select "Active Directory Users and Computers". Once opened right click on "mydomain.com" drag down to "New" and select "Organinizational Unit". In the name field type "_CLIENTS" and click the "Ok" button at the bottom.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/27412458-28e7-4e87-b795-cc9c06fcfd87" />

<br>Next, allow domain users remote access to "client1". Reconnect to "client1" through Remote Desktop Connection and use "mydomain.com\jane_admin" as the user. Once logged in, right click on the start button and click on "System". On the right click on the "Remote Desktop" link. Click on the "Select users that can remotely access this PC" link at the bottom. Click on the "Add" button the type "Domain Users" in the field and select "Check Names" then click the "OK" button.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/1baf7865-b91b-4ff6-a4f7-132df40028e8" />

<br>Create multiple users to the domain by using a script. Log back into the "dc1" as "mydomain\jane_admin". Open Windows Powershell ISE and run it as an administrator. Then, copy the script below. in Windows Powershell ISE click on the "New Script" button and paste the script code into the script field. Then click on the "Run Script" button.
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/5e2e06dd-3c89-4f61-811f-97cbedc5b882" />

<br>Now, view the added new users in the "_EMPLOYEES" folder in Active Directory. 
<img width="1432" height="805" alt="image" src="https://github.com/user-attachments/assets/e0b6c056-484e-4b17-ae55-e7351ed3c186" />

<br>Next in the "client1" virtual machine log out of "jane_admin" and log into "client1" as a random employee under "_EMPLOYEES". In the script all passwords for every user is "Password1".

<br>Next, configure the group policy to allow for accounts to be locked out. Connect to "dc1" using the Remote Desktop Connection. Once logged in, right click on the start button then select "Run" and then type "gpmc.msc" and hit enter. Click the drop down arrow for the "Forest: mydomain.com" then the drop down arrow for "Domains" then again with "mydomain.com". Right click on "Default Domain" and select "Edit". Navigate to Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy. Double click "Account lockout threshold" and enter "5" for invalid logon attempts then click "OK" at the bottom.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/26026194-d792-471e-b4ce-0706b818f0d4" />

<br>Now go back to "client1" and update the Group Policies in a command line. Right click on the start button and select "Run" then type "cmd" and hit enter. In the command line type "gpupdate /force". It should now update the group policies to "client1". Right click the start button then 
 "Run" and type "logoff".
 <img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/02df685c-5448-47d8-9462-fa418772f4fe" />

<br>Now test the new Group Policy by logging on "client1" with a random user from the "_EMPLOYEES" folder in Active Directory earlier. Attempt to log on as this user in Remote Desktop Connect and purposefully enter a wrong password six times and see if you get it locked out.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2ca9f5ef-81a6-4a68-b759-135ef6899138" />

<br>Next, unlock the account and log in with the correct credentials. Log back into "dc1" and find the user in Active Directory. When logged in click on the start button, "Windows Administrative Tools", "Active Directory Users and Computers". Navigate to the "_EMPLOYEES" folder and find the user and double click on the user. Then click on the "Account" tab and check to box "Unlock Account" then click "Apply" and then click "OK"
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2826eb4b-bf79-4268-a5dd-31d96ebfbaf0" />

<br>Log back into "client1" with the correct credentials for the user's account we just unlocked.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2d17b240-369a-445e-8901-916ed3f42a2c" />


<br>Now perform a password reset on a user within Active Directory on "dc1". Log back into "dc1" and find the user in Active Directory. When logged in click on the start button. Then select the "Windows Administrative Tools" and select "Active Directory Users and Computers". Navigate to the "_EMPLOYEES" folder and find the user and right click on the user then select "Reset Password". Enter in the new password and then press "OK"
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c6d12eeb-8975-490a-a5a3-0dc599a74737" />


<br>Now view the events in Event Viewer to see the failed log in attempts by the user's account we unlocked earlier.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/899f8545-eb1d-4e98-bf13-82faef749604" />
