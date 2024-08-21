<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Prepping for On-premises Active Directory (AD) Deployed in Azure</h1>
This tutorial outlines the steps necessary to ultimately deploy on-premises AD within Azure.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a Resource Group
- Create a Domain Controller Virtual Machine (VM)
- Create a Client VM
- Set the Domain Controller's NIC private IP address to static

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/nQF6Jh6.png" height="80%" width="80%" alt="RG Creation"/>
</p>
<p>
Go to portal.azure.com. Either select "Resource Group" from Azure Services or begin typing "Resource Group" in the search bar at the top. Click "+ Create." Give your Resource Group a name, and select the region in which you want your Resource Group to reside. Select "Review + create," and allow sufficient time for its creation (notice the notification bell at that top of the page). This Resource Group will contain the following resources.
</p>

<p>
<img src="https://i.imgur.com/LIJBHjw.png" height="80%" width="80%" alt="VM Creation"/>
<img src="https://i.imgur.com/IZm1qcf.png" height="80%" width="80%" alt="VM Options"/>
</p>
<p>
While still in Azure, select "Virtual Machine" from Azure Services, if shown, or begin typing "Virtual Machine" in the search bar at the top. Click "+ Create" and select the "Azure virtual machine" option. Make sure the correct Subscription is shown, in the event you have more than one, and select the Resource Group in which you want your VM to reside. Give your VM a name (e.g., DC-1), and select a region. You are able to select a different region than the Resource Group if all machine sizes are not available, but your VMs and virtual network must be in the same region to ensure reliable communication. For "Image," select the type of VM you are creating from the drop-down menu. For this demonstration, select Windows Server 2022 Datacenter (name DC-1), then Windows 10 Pro, version 22H2 (name Client-1). For "Size," select enough vcpus and memory to meet your needs; more speed costs more money. When creating the VMs, set the username and password to something you'll remember. Other default settings should be fine for our purposes.
</p>
<br />

<p>
<img src="https://i.imgur.com/3zYni3e.png" height="80%" width="80%" alt="Virtual Network Creation"/>
</p>
<p>
During the course of creating your first VM, you will create a Virtual Network. Select "Networking" at the top of the page or click "Next" at the bottom until you arrive at "Networking" settings. While creating your first VM, you can allow a Virtual Network to be created automatically, along with a Public IP. If you prefer a specific name, enter it in the "Virtual network" field. However, when you create your second VM, you will need to select the Virtual Network that was created with the first VM. The pic above shows the second VM being created (notice the new Public IP), with the first Virtual Network chosen from the drop-down menu. If you do not allow enough time for the first VM/resource to be deployed in Azure, you may not see the originally-created Virtual Network available to be selected. Allow more time before proceeding as your VMs will not be able to communicate with one another.
</p>
<br />

<p>
<img src="https://i.imgur.com/1MkgJl0.png" height="80%" width="80%" alt="Resource Group View"/>
<img src="https://i.imgur.com/PrFpgCd.png" height="80%" width="80%" alt="IP Configuration"/>
<img src="https://i.imgur.com/aZx8PzA.png" height="80%" width="80%" alt="Edit IP Configuration"/>
<img src="https://i.imgur.com/xsHQpw5.png" height="80%" width="80%" alt="Setting as Static"/>
</p>
<p>
After creating both VMs and the one Virtual Network, you click "Home" or re-enter the portal.azure.com URL. Select your Resource Group. What you see above (the first of four) are the Resource Group resources that were created. We are going to change the Domain Controller's IP address to static, and you can get there a couple of ways. In the RG, you can select DC-1 Virtual machine > Network Settings > Network Interface. Or, you can click the resource identified in the Resource Group under "Type" as "Network Interface" (in the top pic, you would select "dc-1927_z1"). When in the Network Interface, select "IP Configurations" on the left (the second of four). Click "ipconfig1," which will display the "Edit IP configuration" window (the third of four). Select the "Static" radio button (the fourth of four). This will allow the Client-1 VM to still be able to connect to the Domain Controller should the resources be utilized over multiple days, as the DC could be issued a new IP address without our intervention. You are now able to connect to each VM, install Active Directory on DC-1 (https://lazyadmin.nl/it/active-directory-users-and-computers/), and conduct any desired network activities.
</p>
<br />
