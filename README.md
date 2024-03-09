# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/Ultrainstinct1995/SandBox/assets/155921166/4e65b93a-a2e5-435a-a4fc-f4f27061591c)


## Introduction

In this project, I constructed a miniature honeynet within the Azure cloud platform. I gathered log data from diverse sources and consolidated them into a Log Analytics workspace. Subsequently, Microsoft Sentinel leveraged this data to construct visual attack maps, generate alerts, and manage security incidents.

The project involved a two-phase approach: initially, I assessed security metrics within the vulnerable environment over a 24-hour period. Following this, I implemented various security controls to fortify the environment and monitored metrics for an additional 24 hours.

The showcased metrics include

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

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
![image](https://github.com/Ultrainstinct1995/SandBox/assets/155921166/ba5fe134-41fb-4168-9a38-9a15a0e513bc)
![image](https://github.com/Ultrainstinct1995/SandBox/assets/155921166/48a4cc5a-7aa3-45b6-9273-10dc87be9721)
![image](https://github.com/Ultrainstinct1995/SandBox/assets/155921166/abfbee28-6fc2-44d5-a72e-ec96107878b6)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

`![image](https://github.com/Ultrainstinct1995/SandBox/assets/155921166/b33df8d8-378d-442b-bf97-19f3c16fd459)

## Metrics After Hardening / Security Controls
All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

The table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls.


## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
