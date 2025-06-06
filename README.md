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
This is where I set up a resource group in Azure for my Active Directory lab. I named it Active-Directory-Lab and picked East US as the region. Creating a resource group keeps everything for the project in one place so it's easier to manage later on.
</p>
<br />

<p>
<img src="https://i.imgur.com/6zyol9J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This is where I started setting up the domain controller VM in Azure. I named it dc-1 and placed it under the Active-Directory-Lab resource group I created earlier. It's set to deploy in the East US region and availability zone 1.

This VM will eventually be promoted to a domain controller so I can build out an Active Directory environment. After this, I’ll set up a second VM that acts as a client machine to join the domain and test everything out.
</p>
<br />

<p>
<img src="https://i.imgur.com/o7usMKS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After creating the domain controller VM, I went into its network settings to set a static private IP address. This is an important step for Active Directory setups, since the domain controller needs a consistent IP that client machines can always connect to.

I made sure the VM was connected to the right virtual network and subnet, then locked in the private IP (10.0.0.4) so it won’t change if the VM restarts. 
</p>
<br />

<p>
<img src="https://i.imgur.com/wQIlQdF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>Here I’m connecting to the domain controller VM using Remote Desktop Connection. I entered the public IP address and the username (labuser) that I set up earlier during the VM creation process.

Once logged in, I’ll be able to start configuring the server — including installing Active Directory Domain Services and promoting it to a domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/lqqpx15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once inside the virtual machine, I opened the Run window by right clicking the start menu and typing wf.msc to access the Windows Firewall settings. This command brings up the advanced firewall configuration panel, where I can manage inbound and outbound rules — something needed later when setting up domain and network access between the VMs.
</p>
<br />

<p>
<img src="https://i.imgur.com/4zunIKz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After opening Windows Defender Firewall with Advanced Security, I clicked on "Windows Defender Firewall Properties" to access the settings for each network profile. From there, I turned the firewall off for the Domain, Private, and Public profiles.

This was done temporarily to make sure the VMs can communicate without firewall issues during the domain setup process.
</p>
<br />

<p>
<img src="https://i.imgur.com/eh9ZCqE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, I grabbed the private IP address of the domain controller (which was 10.0.0.4) and went into the client VM’s network settings. Under the DNS settings, I switched from using the default virtual network DNS to custom, and entered the domain controller’s IP.

This allows the client VM to find and communicate with the domain controller for things like domain joining, DNS resolution, and group policy — all key parts of getting Active Directory working correctly.
</p>
<br />

<p>
<img src="https://i.imgur.com/qsxvtCy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside the client VM, I opened up PowerShell and used the ping command to test the connection to the domain controller. I entered its private IP address (10.0.0.4) to make sure the client could reach it over the network.

The replies came back successfully with 0% packet loss, which confirms that the two VMs can communicate — a necessary step before trying to join the domain.
</p>
<br />
