<h1>Active Directory Home Lab</h1>

 ### [YouTube Demonstration]

<h2>Description</h2>
In this lab we will create an Active Directory home lab environment on our personal computer utilizing Virtual Box. This lab will resemble a miniature corporate network and can serve as an environment to explore and learn the parameters of Active Directory and Windows networking.
We will create two virtual machines in Virtual Box. The first VM will run on Windows Server 2019 and run the Active Directory Domain Service, acting as a Domain Controller. This DC will have two network interface cards, an external one connected to our home internet (which will use DHCP on our home router to get addressing). The second NIC will be internal and serve as a private network on Virtual Box to which "clients" will be able to connect from our second VM. We will then set up a domain via Active Directory, we will configure NAT and routing and we will set up DHCP on the DC, so the "clients" on our private network can be assigned an IP address and reach the internet through our DC. Finally we will run a PowerShell script to quickly create users, similar to the process of onboarding employees in a corporation. We will then be able to then sign on as a user we created, on the second virtual machine, and access the Internet! 

Configuring and running this lab will definitely help to develop your comprehension of how active directory and windows networking function. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10 Pro</b> (22H2)
- <b>Windows Server 2019</b>

<h2>Program walk-through:</h2>

1. First we will create our first VM with Windows Server 2019 for our Domain Controller. In Virtual Box, select "New", name it "DC". In the settings for the VM, give it 2 GB of ram, 20 GB of storage, and one more processor core to speed it up, if your computer has enough to share. After creating the VM, go to its settings, then in general->advanced, apply bi-directional mouse controls. Next, in the network settings, create two network adapters: one external running NAT and one internal adapter. Finally, start up the VM, mount your .iso for Server 2019, and complete installation, first by selecting "Standard Desktop Experience" and then doing a custom install on our VM storage device. After leaving it alone for few minutes of set up, we will be prompted to create a standard administrator account. Give it an easy, memorable password (e.g. 'Password1') which we will use for every password in this lab (this is OK for a lab environment). After set up is complete, we can log in to our admin account by selecting input->keyboard->CTRL+ALT+Delete: <br/>

<details>

<summary>Expand images</summary>

<img src="https://i.imgur.com/fnPSNHN.png" height="80%" width="80%" />
<img src="https://i.imgur.com/48x4HJe.png" height="80%" width="80%" />
<img src="https://i.imgur.com/1NXEE7U.png" height="80%" width="80%" />
<img src="https://i.imgur.com/EWneNUG.png" height="80%" width="80%" />
<img src="https://i.imgur.com/sdeEgxn.png" height="80%" width="80%" />
<img src="https://i.imgur.com/LqrxpNo.png" height="80%" width="80%" />
<img src="https://i.imgur.com/Oo75jJz.png" height="80%" width="80%" />
<img src="https://i.imgur.com/SBw25Nx.png" height="80%" width="80%" />
<img src="https://i.imgur.com/U9jGN0I.png" height="80%" width="80%" />
<img src="https://i.imgur.com/LY7EV8S.png" height="80%" width="80%" />
<img src="https://i.imgur.com/NfqhYLB.png" height="80%" width="80%" />

</details>

2. After finishing set up of our first VM and logging in, we should see a screen like this. First we will install the Guest Additions add-on to improve the screen responsiveness of the VM, by clicking devices->insert Guest Additions CD image, going to file explorer->PC->Guest Additions Drive and double clicking on the AMD64 edition. Click through the install prompts, and then reboot the VM: <br/>

<details>

<summary>Expand images</summary>

<img src="https://i.imgur.com/vdBHKZT.png" height="80%" width="80%" />
<img src="https://i.imgur.com/NBvnJG8.png" height="80%" width="80%" />
<img src="https://i.imgur.com/HgC3qyY.png" height="80%" width="80%" />

</details>

3. Now we will set up our IP addressing. Go into Network Settings by clicking on the Network icon at the bottom right, and then select "Change Adapter Options". Go to right-click->status->details for each adapter and check whether the IP address is one provided by our home router, or one provided by the VM, and name each adapter accordingly (see images for which is which). Finally, change the IPv4 properties of the internal adapter by going right-click->properties->double-click IPv4 and input the following IP addresses: 172.16.0.1, Subnet Mask 255.255.255.0 and the DNS Server as 172.16.0.1 (home loop address). We do not enter a default gateway here because our Domain Controller itself will serve as a default gateway, and we input the home loop address as the DNS as our DC will use itself as the DNS server after we install Active Directory <br/>

<details>

<summary>Expand images</summary>

<img src="https://i.imgur.com/qnmtxlm.png" height="80%" width="80%" />
<img src="https://i.imgur.com/XV9IN8e.png" height="80%" width="80%" />
<img src="https://i.imgur.com/pUQLApr.png" height="80%" width="80%" />
<img src="https://i.imgur.com/OEWMqIq.png" height="80%" width="80%" />
<img src="https://i.imgur.com/oVqRsYl.png" height="80%" width="80%" />

</details>

4. Rename the PC to something clear such as DC for Domain Controller. Restart the VM and log in again: <br/>

<details>
<summary>Expand images</summary>

<img src="https://i.imgur.com/bkJ8zsw.png" height="80%" width="80%" />

</details>

5. Now we will install Active Directory Domain Services and create a domain. First in Server Manager, click on 'Add roles and features' and click next twice, then select our VM 'DC' to be our server. Next in Server Roles, select 'Active Directory Domain Services' and then click through to install this role. : <br/>

<details>

<summary>Expand Images</summary>

<img src="https://i.imgur.com/EIX5l1i.png" height="80%" width="80%" />
<img src="https://i.imgur.com/ZNfHp68.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/vO0GrYq.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/5sJTalr.png" height="80%" width="80%" />

</details>

6. After installation of AD/DS, click the flag and select "promote the computer to a domain" to create and configure the domain, selecting "add new forest" and entering "mydomain.com" or something similar: <br/>
<img src="" height="80%" width="80%" />


7. After restarting, we will create our own domain admin account. Select the Start menu, and in the Windows Administrator Tools folder, open "Active Directory Users and Computers". In the mydomain.com folder, create a new Organizational Unit and name it "_ADMINS" or something similar. Finally, create a user (yourself), and then in the "Member Of" folder of their properties, enter "domain admins" and add to create a domain admin account:<br/>
<img src="" height="80%" width="80%" />


8. You should now see the user in the _ADMINS folder<br/>
<img src="" height="80%" width="80%" />


9. Now we will set up Routing and Remote Access for our Domain Controller. First, select "Add Roles and Features" and select our server and then "Remote Access" for the role. On the Role Services, select "Routing" and install the role.   <br/>
<img src="" height="80%" width="80%" />


10. To figure the role, click on tools at the top right of Server Manager and select "Routing and Remote Access". Right click on our DC in left column of the window, and select "Network Address Translation" NAT on the configuration page. Finally select the "_INTERNET_" to use this public interface to connect to the Internet: (This part may require trying to open the windows twice if the adapters do not appear): <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />

<p align="center">
 <br/>
<img src="" height="80%" width="80%" />






<br />
<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
