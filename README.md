# Creating a Security Operations Center (SOC) and Honeynet in Microsoft Azure with Live Traffic.
![image](https://github.com/bconway1906/CLOUD-SOC-HONEYNET/assets/148906255/8b6c94e1-5548-42b4-91e4-91acc2e131f5)


## Introduction

In this project, I set up a small honeynet within Microsoft Azure, collecting logs from various sources into a Log Analytics workspace. Microsoft Sentinel was then used to generate attack maps, trigger alerts, and create security incidents. I conducted security metric measurements in an initially vulnerable environment for 24 hours, implemented security controls to enhance security, measured metrics for an additional 24 hours, and present the following results.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Mini Honeynet Architecture
The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network
- Network Security Group
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

![image](https://github.com/bconway1906/CLOUD-SOC-HONEYNET/assets/148906255/513093f2-7303-42a9-8911-3989960d07c0)

## Architecture Before Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

In the initial configuration, all resources were deployed with exposure to the internet. This setup left Virtual Machines vulnerable, as both their Network Security Groups and built-in firewalls allowed unrestricted inbound and outbound traffic. Furthermore, all other resources had public endpoints that were accessible from the internet, rendering the need for Private Endpoints redundant.

## Architecture After Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The Network Security Groups underwent a substantial security enhancement, implementing a strict block on all network traffic except for that originating from my admin workstation. Furthermore, the remaining resources were fortified by utilizing both their built-in firewalls and Private Endpoints for enhanced protection.

## Attack Maps Before Security Controls
![image](https://github.com/bconway1906/CLOUD-SOC-HONEYNET/assets/148906255/f9df8bf9-2297-4d0d-9929-31967485e847)<br>
![image](https://github.com/bconway1906/CLOUD-SOC-HONEYNET/assets/148906255/216db8ff-fc86-4d7f-b573-cea3f2db4f5f)<br>
![image](https://github.com/bconway1906/CLOUD-SOC-HONEYNET/assets/148906255/fc2eb31d-c07d-48ed-9d67-cbed4371f1f5)<br>
![image](https://github.com/bconway1906/CLOUD-SOC-HONEYNET/assets/148906255/a2b7af8e-90d6-4dab-968a-208384d23e99)<br>

## Metrics Before Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 10/23/2023 10:30 AM
Stop Time 10/24/2023 10:30 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 42554
| Syslog                   | 951
| SecurityAlert            | 14
| SecurityIncident         | 130
| AzureNetworkAnalytics_CL | 2896

## Attack Maps After Security Controls

All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after implementing security controls

## Metrics After Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 
Stop Time	

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 15000
| Syslog                   | 8
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, we established a miniature honeynet within Microsoft Azure, seamlessly integrating log sources into a Log Analytics workspace. Employing Microsoft Sentinel, we harnessed the log data to trigger alerts and create security incidents. Before implementing security controls, we initially measured metrics in the less secure environment and then repeated the process post-implementation. Notably, the implementation of these security measures led to a significant reduction in the number of security events and incidents, underscoring their effectiveness.
