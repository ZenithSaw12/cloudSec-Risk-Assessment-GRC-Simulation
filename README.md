# Cloud Security Risk Assessment & GRC Simulation (Azure)

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


## Step 2: Assign Risk Scores (Quantifying Risk)

Risk Scoring Method
To quantify the identified risks, the following scoring system was utilized:

* **Likelihood:** 1 (Low) → 5 (High) - How probable it is that the threat will occur?
* **Impact:** 1 (Low) → 5 (High) - The severity of damage if the threat is realized.
* **Risk Score:** Likelihood × Impact

Risk Register (Core GRC Artifact)

This register documents the qualitative risk assessment for the Azure lab environment. Risks are calculated using the **NIST SP 800-30** formula: `Likelihood × Impact = Risk Score`.

| Asset | Threat | Likelihood | Impact | Risk Score | Justification |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **RDP** | Brute-force attack | 4 | 4 | 16 | Public Exposure |
| **Admin** | Credential compromise | 3 | 5 | 15 | Full System Control |
| **OS** | Unpatched vulnerabilities | 3 | 4 | 12 | Common Windows Attack |
| **Azure** | Privilege misuse | 2 | 5 | 10 | High Impact |
| **Logs** | Undetected attack | 3 | 3 | 9 | Delayed Responses |

## Step 3: Map Controls to Policies & Frameworks

Select a Framework: e.g. NIST CSF, CIS Critical Security Controls, etc.

Control Identification: e.g. preventive, detective, corrective.

# Control Mapping Table

This table maps identified risks to specific security controls and industry-standard frameworks (CIS and NIST CSF), demonstrating a structured approach to risk mitigation.

| Risk | Security Control | Control Type | Framework |
| :--- | :--- | :--- | :--- |
| **RDP attacks** | Restrict IP access | Preventive | CIS 4 |
| **Credential theft** | MFA enforcement | Preventive | NIST PR.AC |
| **OS exploits** | Patch management | Corrective | CIS 7 |
| **No detection** | Centralized logging | Detective | NIST DE.CM |
| **Privilege misuse** | RBAC | Preventive | CIS 5 |

Explanation:

* RDP attacks are mitigated by restricting inbound traffic to trusted IPs (CIS 4; Preventive) to mitigate brute-force attacks.

* Credential theft is addressed through Multi-Factor Authentication (NIST PR.AC; Preventive).

* Operating system exploits are reduced through patch management (CIS 7; Corrective) to remediate vulnerabilities.

* Lack of visibility/detection is mitigated by centralized logging (NIST DE.CM; Detective) to address visibility gaps.

* Privilege misuse is controlled through Role-Based Access Control (CIS 5; Preventive) to enforce least privilege and prevent privilege misuse.
