<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Power Shell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Creating a Resource Group with Server and Client
- Configuring TCP Proctols in Windows Firewall
- Installing Active Directory and User Groups
- Connecting Virtual Machine to Cloud Server and Adding Users

<h2>Deployment and Configuration Steps</h2>
<br />
<h3 
<br />
<p>
  

### 1. Create the Domain Controller VM  
- **Virtual Machine Name**: `DC-1`  
- **Operating System**: Windows Server 2022  
- **Network**: Create a new Resource Group and Virtual Network (VNet).  
- **Configuration**: Use Azure's default settings for the VM size (e.g., 2 VCPUs).  

  
![Resource Group](https://i.imgur.com/gaAzjvb.png)  
![VM Configuration - Windows Server](https://i.imgur.com/hubTfey.png)  

---

### 2. Create the Client VM  
- **Virtual Machine Name**: `Client-1`  
- **Operating System**: Windows 10  
- **Network**: Use the **same Resource Group and VNet** created in the previous step.  

  
![VM Configuration - Windows 10](https://i.imgur.com/XyEmv8f.png)  

---

### 3. Configure Static Private IP for the Domain Controller  
- Navigate to the **Networking tab** of the Domain Controller VM in Azure.  
- Set the **Network Interface Card (NIC)** private IP address to **Static** to ensure consistent connectivity.  


![Static IP Configuration](https://i.imgur.com/KHU9kC4.png)  


By following these steps, you will have a functioning Domain Controller (`DC-1`) and Client VM (`Client-1`) ready for further Active Directory configuration in a controlled Azure environment.


</p>
<p>
# Deploying Active Directory in Azure Virtual Machines  

This guide outlines the steps to deploy a Domain Controller (Windows Server 2022) and a Client (Windows 10) within Microsoft Azure, configure their network settings, and set up Active Directory.

---

## Deployment Overview  

### Virtual Machines Setup  
- **Domain Controller (DC-1):**  
  - Operating System: Windows Server 2022  
  - Configuration: 2 VCPUs  
  - Network: Assign a static IP in network settings.  

- **Client (Client-1):**  
  - Operating System: Windows 10  
  - Network: Use the same resource group and VNet as DC-1.  

---

## Configuration Steps  

### 1. Configure Windows Firewall for ICMP Protocols  
- Log into DC-1 via **Remote Desktop**.  
- Open **Windows Defender Firewall with Advanced Security**.  
- Enable **ICMPv4 TCP Protocols** by modifying the "Protocols" section.  

  
![Firewall Setup](https://imgur.com/fxiahMT.png)  

---

### 2. Install and Configure Active Directory  
- Install Active Directory Domain Services on DC-1.  
- Create a new forest and domain.  
- Restart the machine (automatically triggered by the installation).  

  
![Add Forest](https://imgur.com/39rEkhJ.png)  

- Log back into DC-1 using the new domain and username.  
- Set up **Organizational Units (OUs)** and create users.  

---

### 3. Assign Administrator Properties to a User  
- Select a user in Active Directory.  
- Right-click → Properties → Member tab.  
- Add the user to the **Domain Admins** group by typing "domain admins" and clicking **Check Names**.  

  
![Add User Role](https://imgur.com/kzGVLjr.png)  

---

### 4. Update DNS Settings for Client-1  
- Change the DNS settings of Client-1 to the **private IP address of DC-1** in Azure.  
- Verify connectivity between Client-1 and DC-1.  
- Confirm that Client-1 is listed in the "Computers" container of Active Directory.  

 
![Change DNS Settings](https://imgur.com/G8LMrqB.png)  
![Verify Connectivity](https://imgur.com/lQCfRDf.png)  

---

### 5. Enable Domain Users for Remote Desktop Access  
- Log into Client-1 with the admin user.  
- Allow **Domain Users** access to remote desktop via **System Properties**.  

 
![Allow Users Access](https://imgur.com/TmSDbUU.png)  

---

### 6. Create Random Users in Active Directory  
- Use **PowerShell as Administrator** to run a script generating random users in the OU.  
- Alternatively, manually create users.  

 
![Generate Users](https://imgur.com/H9Y3SMB.png)  

---

### 7. Test User Login  
- Select a random user from the OU.  
- Log into Client-1 using the user credentials.  

 
![Login Test](https://i.imgur.com/aQ1W5gf.jpeg)  

---

By following these steps, you can deploy and configure Active Directory within Azure Virtual Machines, ensuring seamless communication and user management across your network.
