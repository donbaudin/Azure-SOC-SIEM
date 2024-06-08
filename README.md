# Azure-SOC-SIEM

## SOC Cloud Security Integration

This repository contains the implementation details of a state-of-the-art Security Operations Center (SOC) tailored for modern cloud security integration. The project leverages Microsoft Sentinel as the core Security Information and Event Management (SIEM) solution, utilizing Log Analytics workspaces to aggregate and analyze logs from various platforms. It focuses on data collection, correlation, and analysis to enhance threat detection capabilities in the cloud, with a global visualization of event locations for actionable insights. The repository also includes an Azure honeynet setup and the assessment of security metrics before and after hardening measures.

![AZURE-SOC-SIEM-1](https://github.com/donbaudin/Azure-SOC-SIEM/assets/169613545/00d6b343-f08e-4053-a9de-c7c2a84e0767)


## Introduction and Objective

A miniature honeynet was set up within the Azure platform to analyze security metrics in a controlled environment. Log data from various sources were aggregated into a Log Analytics workspace, and Microsoft Sentinel used this data to create attack visualizations, trigger alert notifications, and generate incident reports.

The experiment commenced with assessing security metrics in an initially vulnerable environment over 24 hours. Following this baseline measurement, security protocols were implemented to strengthen the environment. Another 24-hour period was then dedicated to reassessing the metrics under the enhanced security posture. The findings, detailed in the following section, include metrics for:

- **SecurityEvent** (Windows Event Logs)
- **Syslog** (Linux Event Logs)
- **SecurityAlert** (Log Analytics Alerts Triggered)
- **SecurityIncident** (Incidents created by Sentinel)
- **AzureNetworkAnalytics_CL** (Malicious Flows allowed into our honeynet)

## Technologies, Azure Components, and Regulations Employed

- **Azure Virtual Network (VNet)**
- **Azure Network Security Groups (NSG)**
- **Virtual Machines** (2 Windows VMs, 1 Linux VM)
- **Log Analytics Workspace** with Kusto Query Language (KQL) Queries
- **Azure Key Vault** for Secure Secrets Management
- **Azure Storage Account** for Data Storage
- **Microsoft Sentinel** for Security Information and Event Management (SIEM)
- **Microsoft Defender for Cloud** to Protect Cloud Resources
- **Windows Remote Desktop** for Remote Access
- **Command Line Interface (CLI)** for System Management
- **PowerShell** for Automation and Configuration Management
- **Microsoft Cloud Security Benchmark
- **Azure CSPM
- **NIST SP 800-53 Revision 5** for Security Controls
- **NIST SP 800-61 Revision 2** for Incident Handling Guidance

## Architecture Before Hardening and Security Controls

![AZURE-SOC-SIEM-2](https://github.com/donbaudin/Azure-SOC-SIEM/assets/169613545/93a86ac2-60f2-403b-906b-e33c568c24b6)


**Before Hardening Measures and Security Controls:**

Before hardening, all resources were initially deployed with public exposure to the internet. This intentionally insecure setup aimed to attract potential cyber attackers and observe their tactics. The Virtual Machines had their Network Security Groups (NSGs) and built-in firewalls open, allowing unrestricted access from any source. Additionally, all other resources, such as storage accounts and databases, were deployed with public endpoints visible to the internet, without using any Private Endpoints for enhanced security.

## Architecture After Hardening and Security Controls

![AZURE-SOC-SIEM-3](https://github.com/donbaudin/Azure-SOC-SIEM/assets/169613545/f0f4c56a-f6cd-4648-9076-26a8d7b8d534)


The architecture of the mini honeynet in Azure consists of the following components:

- **Virtual Network (VNet)**
- **Network Security Group (NSG)**
- **Virtual Machines** (2 Windows, 1 Linux)
- **Log Analytics Workspace**
- **Azure Key Vault**
- **Azure Storage Account**
- **Microsoft Sentinel**

For the "BEFORE" metrics, all resources were originally deployed with exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the internet, without using Private Endpoints.

For the "AFTER" metrics, network Security Groups were hardened by blocking all traffic except from my admin workstation. Additionally, all other resources were secured by their built-in firewalls and using Private Endpoints.

## Attack Maps Before Hardening / Security Controls

![AZURE-SOC-SIEM-4](https://github.com/donbaudin/Azure-SOC-SIEM/assets/169613545/4cad27f2-8558-4d4c-82af-c0b814b7a2e6)


## Metrics Before Hardening / Security Controls

**Before Securing Environment:**

The following shows the metrics we measured in our insecure environment for 24 hours:

| Start Time            | Stop Time             | Security Events (Windows VMs) | Syslog (Linux VMs) | SecurityAlert (Microsoft Defender for Cloud) | SecurityIncident (Sentinel Incidents) | NSG Inbound Malicious Flows Allowed |
|-----------------------|-----------------------|-------------------------------|--------------------|---------------------------------------------|---------------------------------------|--------------------------------------|
| 5/11/2024, 8:49:58 PM | 5/12/2024, 8:49:58 PM | 15110                         | 3554               | 3                                           | 241                                   | 2113                                 |

**After Securing Environment:**

The following shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

| Start Time            | Stop Time             | Security Events (Windows VMs) | Syslog (Linux VMs) | SecurityAlert (Microsoft Defender for Cloud) | SecurityIncident (Sentinel Incidents) | NSG Inbound Malicious Flows Allowed |
|-----------------------|-----------------------|-------------------------------|--------------------|---------------------------------------------|---------------------------------------|--------------------------------------|
| 5/17/2024, 9:04:42 PM | 5/18/2024, 9:04:42 PM | 106                           | 1                  | 0                                           | 0                                     | 0                                    |

### Change After Securing Environment

| Metric                                | Percentage Change  |
|---------------------------------------|--------------------|
| Security Events (Windows VMs)         | -99.30%            |
| Syslog (Linux VMs)                    | -99.97%            |
| SecurityAlert (Microsoft Defender for Cloud) | -100.00%           |
| Security Incident (Sentinel Incidents)| -100.00%           |
| NSG Inbound Malicious Flows Allowed   | -100.00%           |

## Conclusion

A miniature honeynet was created within Microsoft Azure, with log sources seamlessly integrated into a Log Analytics workspace. Microsoft Sentinel was crucial in triggering alerts and managing incidents based on the ingested logs. Initially, security metrics were assessed in an intentionally insecure environment, where all resources were exposed to the internet with open Network Security Groups, built-in firewalls, and public endpoints. Following this baseline assessment, security measures were implemented: Network Security Groups were hardened to block all traffic except from the admin workstation, and resources were secured with built-in firewalls and Private Endpoints. The reassessment of security metrics post-implementation showed a significant reduction in security events and incidents, highlighting the effectiveness of these measures. However, it’s important to note that if the network's resources had been heavily utilized by regular users, a higher volume of security events and alerts might have been generated, suggesting that ongoing vigilance and adjustment of security protocols are essential for maintaining robust protection, vigilance and adjustment of security protocols for maintaining robust protection.
