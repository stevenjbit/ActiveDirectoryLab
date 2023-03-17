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

<p align="center">
1. To set up our first VM with Windows Server 2019 for our Domain Controller. Select "New", name it "DC" and create two network adapters in settings->network, one external running NAT and one internal adapter. Select "Standard Desktop Experience" during Windows installation after mounting the .iso of Windows Server. <br/>
<img src="https://i.imgur.com/j7zvtyN.png" height="80%" width="80%" />

<p align="center">
2. After finishing set up of our first VM and logging in, we should see a screen like this: <br/>
<img src="https://i.imgur.com/HJwevWr.png" height="80%" width="80%" />

<p align="center">
3. Go into Network Settings by clicking on the Network Icon at the bottom right, and then select "Change Adapter Options". Go into the status for each adapter and name it according to whether its IP address is matches our home internet or an internal IP from Virtual Box. Finally, change the IPv4 properties of the internal adapter with IP: 172.16.0.1, Subnet Mask 255.255.255.0 and the DNS as 172.16.0.1 (: <br/>
<img src="https://i.imgur.com/cNxmKkK.png" height="80%" width="80%" />

<p align="center">
4. Rename the PC to something clear such as DC for Domain Controller and restart: <br/>
<img src="https://i.imgur.com/bkJ8zsw.png" height="80%" width="80%" />

<p align="center">
5. On Server Manager, click "add roles and features" and select Active Directory Domain Services to install this role. : <br/>
<img src="https://i.imgur.com/5sJTalr.png" height="80%" width="80%" />

<p align="center">
6. After installation of AD/DS, click the flag and select "promote the computer to a domain" to create and configure the domain, selecting "add new forest" and entering "mydomain.com" or something similar: <br/>
<img src="https://i.imgur.com/uwvvVPx.png" height="80%" width="80%" />

<p align="center">
7. After restarting, we will create our own domain admin account. Select the Start menu, and in the Windows Administrator Tools folder, open "Active Directory Users and Computers". In the mydomain.com folder, create a new Organizational Unit and name it "_ADMINS" or something similar. Finally, create a user (yourself), and then in the "Member Of" folder of their properties, enter "domain admins" and add to create a domain admin account:<br/>
<img src="https://i.imgur.com/Ue39dos.png" height="80%" width="80%" />

<p align="center">
8. You should now see the user in the _ADMINS folder<br/>
<img src="https://i.imgur.com/gUdUaRv.png" height="80%" width="80%" />

<p align="center">
9. Now we will set up Routing and Remote Access for our Domain Controller. First, select "Add Roles and Features" and select our server and then "Remote Access" for the role. On the Role Services, select "Routing" and install the role.   <br/>
<img src="https://i.imgur.com/tLVxNmu.png" height="80%" width="80%" />

<p align="center">
10. To figure the role, click on tools at the top right of Server Manager and select "Routing and Remote Access". Right click on our DC in left column of the window, and select "Network Address Translation" NAT on the configuration page. Finally select the "_INTERNET_" to use this public interface to connect to the Internet: (This part may require trying to open the windows twice if the adapters do not appear): <br/>
<img src="https://i.imgur.com/rFRWGiK.png" height="80%" width="80%" />

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
