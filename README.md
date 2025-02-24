<h1 align="center">Active Directory Project</h1> 
<h1 align="center">
  
[![Made With](https://img.shields.io/badge/Made%20With-483d4b)](http://www.firsttimersonly.com/)
[![Splunk](https://img.shields.io/badge/Splunk-77a33b)](http://www.firsttimersonly.com/)
[![Kali Linux](https://img.shields.io/badge/Kali%20Linux-2688f0)](http://www.firsttimersonly.com/)
[![Windows Server 2022](https://img.shields.io/badge/Windows%20Server%202022-29903b)](http://www.firsttimersonly.com/)
[![Windows 10 Pro](https://img.shields.io/badge/Windows%2010%20Pro-4cb17b)](http://www.firsttimersonly.com/)
[![Ubuntu Server](https://img.shields.io/badge/Ubuntu%20Server-e2511f)](http://www.firsttimersonly.com/)

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)

</h1>

This repository guides you in setting up an Active Directory (AD) home lab with Splunk, Kali Linux, and Atomic Red Team (ART) to simulate real-world cyber threats. It is ideal for cybersecurity enthusiasts, SOC analysts, and IT professionals, providing hands-on experience in threat detection, log analysis, and attack simulation in a safe environment.
<br><br>

## Table of Contents
- [Build a Logical Diagram](#build-a-logical-diagram)
- [System Requirements](#system-requirements)
- [Install Virtual Machines](#install-virtual-machines)
- [Install and Configure Software](#install-and-configure-software)
- [Configure Active Directory](#configure-active-directory)
- [Generate Telemetry With Kali](#generate-telemetry-with-kali)
<br><br>
## Build a Logical Diagram
For drawing a logical diagram visit: [draw.io](https://app.diagrams.net/)

Watch Tutorial: [Build a Logical Diagram](https://youtu.be/mWqYyl89QaY?si=gVTKNjYdiqw51iAU)

![Diagram](https://github.com/user-attachments/assets/ffa454b9-0ebd-40ee-8fa4-04fbee57cd84)

[Move To Top](#table-of-contents)
<br><br>
## System Requirements
Here's a table summarizing your VM system requirements:

| **Virtual Machine**              | **RAM** | **Storage** | **CPU Cores** |
|----------------------------------|---------|-------------|---------------|
| Windows 10 Pro VM                | 8 GB    | 50 GB       | 1             |
| Windows Server 2022 VM (AD)      | 8 GB    | 50 GB       | 1             |
| Ubuntu Server VM (Splunk Server) | 8 GB    | 100 GB      | 2             |
| Kali Linux VM (Attacker)         | 4 GB    | 50 GB       | 1             |
| **Total**                        | 28 GB   | 250 GB      | 5             |


[Move To Top](#table-of-contents)
<br><br>
## Install Virtual Machines
Here's the table summarizing the download links and sizes for your virtual machines:

| **Virtual Machine**              | **Download Link**                                                                                               | **Size**          |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------|-------------------|
| Kali Linux                       | [Kali Linux](https://www.kali.org/)                                                                             | 3 GB approx       |
| Windows 10 Pro                   | [Windows 10 Pro](https://www.microsoft.com/en-us/software-download/windows10?msockid=2bd229687f9c6c1e186f3c0d7e2e6d4f) | 5 GB approx       |
| Windows Server 2022              | [Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022?msockid=2bd229687f9c6c1e186f3c0d7e2e6d4f) | 5 GB approx       |
| Ubuntu Server                    | [Ubuntu Server](https://ubuntu.com/download/server)                                                              | 3 GB approx       |

Watch Tutorial: [Install Virtual Machines](https://youtu.be/2cEj3bS5C0Q?si=4NyRVKhv2nOBCIaf)

[Move To Top](#table-of-contents)
<br><br>
## Install and Configure Software

### Objective
Install and configure Sysmon and Splunk on Windows Server 2022 (Active Directory) and Windows 10 Pro. The configuration steps are the same for both systems. The process will be demonstrated on Windows 10 Pro, and the same steps can be applied to Windows Server 2022 with the appropriate IP address changes (192.168.10.100 for Windows 10 Pro and 192.168.10.7 for Windows Server 2022).

### Steps

#### Step 1: Create a New Subnet
1. Open VirtualBox.
2. Click on the three dots on the Tools tab.
3. Go to Networks -> NAT Networks -> Click on "Create".
4. Give your subnet a name and IPv4 prefix.
5. Tick "Enable DHCP" and press "Apply".

Now, go to each VM setting and change the network adapter to the NAT network. Your specified network name will appear automatically, e.g., `ad-project`.

#### Step 2: Configure Splunk Server on Ubuntu Server
1. Install Splunk on the Ubuntu server.
2. Follow the Splunk setup instructions to complete the configuration.

#### Step 3: Configure Sysmon & Splunk Universal Forwarder on Windows 10 Pro
1. Configure network settings to access the subnet created above.
2. Verify the subnet configuration by pinging the Ubuntu server, e.g., `ping 192.168.10.4`.
3. Download and install Sysmon on Windows 10 Pro.
4. Configure Sysmon with the appropriate configuration file.
5. Download and install Splunk Universal Forwarder on Windows 10 Pro.
6. Configure the Splunk Universal Forwarder to forward logs to the Splunk server.

If configured properly, you can access the Splunk dashboard at:
```http://your-splunk-server-ip:8000```
For example: ```http://192.168.10.4:8000``` in this case.

**Note**: Allow ports 8000 and 9997 on the Ubuntu server.

#### Step 4: Repeat Step 3 for Windows Server 2022
Follow the same steps as in Step 3 for Windows Server 2022. Use the corresponding IP address for Windows Server 2022 (192.168.10.7).

![image](https://github.com/user-attachments/assets/614726e9-5643-40d4-82bd-47fb0622170b)


Watch Tutorial: [Install and Configure Software](https://youtu.be/uXRxoPKX65Q?si=EPI77sZXcpjyejDN)

[Move To Top](#table-of-contents)
<br><br>
## Configure Active Directory

### Objective
Install and configure Windows Server 2022 (AD) to promote it to a Domain Controller and join Windows 10 Pro to the domain.

#### Steps

##### Step 1: Install and Configure Active Directory Domain Services (ADDS)
1. On your Windows Server 2022, open Server Manager.
2. Navigate to `Add roles and features`.
3. Select `Role-based or feature-based installation` and choose your server.
4. In the `Server Roles` section, select `Active Directory Domain Services` and complete the installation.
5. After installation, promote the server to a domain controller by opening the AD DS Configuration Wizard. Follow the prompts to create a new forest named `splunk.local` (replace with your own domain if different).

##### Step 2: Create Organizational Units (OUs)
1. Open `Active Directory Users and Computers`.
2. Right-click on your domain and select `New > Organizational Unit`.
3. Create two OUs: `IT` and `HR`.

##### Step 3: Create Users in Each Organizational Unit
1. In the `IT` OU, right-click and select `New > User`.
2. Create a user (e.g., ITUser) and set a password.
3. Repeat the `HR` OU steps to create a user (e.g., HRUser) and set a password.
4. Note down the usernames and passwords for later use.

##### Step 4: Configure DNS on Windows 10 Pro VM
1. Open your Windows 10 Pro VM.
2. Navigate to `Network and Sharing Center > Change adapter settings`.
3. Right-click on your network adapter and select `Properties`.
4. Select `Internet Protocol Version 4 (TCP/IPv4)` and click on `Properties`.
5. Set the `Preferred DNS server` to the IP address of your Windows Server 2022 (e.g., 192.168.10.7).

##### Step 5: Join Windows 10 Pro VM to the Domain
1. Open `Settings` on Windows 10 Pro VM.
2. Go to `Accounts > Access work or school`.
3. Click `Connect` and select `Join this device to a local Active Directory domain`.
4. Enter the domain name (e.g., splunk.local) and click `Next`.
5. Enter the Windows 10 Pro administrator credentials (e.g., Administrator: YourPassword).

##### Step 6: Log in with the Created User
1. Restart your Windows 10 Pro VM.
2. On the login screen, select `Other user`.
3. Enter the username and password of one of the users created in Step 3 (e.g., ITUser or HRUser).
4. Login and verify that the domain join was successful.

Watch Tutorial: [Configure Active Directory](https://youtu.be/1XeDht_B-bA?si=Co09joMXt5RcZTEl)

[Move To Top](#table-of-contents)
<br><br>
## Generate Telemetry With Kali
1. Make a firewall rule on Windows 10 Pro for port 3389 (RDP) and ICMP.
2. Simulate attacks using Kali Linux.

Watch Video Walkthrough: [Generate Telemetry](https://www.linkedin.com/posts/mitesh-rathod-8023b7176_cybersecurity-soc-threathunting-activity-7292903151223951361-Qvu3?utm_source=share&utm_medium=member_desktop)


[Move To Top](#table-of-contents)

