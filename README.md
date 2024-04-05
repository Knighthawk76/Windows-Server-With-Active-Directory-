# Windows-Server-With-Active-Directory and Powershell Automation-

![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I build a full blown active directory lab on a windows server from my desktop computer using Oracle Virtual Box. Upon creating the server and active directory infastructure, I leverage powershell to execute a script that automates the onboarding of  1000 users. This greatly decreases time and effort as well as the potential of human errors. The goal is to gain a better understanding of Active Directory operations, the power of Powershell, and to gain a better understanding of Windows server administration.     

## Resources and Tools

For this project I will be leveraging my home computer, Windows Server 2019 which will be my domain controller, a Windows 10 virtual machine as a client, and Oracle Virtual Box as the tool to architect my Virtual Desktop Infrastructure. I leveraged powershell to do some of the heavy lifting like creating 1000 users which might simulate the scale of a small organization.  The script is also scalable if there were a need to add and create more users, and it was a strong ally for saving me time. The domain controller will house our active directory, and will be configured with two network interface cards(NIC). One will be used for outside internet and the other to the private networks (virtual Box).     


![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/da615c01-fb6d-496c-8b0c-d27049fce35d)
![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/ca80f909-7858-4ce7-ba29-2f8dedc05ac6)
![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/f54626eb-0cee-415f-8a58-a497c9ee6e18)




## Task 1 Configuring the Domain Controller
I installed Oracle Virtual Box, Windows server ISO, and Windows 10 ISO. Used the Server ISO as the image for the Domain controller Image. Adjusted settings in oracle to allocate 3 processors and 2gb of memory. This may not be enough for some workloads, but it was sufficient for my project. Successful installation and configurations resulted in a base server infrastructure. 

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/e29e4139-d3a0-4150-af41-dae2327b6c61)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/92965273-e3d1-43d1-ac6c-1f1a7c80760a)

## Task 2 more configuring 

The next thing is to add the funcionality I needed for my server. I proceeded with assigning IP adressing for the internal network. the external network gets addressing for the my home router. Next I name the server, and add Active Directory, and configure Nat and routing so all the clients on my private networks can connect to the internet. I also setup a DHCP on the domain controller so my clients can automatically recieve an IP address.


![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/f794ce1d-78b9-488c-88dd-3dd36283b285)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/7d8c191b-c579-4e5a-a2bf-afcbc2f2c48c)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/6114d2eb-7e82-49a4-9ad9-2bd4641f679a)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/8d7418aa-7272-47fb-a003-3457ab6edffc)


## Task 3 Powershell script on the Domain Controller

Here I am using a script that generates users and groups them into user by username. Leveraging the script created the users OU and assigned a username for all onboarded candidates.  



![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/fea5d7fb-4e26-494b-b6a3-a52a50a78e2e)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/b5a2d262-17ea-482e-8515-c264f7feb60d)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/e3d70a14-4fd7-4593-8600-324911fb5691)

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/e5f603ce-1ae7-4190-911a-c3ae98610305)


## Task 4 Install and Configure Windows 10 Client

Last step is creatng the Windows 10 client in Virtual Box

![Architecture Diagram](https://github.com/Knighthawk76/Windows-Server-With-Active-Directory-/assets/152114740/6f24b218-a4e9-416b-9434-0db6d4fa5f93)








The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
