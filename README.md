<h1>Active Directory Home Lab</h1>

 ### [YouTube Demonstration]

<h2>Description</h2>
In this lab we will create an Active Directory home lab environment on our personal computer utilizing Virtual Box. This lab will resemble a miniature corporate network and can serve as an environment to explore and learn the parameters of Active Directory and Windows networking.
We will create two virtual machines in Virtual Box. The first VM will run on Windows Server 2019 and run the Active Directory Domain Service, acting as a Domain Controller. This DC will have two network interface cards, an external one connected to our home internet (which will use DHCP on our home router to get addressing). The second NIC will be internal and serve as a private network on Virtual Box to which "clients" will be able to connect from our second VM. We will then set up a domain via Active Directory, we will configure NAT and routing and we will set up DHCP on the DC, so the "clients" on our private network can be assigned an IP address and reach the internet through our DC. Finally we will run a PowerShell script to quickly create users, similar to the process of onboarding employees in a corporation. We will then be able to then sign on as a user we created, on the second virtual machine, and access the Internet! 

Configuring and running this lab will definitely help to develop our comprehension of how active directory and windows networking function. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10 Pro</b> (22H2)
- <b>Windows Server 2019</b>

<h2>Program walk-through:</h2>

1. First we will create our first VM with Windows Server 2019 for our Domain Controller. In Virtual Box, select "New", name it "DC". In the settings for the VM, give it 2 GB of ram, 20 GB of storage, and one more processor core to speed it up, if your computer has enough to share. After creating the VM, go to its settings, then in general->advanced, apply bi-directional mouse controls. Next, in the network settings, create two network adapters: one external running NAT and one internal adapter. Finally, start up the VM, mount your .iso for Server 2019, and complete installation, first by selecting "Standard Desktop Experience" and then doing a custom install on our VM storage device. After leaving it alone for few minutes of set up, we will be prompted to create a standard administrator account. Give it an easy, memorable password (e.g. 'Password1') which we will use for every password in this lab (this is OK for a lab environment). After set up is complete, we can log in to our admin account by selecting input->keyboard->CTRL+ALT+Delete. <br/>

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

2. After finishing set up of our first VM and logging in, we should see a screen like this. First we will install the Guest Additions add-on to improve the screen responsiveness of the VM, by clicking devices->insert Guest Additions CD image, going to file explorer->PC->Guest Additions Drive and double clicking on the AMD64 edition. Click through the install prompts, and then reboot the VM. <br/>

<details>

<summary>Expand images</summary>

<img src="https://i.imgur.com/vdBHKZT.png" height="80%" width="80%" />
<img src="https://i.imgur.com/NBvnJG8.png" height="80%" width="80%" />
<img src="https://i.imgur.com/HgC3qyY.png" height="80%" width="80%" />

</details>

3. Now we will set up our IP addressing. Go into Network Settings by clicking on the Network icon at the bottom right, and then select "Change Adapter Options". Go to right-click->status->details for each adapter and check whether the IP address is one provided by our home router, or one provided by the VM, and name each adapter accordingly (see images for which is which). Finally, change the IPv4 properties of the internal adapter by going right-click->properties->double-click IPv4 and input the following IP addresses: 172.16.0.1, Subnet Mask 255.255.255.0 and the DNS Server as 172.16.0.1 (home loop address). We do not enter a default gateway here because our Domain Controller itself will serve as a default gateway, and we input the home loop address as the DNS as our DC will use itself as the DNS server after we install Active Directory. <br/>

<details>

<summary>Expand images</summary>

<img src="https://i.imgur.com/qnmtxlm.png" height="80%" width="80%" />
<img src="https://i.imgur.com/XV9IN8e.png" height="80%" width="80%" />
<img src="https://i.imgur.com/pUQLApr.png" height="80%" width="80%" />
<img src="https://i.imgur.com/OEWMqIq.png" height="80%" width="80%" />
<img src="https://i.imgur.com/oVqRsYl.png" height="80%" width="80%" />

</details>

4. Rename the PC to something clear such as DC for Domain Controller. Restart the VM and log in again. <br/>

<details>
<summary>Expand images</summary>

<img src="https://i.imgur.com/bkJ8zsw.png" height="80%" width="80%" />

</details>

5. Now we will install Active Directory Domain Services and create a domain. First in Server Manager, click on 'Add roles and features' and click next twice, then select our VM 'DC' to be our server. Next in Server Roles, select 'Active Directory Domain Services' and then click through to install this role. After the role installs, click the flag and click 'Promote this server to a domain controller'. In the Deployment configuration, select 'Add a new forest', and enter a root domain name such as 'mydomain.com'. Click next, then in domain controller options, enter our password (it won't be used), and click next a few times, then install. After installation, the computer will restart. Log in again, and then we will create out own administrator account. Select Start->Windows Administrative Tools->Active Directory Users and Computers, right-click on the domain and create a new Organizational Unit, naming it 'ADMINS'. Then create a new user, with your name if you wish, and the standard naming protocol of 'a-(first-initial)(last-name)'. Then give it the password and uncheck the recreate password box. Next, we will create this account as an Admin by going to right-click->properties->Member Of->Add and enter 'domain admins', then select check names, and click OK then Apply. Now we have a domain admin account. Finally, we will log out and log in to this account. 

<details>

<summary>Expand images</summary>

<img src="https://i.imgur.com/EIX5l1i.png" height="80%" width="80%" />
<img src="https://i.imgur.com/ZNfHp68.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/vO0GrYq.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/5sJTalr.png" height="80%" width="80%" />
<img src="https://i.imgur.com/WXBDLkf.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/kV1fod1.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/vKHvYg4.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/X2aFb7z.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/gmkj3Wt.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/Cm1K418.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/mj4LTRQ.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/qBCSyd0.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/ebyzg14.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/VRwA6S7.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/y2BS9L8.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/4XfZ7mn.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/UtCfjWP.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/6WmOf5p.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/H1WdgW4.jpg" height="80%" width="80%" />

</details>


6. Now we will set up RAS / NAT (Remote Access Server and Network Address Translation) to allow the "clients" we will create later to access the internet through our Domain Controller. First in Server Manager, select "Add Roles and Features", select our server and then "Remote Access" for the Server role. Clicking next to the Role Services, select "Routing" and click next a few times to install the role. Next to install NAT for our "clients" to access the internet, we will go to tools->Routing and Remote Access, right-click on 'DC', select 'Configure and Enable Routing and Remote Access", select NAT, select our 'Internet' interface, and hit Finish. We then see our DC server with a green arrow indicating it is totally configured (This part may require two tries). 

<details>
 
 <summary>Expand images</summary>
 
<img src="https://i.imgur.com/I2vRgAV.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/cAbvVE6.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/5IEckbg.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/POEQV0Y.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/w9nnh9x.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/atp3irY.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/MUmrO9w.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/W1ZHO1j.jpg" height="80%" width="80%" />
 
 </details>
 
7. The next step is to set up a DHCP server on our domain controller for our Windows 10 clients. We will create a scope of IP addresses and a lease time for our Windows 10 clients to access the internet, just like in an office or a school. First select 'Add Roles and Features' in Server Manager, hit next, select our server (note the name change), select 'DHCP Server' in the Server Roles, click 'add features' and click next a few times and install the DHCP role. After that is installed, we will set up our scope. Select tools->DHCP to open the DHCP control panel, right-click on IPv4 (note it is currently down) and select 'new scope' to open the creation wizard. We might name the scope '172.16.0.100-200'. Click next and then enter the start and end IP addresses of our scope, and the address /24 for the subnet mask. Select next to pass through the exclusions which we aren't using, and keep the standard 8-day IP address lease duration. Lastly, in the DHCP control panel, right-click the dc.mydomain.com server and hit 'authorize'. We now see the our server's IPv4 up and running with the scope configured. Finally, now that DNS is set up, to improve browsing, in Server Manager, select 'Configure this local server', then click 'on' next to Security Configuration and turn it off for Administrators and Users. 
 
 <details>
  
  <summary>Expand images</summary>
  
<img src="https://i.imgur.com/81P2MTl.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/9foLi8d.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/3i5JEOa.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/e8Gp4Nr.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/RRvffsC.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/oHC7WC0.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/1QrSC2F.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/DAc9S7u.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/lCJJnMQ.jpg" height="80%" width="80%" />
  <img src="https://i.imgur.com/PoAwyvL.jpg" height="80%" width="80%" />

 </details>
 
 8. Now we will use a PowerShell script to quickly create ~1000 users on our Active Directory. This will give us some practice using PowerShell and scripting. First we will open Windows PowerShell ISE as an administrator. Then we will open our PowerShell script in the folder to which we have downloaded it on our VM (desktop in this case). Next we will use the command 'Set-ExecutionPolicy Unrestricted' to allow us to run our script. Then we will use the Change Directory Command to go to the folder where our script and folder is located, in this case 'cd C:\Users\a-sjbit\Desktop\*folder*\*folder*' and use the ls command to list the files in the folder. After we verify we are in the folder with the script, we can press play and run the script to create our users. After the script runs, we can go to Start->Windows Administrative Tools->Active Directory Users and Computers to see the users which we have created. This is similar to onboarding new employees in a corporate network. 
 
 <details>
 
 <summary>Expand images</summary>
 
<img src="https://i.imgur.com/n4oiyEk.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/gaEPUrl.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/gYpP0Fi.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/HkMc39q.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/e3QGcjp.jpg" height="80%" width="80%" />
<img src="https://i.imgur.com/tLF1M7f.jpg" height="80%" width="80%" />

</details>

9. Our final step is to create our client computer, which will be given an IP address and access the internet through our DC. First we create a new VM in VirtualBox, assigning it a sufficient amount of processors, RAM and storage. Then we adjust the settings of our VM to include bi-directional mouse controls and choose an internal network for the network adapter. Then we mount the .iso of Windows 10 we downloaded and install the operating system. During installation, be sure to select Windows 10 Pro (otherwise we will not be able to access the domain) and select 'I don't have a product key' and make a local account (selecting 'I don't have internet'), naming it 'user' and don't use a password. After installation has finished, right click on the start button, select system, and go to 'rename this PC (advanced)'. In the system properties panel, select 'change' and name the computer 'CLIENT1', then click domain and enter our domain name, 'mydomain.com'. After clicking OK you will be prompted to enter administrator credentials from our DC. After entering those, the computer will restart. On the sign in screen, we can choose a user we created from our DC, then we can log in to our domain, just as we would on a corporate network or a school. Back on our DC, we will now see our "client" has been given an IP address lease (in Server Manager->tools->DHCP). Finally, back on our client computer, we can run 'ipconfig' and 'ping google.com' to see that we have full access to the internet through our DC. Our lab is now hopefully functioning just as our initial diagram, and we can explore our set up!

<details>
 
 <summary>Expand images</summary>
 
 <img src="https://i.imgur.com/lfNZZfH.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/LjFfxeX.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/1O2CGN9.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/WnDyHuh.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/jeyhjSE.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/vnUZtGd.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/pjY0c4Z.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/vcnGNrT.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/Shwq21h.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/D9Ub8vq.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/3nr5ZS8.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/7YLcVgp.jpg" height="80%" width="80%" />
 <img src="https://i.imgur.com/DYr7QbS.jpg" height="80%" width="80%" />
 
 </details>
 

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
