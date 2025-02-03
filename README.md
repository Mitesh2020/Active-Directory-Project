<h1 align="center">Active Directory Project</h1> 
<h1 align="center">
  
[![Made With](https://img.shields.io/badge/Made%20With-483d4b)](http://www.firsttimersonly.com/)
[![Splunk](https://img.shields.io/badge/Splunk-77a33b)](http://www.firsttimersonly.com/)
[![Kali Linux](https://img.shields.io/badge/Kali%20Linux-2688f0)](http://www.firsttimersonly.com/)
[![Atomic Red Team](https://img.shields.io/badge/Atomic%20Red%20Team-d1212e)](http://www.firsttimersonly.com/)

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
- [Generate Telemetry With Kali and ART](#generate-telemetry-with-kali-and-art)
<br><br>
## Build a Logical Diagram
For drawing a logical diagram visit: [draw.io](https://app.diagrams.net/)

Watch Tutorial: [Build a Logical Diagram](https://youtu.be/mWqYyl89QaY?si=gVTKNjYdiqw51iAU)

![Diagram](https://github.com/user-attachments/assets/6870952a-2def-42b9-a9b5-30ab2bafa719)

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
[Move To Top](#table-of-contents)
<br><br>
## Generate Telemetry With Kali and ART
[Move To Top](#table-of-contents)

