<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines creating a domain controller virtual machine as well as a client virtual machine to join domains and access information on the domain controller.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Resource Group
- Virtual Network
- Firewall
- Ping

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/8RzNJt6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a Resource Group in Azure.
</p>
<br />

<p>
<img src="https://i.imgur.com/6zyol9J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create the Domain Controller and Client virtual machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/o7usMKS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go into the Domain Controller virtual machine, Into the network settings and set the Domain Controller IP address to static.
</p>
<br />

<p>
<img src="https://i.imgur.com/wQIlQdF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to the Domain Controller's virtual machine with the username and password created earlier.
</p>
<br />

<p>
<img src="https://i.imgur.com/lqqpx15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside the virtual machine, right clcik the start menu and type wf.msc to get to the firewall settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/4zunIKz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After clicking into "Windows Defender Firewall Properties", turn off the firewall state for the Domain, Private, and Public Profiles.
</p>
<br />

<p>
<img src="https://i.imgur.com/eh9ZCqE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Get the domain controllers private IP address and go into the clients virtual machines network settings and change the DNS server to the domain controllers private IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/qsxvtCy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside the clients virtual machine, open PowerShell and attmep to ping the domain controller by typing ping and then the domain controllers private IP address.
</p>
<br />
