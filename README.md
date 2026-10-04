# ActionDetectionLab


# Building a SOC + Honeynet in Azure (Live Traffic)
<img width="1049" height="593" alt="image" src="https://github.com/user-attachments/assets/32fff895-0f50-4327-8b76-23a7398ff800" />



## Introduction

In this project, I architected a sophisticated honeynet within the Azure cloud ecosystem and integrated log sources from a multitude of resources into a Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel to construct dynamic attack maps, initiate alerts, and orchestrate incident responses. Initially, I conducted a 24-hour evaluation of various security metrics in this intentionally vulnerable environment. Afterward, I implemented stringent security measures to enhance the system's defenses and performed a subsequent 24-hour assessment to gauge the effectiveness of these improvements. The comparative analysis of these metrics is presented below. The metrics  will showcase are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls



## Architecture After Hardening / Security Controls
<img width="1034" height="596" alt="image" src="https://github.com/user-attachments/assets/c312925c-d5d0-4a5a-9f6b-1d384fae7a33" />

<img width="1058" height="580" alt="image" src="https://github.com/user-attachments/assets/2799d22e-d0b8-4fc9-a891-a2efb41ac220" />


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially provisioned with unrestricted internet exposure. Specifically, the Virtual Machines were configured with Network Security Groups (NSGs) and integrated firewalls set to allow all inbound and outbound traffic, effectively leaving them without any security constraints. Moreover, every resource within the deployment had public endpoints accessible directly from the internet, with no utilization of Private Endpoints to mitigate exposure to potential threats.

In the "AFTER" state, a rigorous security enhancement protocol was implemented. The Network Security Groups were hardened, blocking all traffic except that originating from a pre-authorized administrative workstation. Concurrently, all other resources were secured using a dual-layer protection strategy: their inherent firewalls were meticulously configured, and Private Endpoints were employed to obfuscate them from the public internet. This approach significantly minimized the attack surface and enhanced the overall security posture of the deployment.

## Attack Maps Before Hardening / Security Controls
<img width="1065" height="606" alt="image" src="https://github.com/user-attachments/assets/0f7f51f7-b238-49a0-bed6-0c0b766d1d1b" />
<img width="1057" height="599" alt="image" src="https://github.com/user-attachments/assets/8dd38a60-60c5-40d0-9c94-a88ee25d0d96" />
<img width="1058" height="600" alt="image" src="https://github.com/user-attachments/assets/a1487263-b42f-473c-a8dc-332a071b7f91" />


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-05-28 08:04
Stop Time 2024-05-29 08:04

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 90513
| Syslog                   | 5619
| SecurityAlert            | 5
| SecurityIncident         | 267
| AzureNetworkAnalytics_CL | 1709

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-05-30 08:04
Stop Time	2023-05-31 08:04

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 110
| Syslog                   | 334
| SecurityAlert            | 1
| SecurityIncident         | 2
| AzureNetworkAnalytics_CL | 0

## Conclusion

I architected an advanced honeynet within the Microsoft Azure framework, seamlessly integrating log sources into a Log Analytics workspace. Leveraging Microsoft Sentinel, configuring alerts and orchestrated incident responses based on the ingested log data.

To ascertain the efficacy of  security controls, I conducted a thorough evaluation of metrics within the unsecured environment, followed by a reassessment post-implementation. The findings were compelling: there was a marked reduction in security events and alerts, underscoring the robustness of my security measures.

Furthermore, it is worth noting that with intensive utilization of network resources by regular users, the volume of security events and alerts might have been higher within the initial 24-hour period following the implementation of the security controls. This potential variability further validates the strength and adaptability of our security strategies.
