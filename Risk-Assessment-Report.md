# Risk Assessment Report

1. Executive Summary

    This report presents the results of a cloud security risk assessment performed on an Azure-hosted virtual machine. Viewed through a Governance, Risk, and Compliance (GRC) lens, the study evaluates the security posture of the asset within a simulated enterprise environment.

    The primary objective was to inventory critical assets, model potential threat scenarios, and assess technical vulnerabilities. By quantifying these risks, the assessment provides actionable security recommendations mapped to industry-standard frameworks like NIST and CIS to ensure a compliant and resilient configuration.

    The audit revealed several medium-to-high risks, specifically concerning exposed remote management ports, lack of multi-factor authentication (MFA), and gaps in system hardening and centralized logging. While no active compromises were found, these common cloud misconfigurations represent significant security weaknesses that require remediation to prevent future exploitation.

2. Scope and Environment

Assessment Scope:

* Single Azure Virtual Machine
* No additional cloud services or applications included
* Assessment performed from a GRC (non-exploitative) perspective

The following table summarizes the scope of the infrastructure audit, identifying the primary cloud assets and their respective configurations.

| Item | Description |
| :--- | :--- |
| **Cloud Provider** | Microsoft Azure |
| **Resource Group** | GRC-Lab |
| **Virtual Machine Name** | GRC-WIN-VM01 |
| **Operating System** | Windows Server 2022 Datacenter |
| **Access Method** | Remote Desktop Protocol (RDP) |
| **Public Exposure** | Yes (Public IP enabled) |
| **Administrative Account** | azureadmin |

3. Asset, Threat, and Vulnerability Summary

This table correlates specific technical vulnerabilities with their respective threats and provides a business-centric justification for remediation.

| Asset | Threat | Vulnerability | Why it Matters (Impact) |
| :--- | :--- | :--- | :--- |
| **Azure VM** | Brute-force attack | RDP exposed to the internet | Creates an unmonitored gateway for unauthorized external access. |
| **Admin Account** | Credential theft | No MFA | Increases the risk of a single password compromise leading to total system takeover. |
| **OS** | Exploitation | Default hardening | Leaves the system vulnerable to well-known, automated exploitation techniques. |
| **Logs** | Undetected attacks | No centralized logging | Severely limits the ability to identify, respond to, and investigate security breaches. |
| **Azure Subscription** | Misconfiguration | Single admin | Creates a single point of failure and lacks the oversight of administrative accountability. |

4. 
