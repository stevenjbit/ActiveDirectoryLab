<h1>Active Directory Home Lab</h1>

 ### [YouTube Demonstration]

<h2>Description</h2>
In this lab we will create an Active Directory home lab environment on our personal computer utilizing Virtual Box. This lab will resemble a miniature corporate network and can serve as an environment to explore and learn the parameters of Active Directory and Windows networking. 

We will create two virtual machines in Virtual Box. The first VM will serve as a Domain Controller running on Windows Server 2019, enabling us to run Active Directory. This DC will have two network interface cards, an external one connected to our home internet (which will use DHCP on our home router to get addressing). The second NIC will be internal and serve as a private network on Virtual Box to which "clients" will be able to connect from our second VM. We will then set up a domain via Active Directory, we will configure NAT and routing and we will set up DHCP on the DC, so the "clients" on our private network can be assigned an IP address and reach the internet through our DC. Finally we will run a PowerShell script to quickly create users, similar to the process of onboarding employees in a corporation. We will then be able to then sign on as a user we created, on the second virtual machine, and access the Internet! 

Configuring and running this lab will definitely help to develop your comprehension of how active directory and windows networking function. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (22H2)

<h2>Program walk-through:</h2>

<p align="center">
Setting up our first VM to serve as our DC: <br/>
<img src="https://i.imgur.com/j7zvtyN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
