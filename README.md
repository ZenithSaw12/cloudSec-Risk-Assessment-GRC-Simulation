# cloudSec-Risk-Assessment-GRC-Simulation

### Virtual Machine Creation

Created VM `GRC-WIN-VM01`

During the setup I intentionally set the public inbound port to allow RDP (3389)
This exposure will be documented as a security risk later

This VM will act as the entire assessment scope

GRC Steps

## Step 1: Identify Assets “What would hurt if compromised?”

> Confirming the operating system
>
> <img src="images/os.png" alt="Confirm OS" width="60%">

> Identify Externally Acessible Services That Increase Attack Surface
>
> <img src="images/network.png" alt="Inbound port rules" width="60%">
>
> Notice that RDP is open

> Identify Privileged Accounts With Elevated Access to The System.
>
> powershell
> ```powershell
> Get-LocalUser
> ```
>
> Output
>
> <img src="images/output.png" alt="powershell output" width="60%">
>
> Here we notice that..

> Determine if VM is Accessible From The Internet
>
> <img src="images/overview.png" alt="VM overview" width="60%">
>
> The VM is assigned a public ip. This is considered High Risk as hackers constantly run automated scripts to scan the internet for open RDP ports.

## Step 2: Identify Threats "What Could Go Wrong?"

# Asset-Specific Threat Scenario Matrix

| Asset | Threat Scenario |
| :--- | :--- |
| **Public RDP** | Internet brute-force attacks |
| **Admin account** | Password compromise |
| **OS** | Exploitation of known vulnerabilities |
| **Azure account** | Unauthorized configuration changes |
| **Logs** | Undetected malicious activity |

## Step 3: Identify Vulnerabilites "Why the Threat Could Work"

> <img src="images/nsg.png" alt="nsg screenshot" width="60%">
>
> The Network Security Group is attached to the netowrk interface and RDP is allowed in the inbound port rules. This increases the risk of brute-force and credential-based attacks.

OS-Level Confirmation

Confirm admin account exits and is a member of the Administrators group

> <img src="images/azureadmin.png" alt="admin screenshot" width="60%">

Ensuring least priviledge by ensuring to "shadow" accounts

Confirm monitoring is enabled for both Azure and OS-level

> Azure Monitoring
>
> <img src="images/monitor.png" alt="monitor screenshot" width="60%">
>
> Monitoring is enabled as metrics and basic performance data are visible

> OS-Level Logging
>
> <img src="images/logging.png" alt="event viewer screenshot" width="60%">
>
> Logs are being generated

We Assume Default OS Configuration Unless Hardened

Identified Vulnerabilities & Impact
*Technical gaps identified during the initial system audit and their potential business impact.*

| Asset | Vulnerability | Why It Matters |
| :--- | :--- | :--- |
| **Virtual Machine (VM)** | RDP exposed to the internet | Increases attack surface |
| **Authentication** | No MFA | Password compromise risk |
| **Operating System (OS)** | Default hardening | Common exploit target |
| **Monitoring** | No SIEM | Attacks may go unnoticed |
| **Identity** | Single admin | No accountability |


## Step 2: Assign Risk Scores



