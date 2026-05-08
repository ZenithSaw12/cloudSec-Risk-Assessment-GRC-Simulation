# cloudSec-Risk-Assessment-GRC-Simulation

### Virtual Machine Creation

Created VM `GRC-WIN-VM01`

During the setup I intentionally set the public inbound port to allow RDP (3389)
This exposure will be documented as a security risk later

This VM will act as the entire assessment scope

GRC Steps

Step 1: Identify Assets “What would hurt if compromised?”

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



